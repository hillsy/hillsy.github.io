---
layout:     post
title:      "Shirky, Conway, and designing for the long term"
readout:    "Why your digital service should be independent of your current temporary organisational reality"
date:       2015-11-11
categories: architecture, servicedesign, ontology
comments:   true
---

Clay Shirky's [Ontology is Overrated] [1] is one of my all-time favourite articles about the way information should be, often is, and often isn't, organised on the World Wide Web.

His main theme is that information on the Web is completely decentralised. It's impossible and indeed **undesirable** to impose a centralised, comprehensive classification system (like a library catalogue) onto it. If people want to associate bits of information on the Web with other bits, that's up to them and the Web allows them to do that in a very direct way. Hyperlinks are powerful things.

Shirky also says that centralised, comprehensive classification systems exist to solve problems that don't even apply to the digital realm. For example library catalogues optimise for the amount of space taken up by books on a library shelf, or for the fact that a book can't be on two different shelves at once.

Both these ideas have implications for how we design digital services. Direct linking and Google searches happen; we shouldn't assume that users will follow a predetermined path to a service entry point. We should assume that users will follow a multiplicity of paths. We shouldn't try to rigidly pigeon-hole information into one particular category.

People familiar with [Conway's Law] [2] will recognise some of these ideas. The design of a system will tend to reflect the structure of the organisation building it. Actually Conway says *communication* structure, but I suspect it's a bit broader than that. System designs can also reflect the structure of the organisation as it perceives itself, even if that's not how the organisation's really structured. And designs can reflect organisational thinking about classification and hierarchy which may be be quite constrained ("thing A is the domain of department B, so that's where it must go in the UI"). We're back at Shirky again.

(Hands up if you've ever worked on or used a website or application that falls into these traps. OK, hands down, thanks). Service designers, please stop doing this.

Shirky has another interesting idea too. Classification systems are effectively fortune telling the future. The categoriser is expected to come up with categories that not only make sense to all end users, but that are also future proof.

Here's Clay:

> Consider the following statements:
>   A: "This is a book about Dresden."
>   B: "This is a book about Dresden, and it goes in the category 'East Germany'." 
> That second sentence seems so obvious, but East Germany actually turned out to be an unstable category. Cities are real. They are real, physical facts. Countries are social fictions. It is much easier for a country to disappear than for a city to disappear, so when you're saying that the small thing is contained by the large thing, you're actually mixing radically  different kinds of entities.

In a recent job for a large public sector organisation, I was partly responsible for branding and domain names for some digital services. This organisation, along with many other public organisations, would occasionally get reorganised out of existence according to the political currents of the time. Its two predecessor organisations had lasted about eight years each. But here's the thing: this third incarnation was still managing many of the services developed 15-odd years earlier. These services were important; much more so than the name of the organisation that was managing them.

Sometimes these services would have close ties to the branding, corporate "message", enterprise architecture and so on of the predecessor organisations. This made it difficult and costly to transition to the new, and ultimately temporary, organisational reality.

Now, go back to Clay's example of classifying a book about "Dresden" into "East Germany". Substitute "important digital service" for "city", "organisation" for "country" and "bureaucratic construct" for "social fiction". It's pretty easy to see why we should be careful about tying digital services too closely to the organisational/political structure *du jour*.

[1] http://www.shirky.com/writings/ontology_overrated.html "Ontology is Overrated: Categories, Links, and Tags"
[2] http://www.melconway.com/Home/Conways_Law.html         "Conway's Law"