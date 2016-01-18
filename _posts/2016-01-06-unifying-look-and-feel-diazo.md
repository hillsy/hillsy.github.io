---
layout:       post
title:        "Unifying site look & feel with Diazo"
readout:      "Applying lipstick to a heterogeneous plethora of backend systems"
image-file:   tux-cookie-cutter.jpg
image-alt:    "Tux (penguin) cookies, and a cookie cutter"
image-credit: https://www.flickr.com/photos/cookingforgeeks/4358890809
date:         2016-01-06
categories:   post
tags:         [diazo, python, plone, sysadmin, architecture]
comments:     true
---

### Systems integration from the user's perspective

A place I once worked had quite a big website. It ran on a CMS that was good for content but was pretty difficult to extend with new features. A lot of large monolithic systems are like that, which doesn't stop people trying to get them to do things they're not suited for. When what you have is a large hammer (and possibly you've invested quite a lot of money or time in hammer licenses or training), all your digital problems start to look very nail-ish.

Eventually it came to pass that some parts of the site infrastructure needed to be updated. We took the opportunity to think about some improvements. We recognised the **user** didn't really care what system was being used to serve the site; they cared about a consistent experience. We also recognised that different technology stacks were better for different types of problems, and that different teams in the organisation used different technologies according to their own preference. We also noticed the web applications developed by these different teams were - ahem - variable in terms of their front end standards compliance, and didn't offer a consistent user experience.

So one goal of the infrastructure update was to build something that:

  * Applied consistent corporate branding and UX (navigation elements etc) across a number of different backend systems, and

  * Did so in a technology-agnostic way, ideally without having to significantly alter the code of the backend systems themselves.

This would allow us to better separate content from presentation code. It'd also reduce the burden on other teams and give a more consistent and better quality user experience, because we'd maintain branding, navigation elements and so on centrally.

### Enter Diazo

About this time I came across a presentation [^1] from the folks at Netsight [^2] who we'd worked with before. Charmingly titled *Lipstick on a Pig* it talked about how they'd used a tool called Diazo [^3] to change the user-facing presentation of a legacy .NET system. It was immediately obvious that this was something we could use.

Diazo is some open source software that applies a static HTML theme to a website created using any technology. It takes a set of rules and an HTML template as input, and "compiles" those into an XSLT [^4] file for you. Deployed on an intermediary reverse-proxying web server (we used Apache) the XSLT file can be used to change the HTML markup of some or all your proxied services.

Here's a diagram:

![Diazo architecture](/assets/diazo-architecture.png){:class="img-responsive"}

So we applied the template to a number of backends including:

  * Static content. These were things teams had written themselves and given us to host. The only thing they had to do was include a specific class in the `<body>` tag; we could then create a rule that lifted the entire `<body>` of their document into our template.

  * The content management system. This was Plone, and Diazo itself was developed by the Plone community. However it's important to realise there's **nothing Plone-specific about Diazo**. We could have been using SilverStripe, Drupal, WordPress, Umbraco or any system that serves content over HTTP.

  * Web applications. These were a disparate bunch, and one of the main reasons for doing this in the first place. The applications themselves remained completely standalone from a technical perspective, but we were able to consistently integrate them into our website from the user perspective.

### So how did we do?

This was quite a successful project. It solved a problem that, as far as I know, a lot of heterogeneous digital estates have. It's still in production several years later, serving around 1 million visits a month. It was easy to deploy with a basic understanding of Python deployment tools, and a basic understanding of how to configure a web server as a reverse proxy. Performance was good; when benchmarked the backend services were the bottleneck, not the transform server.

One reason for blogging about it now is that it never really got much recognition; only a few other teams ever started using it. Perhaps we didn't do a good job of explaining the clear benefits. Maybe the benefits weren't as clear as we thought. Perhaps people were nervous about centralising their look and feel, or perhaps they simply didn't care that much about consistent user experience. Centralised tools like this would probably see better adoption if they're in support of a central mandate ("you must use this") or strategy ("we're going to make UX a priority"). We didn't have those.

There are some things we didn't try. The Diazo documentation talks about deploying it in a WSGI pipeline. We never did this; a simple HTTP proxy worked fine. We also only used it for anonymous content on public websites. It would have been interesting to try it on a site that had user accounts and personalisation.

### Some example code, Luke

Here's a short example. It assumes you already know a bit about how to use the command line, virtualenv, and both operating system and Python packages.

1. Set up the environment

        virtualenv diazo
        cd diazo && source bin/activate
        pip install zc.buildout

2. lxml is a dependency; this buildout downloads and compiles the correct version (alternative buildouts and installation methods are in the Diazo documentation [^5])

        curl http://hillsy.org/assets/diazo-buildout.cfg > buildout.cfg
        bin/buildout -v

3. ...some stuff happens... *...quite a bit if you're compiling lxml...*

4. Get and compile a sample theme. You can see a full list of command line flags with `bin/diazocompiler --help`

        svn co https://svn.plone.org/svn/collective/collective.examples.diazo/trunk/collective/examples/diazo/static/collective-xdv-example/ ./theme
        bin/diazocompiler -r theme/rules.xml -o theme/theme.xsl

7. Sample config to deploy the XSLT to your web server (Apache in this case)

        # see http://docs.diazo.org/en/latest/deployment.html#apache
        LoadModule transform_module /usr/lib/apache2/modules/mod_transform.so
        <VirtualHost *>

             FilterDeclare THEME
             FilterProvider THEME XSLT resp=Content-Type $text/html

             TransformOptions +ApacheFS +HTML +HideParseErrors
             TransformSet /path/to/theme.xsl
             TransformCache /path/to/theme.xsl /etc/apache2/theme.xsl

             <LocationMatch "/">
                FilterChain THEME
             </LocationMatch>

        </VirtualHost>

There's quite a lot more can be done with the web server configuration. Such as applying the theme to only certain URLs, and creating a custom error page. The latter is unfortunately necessary as Apache errors don't go through the filter chain but wasn't a problem in practice; we just shipped error pages as part of the static theme.

[^1]: <http://www.slideshare.net/hammertoe/lipstick-on-a-pig>

[^2]: <http://www.netsight.co.uk>

[^3]: <http://diazo.org>

[^4]: <https://en.wikipedia.org/wiki/XSLT>

[^5]: <http://docs.diazo.org/en/latest/installation.html>
