---
layout: post
title:  "2021: Setting the Scene"
author: "tokcum"
location: "Augsburg"
time-required: "10 min"
date: 2021-01-01 22:00:00 +0200
categories: project
tags: setup
---

The second half of 2020 was quite busy, and I did not find time to write a mature article to post here. 
Nevertheless, I was able to do some related research and develop the ideas and concepts behind this 
project. Driven by use cases I faced at work, my thoughts were revolving around an application 
enabling its users to manage arbitrary objects. In the past I implemented such requirements with 
products from Atlassian and enhanced the solution with Insight, which allowed me to model the 
problem domain freely. Additionally, I enjoyed the minimal costs involved at least as long as 
the customers' environment stayed small and I was able to stick to the starter license. 
Despite the effort I put from time to time into finding a comparable alternative, 
a competitive solution didn't cross my track.

And then in Oct 2020 Atlassian announced to stop selling its server products effective in Feb 2021. This 
move put an end to the approach I took so far and contributed to my motivation to implement an own 
solution, going hand in hand with my objective to become a software developer.

Having said that, it is clear that this project is about a full stack application. On the one hand, 
the application should be self-contained enabling it to just run out of the box with virtually 
no additional requirements to its environment. On the other hand it is decisive to keep a certain 
flexibility and scalability in mind. I'm not talking about a globally used application with 
millions of users here but about small and mid size organizations which might have a clear agenda 
e.g. regarding user authentication or the database. The capability to integrate 
an application with an existing identity management or a common, centrally managed database 
could prove to be an enabler for scalability.

# Building Blocks

When implementing a full stack application, we need to think about the following building blocks in the 
first place. Later, additional components such as search and cache will increase in importance which 
reminds us to keep the architecture open for future changes.

1. Front End
2. Application Server 
3. Database

# Technology

Today there is a nearly endless amount of technologies available to build an application, 
and they are evolving at a pace that just following is hard let alone choosing and sticking to one 
in the long run.
Considering that we could even leverage a different technology at each layer of the application stack 
there are myriads of options at our hands.

To cut short: I've chosen Rust for the complete stack. It might sound like a strongly opinionated choice,
but there are good reasons for this commitment. In 2020, I wrote a report about Rust's relevance 
in secure software development for my employer. Unfortunately I'm not able to disclose the full report 
here. However, my personal conclusion is that Rust is the way to go. My first experiments with

(1) [Seed][seed-rs.org_seed-project-site] in the front end,

(2) [Actix][actix.rs_actix-project-site] as the runtime of the application server and 

(3) [Sqlx][github.com_sqlx-repo] to interface with the database 

were very promising, and despite the steep learning curve a lot of fun. Just as a 
reminder: this is still a project with a strong focus on learning.

# Business Model

Although I'm not sure about the licensing yet, this is definitely going to be an Open Source project.
To a significant extent what I am today I owe to the existence of Open Source. If I am ever able to 
earn money from this, I would like to gain it by transforming technology into tangible business value and 
not by licensing revenues.

# Further reading

#### in English

[ZDNet: Atlassian to end sale and support of on-premise server products by 2024, last accessed on 2021-01-16][zdnet.com_atlassian-to-end-sale-and-support-of-on-premise-server]

 
# References 

[Actix Project, last accessed on 2021-01-16][actix.rs_actix-project-site]

[Seed Project, last accessed on 2021-01-16][seed-rs.org_seed-project-site]

[Sqlx Repo, last accessed on 2021-01-16][github.com_sqlx-repo]


[//]: # (Links)
[actix.rs_actix-project-site]: https://actix.rs/
[seed-rs.org_seed-project-site]: https://seed-rs.org/
[github.com_sqlx-repo]: https://github.com/launchbadge/sqlx
[zdnet.com_atlassian-to-end-sale-and-support-of-on-premise-server]: https://www.zdnet.com/article/atlassian-to-end-sale-and-support-of-on-premise-server-products-by-2024/
