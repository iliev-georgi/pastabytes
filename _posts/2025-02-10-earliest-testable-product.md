---
layout: post
title: Earliest testable product
categories: [Encounter]
---

### The "Why"

What is described in the previous installments in this series has been mostly motivated by my own need to "do something" with linked data and to prove to myself that my early ideas could be implemented. I am still not convinced that what I've put my time into is of any use to anyone out there, and the only way to find out would be to share it with potential users. At this stage I have developed some idea around who those are.

### Personas

For one, I am a user myself, embodying the relatively data-savvy technical "persona" who is driven by the potential of doing useful stuff with the data we can collect. We could refer to them as the **data consumer**. There is also a different kind of user on which the amount and quality of data collected depend. I refer to that user's persona as the **citizen ornithologist**. There is a third kind of user, the one for whom I am writing this and making my code and other artifacts available on GitHub, the **community developer**.

When I completed my POC in the scope I had originally planned I realized that I was only addressing the potential needs of the **community developer** -- hopefully making it easy and clear to anyone who might want to experiment with the tools and technologies I had chosen, or even contribute to my project. In terms of the needs of the other two personas, however, the result was rather underwhelming.

### Earliest Testable Product

It has been my goal from the start that I should also learn about what it means to be building a product from the ground up. At this stage it is still hard to see what exactly the product could be but I am driven by an overall vision for it to develop as a hub for crowd-sourced data. Having identified the three main personas, I think I know what I should keep doing to serve the needs of **community developers**. For **data consumers**, and particularly such that are not too familiar with the concept of linked data, I need an easy way to demonstrate the value of such data. And for **citizen ornithologists** I need to make the system at least marginally usable. Both needs could only be served by making publicly available instances of the three services currently making up the solution: the photo sharing app, the photo annotation app and the semantic data repository.

This is how I came up with an additional list of tasks in my backlog beyond the [POC](https://github.com/iliev-georgi/encounter/milestone/1) milestone (marking a fully integrated local deployment). By completing these extra tasks I should be able to deliver something I could put into the hands of some alpha testers representative of the **citizen ornithologist** and **data consumer** personas. This version of my work I refer to as the [Earliest Testable Product](https://github.com/iliev-georgi/encounter/milestone/2), a concept borrowed from [The Lean Forum](https://leanforum.se/artiklar/think-tank/making-sense-of-mvp-minimum-viable-product-and-why-i-prefer-earliest-testableusablelovable/).

#### 1. Public cloud infrastructure

The hosting options available at reasonable cost for such a project were discussed as part of [this task](https://github.com/iliev-georgi/encounter/issues/2). The following services are now publicly available:

- [Pixelfed](https://pixelfed.pastabytes.com), photo sharing app
- [Photo annotation app](https://encounter.pastabytes.com) integrated with the above
- [Virtuoso SPARQL endpoint](https://virtuoso.pastabytes.com/sparql) allowing public read-only access to the linked data managed by the photo annotation app

#### 2. Deployment orchestration

The way the solution is configured and deployed locally is rather high-touch. To shorten the path from development to deployment, first we had to add a Dockerfile packaging the photo annotation app and its dependencies, and update the docker compose script and configurations originally provided with the Pixelfed app. For details see this [PR](https://github.com/iliev-georgi/encounter/pull/13). One could argue against this kind of coupling between the components but on this early stage of development it does the job.

#### 3. Demonstrating the value of linked data

Ahead of onboarding our first users and collecting our first encounter data it would be hard to demonstrate the value of linked data. Yet that is one feature I found critical to be able to explain why we would want to build such a system in the first place. I decided therefore not to go for the necessary improvements to the initial [model](https://github.com/iliev-georgi/encounter/discussions/5) and instead to freeze it for the time being and build a quick and dirty visualization on top of that, also using some fake data and an out-of-the-box interactive map embedded in the Streamlit application. For details see [this](https://github.com/iliev-georgi/encounter/pull/26) and [this](https://github.com/iliev-georgi/encounter/pull/28) PR.

#### 4. Enabling a minimal end-to-end annotation workflow

Compared to the original idea of citizen ornithologists sharing photos via our system and then annotating those with the necessary metadata to populate the Encounter semantic model, the POC system had no way of adding location data to the encounter evidence. To be able to serve this basic need we had to solve a number of UX challenges in terms of selecting the encounter location on the interactive map and also making sure multiple annotations of the same evidence would not result in an explosion of the number of Encounter instances in the graph. For details see [this](https://github.com/iliev-georgi/encounter/pull/31) and [this](https://github.com/iliev-georgi/encounter/pull/32) PR and the resulting bugfixes.

With those enhancements in place we have arrived at the first working implementation of an end-to-end annotation workflow and linked-data visualization. Is it good? I doubt it -- just take a look at the growing number of issues I've identified myself already on the [Kanban board](https://github.com/users/iliev-georgi/projects/1). Does it work? Only a user can tell. Is it testable? I believe it is, so I will be on the lookout for some early alpha users representing the different personas identified above, and collecting some real-world feedback that would then be used to drive the roadmap of features and enhancements ahead.

## Coming up next

- Onboarding alpha users