---
layout: post
title: Choosing POC technology
categories: [Encounter]
---

### Photo sharing

Woke up in the new year with the ambition to start a personal project, as described. I quickly realized that properly done photo sharing is a huge task that I am not really interested in solving given my current tech stack and the time I can afford to spend on the task. This is first and foremost a community effort, and the photo sharing app is the centerpiece in that, even if my end goal is collecting and annotating linked data. As such it should offer sufficiently well-developed UX, doing well just photo sharing. Hence I started looking for suitable open-source projects that could fit my plans. [Pixelfed](https://pixelfed.org/) stood out, in terms of

- **philosophy**: Pixelfed instances can form nodes in a decentralized social network
- **UX**: for better or worse, the UX is highly inspired by popular social media apps so it is not something that new, non-technical users, should find too alien
- **capability**: it offers a rich REST API with standard security.

### Photo annotation

The first idea I'd like to explore on the POC stage is the ability to perform lightweight annotation of user-uploaded photos representing live encounters between the user and the bird. The idea is to link each photo to the bird species as described in an existing database. Back to the idea that the solution we're pushing to our users should not be too clunky, one of the reasons I chose to experiment with Pixelfed was its integration capabilities where data elements can be accessed using access tokens -- here I drew some inspiration from [Roma Komarov](https://blog.kizu.dev/embedding-pixelfed-part-2/)'s blog series on Pixelfed integration. This is how I imagine it to work:

1. User walks in the park, sees an interesting bird, takes a photo and uploads to our photo sharing app where photos can also be shared and discussed with like-minded users
2. User gets back home, opens up the photo annotation app, and is presented with the user's latest bird pictures
3. User searches for the exact bird variety in the photo annotation app, and selects the most appropriate one for each picture, resulting in a new entry in the database depicting the entire encounter
4. As the app grows in popularity, our database becomes a live knowledge graph of manually curated data points describing human-bird interactions made available via a standard endpoint to explore and embed into downstream applications (and, yes, you could also point your newly-built AI agent to that endpoint, this is 2025 after all)

### Semantic repositories

Which brings us to the idea of building a semantic representation of the encounter data. What better way to do that than using [RDF](https://www.w3.org/RDF/). First, because there are tons of good and freely available data in RDF out there, including [The Birds of the World Ontology AVIO](https://seco.cs.aalto.fi/publications/2013/tuominen-et-al-avio.pdf). Second, because there are a number of mature triple-store projects out there that we can immediately include in our architecture. Last but not least some of the triple stores would also expose a standard [SPARQL](https://www.w3.org/TR/sparql11-query/) endpoint to query the data both manually and programmatically. As a former Ontotextian, my first choice here may have been [GraphDB](https://www.ontotext.com/products/graphdb/), which is an excellent product with rich capabilities. Yet I decided to try something new and learn how [Virtuoso Open-Source Edition](https://vos.openlinksw.com/owiki/wiki/VOS) approaches RDF data management, as it powers some of the world's biggest open semantic repositories.

### Application

As a data-focused engineer with virtually non-existent front-end skills I have drawn great benefit from [Streamlit](https://streamlit.io/). It shortens dramatically the path from your data to your potential users and is simply awesome. And we might also be able to integrate seamlessly with Pixelfed in an SSO fashion with the help of [Streamlit OAuth](https://pypi.org/project/streamlit-oauth/). More on that in the next post on this topic.

### Project

I've also started a [GitHub project](https://github.com/users/iliev-georgi/projects/1) to track my progress but I'm still keeping it private, along with the POC code base. I plan to open it up to collaborators first, if and when such should materialize...

## Coming up next

- The quick and dirty: reproducible local setup