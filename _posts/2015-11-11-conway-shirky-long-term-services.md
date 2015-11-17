---
layout:       post
title:        "Shirky, Conway, and designing for the long term"
readout:      "Why your digital service should be independent of your current temporary organisational reality"
image:
 - file:      card-catalogue.jpg
   credit:    https://commons.wikimedia.org/wiki/File%3ACard_Catalog_2.jpg
   alt:       "Picture of a library card catalogue"
date:         2015-11-11
categories:   architecture, servicedesign, ontology
comments:     true
---

Clay Shirky's *Ontology is Overrated* [^1] is one of my all-time favourite articles about the way information should be, often is, and often isn't, organised on the World Wide Web.

The main theme in the article is that information on the Web is completely decentralised. It's impossible and indeed **undesirable** to kludge a centralised, comprehensive classification system (like a library catalogue) onto it. If people want to associate bits of information on the Web with other bits, that's up to them and they can do it in a very direct way. Hyperlinks are powerful things.

Shirky also says these library-like classification systems exist to solve problems that are irrelevant in the digital realm. For example library catalogues optimise for the amount of space taken up by books on a library shelf, or for the fact that a book can't be on two different shelves at once. But in cyberspace storage is - for most practical purposes - infinite. And there are several ways to make digital information "be" in a number of places at once.

There are implications here for how we should design digital services. We shouldn't try to pigeon-hole information into one particular classification category. We shouldn't assume that users will follow a predetermined path to a service entry point; direct linking and Google searches for information happen. We should assume that users will follow a multiplicity of paths.

People familiar with Conway's Law [^2] will be on familiar territory. The design of a system tends to reflect the communication structure of the organisation building it. Conway says *communication* structure, but I suspect his law should be broader. System designs can also reflect the organisation's *theoretical* (on paper) structure, even if that's not how it is in reality. They can also reflect constrained collective thinking - and here's the tie-in with Shirky - about classification and hierarchy. "Thing A is the domain of department B, so that's where it goes in the UI".

Hands up if you've ever worked on or used a website or application that falls into these traps. OK, hands down, thanks. Service designers, please stop doing this.

Shirky's got more though, and this is where we start breaking newer ground for digital service design. If you maintain a centralised, comprehensive classification system, categorisers are expected to come up with categories that not only make sense to all end users, but that are also future proof. Here's what he says:

> Consider the following statements:
>
>   A: "This is a book about Dresden."
>
>   B: "This is a book about Dresden, and it goes in the category 'East Germany'."
>
> That second sentence seems so obvious, but East Germany actually turned out to be an unstable category. Cities are real. They are real, physical facts. Countries are social fictions. It is much easier for a country to disappear than for a city to disappear, so when you're saying that the small thing is contained by the large thing, you're actually mixing radically  different kinds of entities.

I once worked on branding and domain names for some digital services deployed in the public sector. The organisation running the services would occasionally get reorganised out of existence according to the political currents of the time. This wasn't new; its two predecessor organisations had lasted about eight years each. And the same was happening to plenty of other organisations.

But here's the thing: this third incarnation was still managing many of the services developed 15-odd years earlier by the predecessor organisations. These services were important; much more so than the name of the organisation that was managing them.

Sometimes these services would have close ties to the branding, corporate "message", enterprise architecture and so on of the predecessor organisations. If nothing else, they'd often have ties to the domain name. This made it difficult and costly to transition to the new, and still ultimately temporary, organisational reality.

So, back to Clay's example of classifying a book about "Dresden" into "East Germany". Substitute "important digital service" for "city", "organisation" for "country" and "bureaucratic construct" for "social fiction". It's pretty easy to see why we should be careful about tying digital services too closely to the organisational/political structure *du jour*.

[^1]: <http://www.shirky.com/writings/ontology_overrated.html>

[^2]: <http://www.melconway.com/Home/Conways_Law.html>