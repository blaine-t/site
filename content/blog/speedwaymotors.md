+++
title = "My Speedway Motors Summer Internship Experience"
date = 2024-08-04
updated = 2024-09-07
description = "My experience with my internship at Speedway Motors over Summer 2024"

[taxonomies]
tags = ["internship", "experience", "software"]

[extra]
giscus = true
quick_navigation_buttons = true
toc = true
+++

This Summer I worked with [Speedway Motors](https://www.linkedin.com/company/speedway-motors-inc) to develop and maintain features for our customers and continually delivered these features to ensure a great experience for every user of the [Speedway Motors Website](https://speedwaymotors.com). I worked 40 hours a week in a hybrid environment where I was able to collaborate with teammates through the use of technologies like [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) and [Slack](https://slack.com/). Through this experience I gained a lot of knowledge in both frontend and backend development that will allow me to be a better software developer in future experiences. I will delve more into the details as this blog goes on, talking about how I effectively navigated tech debt, the specific technologies I learned, how I was an effective team member, and finally how I will use all of this in the future.

## Speedway Motors

I think first off I should probably explain what Speedway Motors is. Speedway Motors is a company [established in 1952](https://www.speedwaymotors.com/Info/SpeedwayHistory) [here in Lincoln, NE](https://maps.app.goo.gl/QRiYQezZuUvnPDiw5) with the goal of allowing more people to share the passion that "Speedy" Bill Smith had in the late 1940s with cars. It has since expanded to offer way more than the original catalog and expanded to [other states like Arizona](https://maps.app.goo.gl/xxoWHFhPm164zvEb9). Starting in 1996 Speedway Motors expanded to their first website which is what I work on now! After having a site around for almost 3 decades you can expect there to be a fair amount of tech debt but honestly I was happily surprised!

## Tech Debt

[Tech debt](https://en.wikipedia.org/wiki/Technical_debt) is one of those inevitable things in software development. No matter what you do you will most likely end up with it over time. I joined Speedweay this summer in kind of a middle ground state of moving away from their old technology. Their old technology was in a [Monorepo](https://www.perforce.com/blog/vcs/what-monorepo) that made it difficult to make changes without having [merge conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts) with other developers. Luckily for me I had to do very little in that repository but when I did it was a pain and I could obviously see why they were moving away from it to a [Multi-Repo](https://www.gitkraken.com/blog/monorepo-vs-multi-repo-collaboration) system. So Speedway Motors was already doing a great job of resolving their tech debt which was a massive sigh of relief for a new intern like me but it also meant I had to learn about both which was great for my experience but definitely hampered my ramping up speed to my full performance. Overall, I believe Speedway Motors does a great job of controlling their tech debt and it was a pleasure to work on the code bases.

## Development

At Speedway Motors I worked primarily with the Multi-Repos adding new features to make consumers have easier buying decisions like improving promotion banners and fixing bugs in existing features that interrupted the flow of customers. My main worked laid primarily around the new garage feature of vehicle + engine fitment which allowed our customers to have a more informed idea of what they were ordering will actually fit their specific vehicle. This is such an important feature because in this space [engine swaps](https://en.wikipedia.org/wiki/Engine_swap) are common which means we can't guarantee a part will fit because the car may have a different engine or for engine parts the engine might be in a new vehicle which changes the clearances. In order to make all of these improvements I had to work on the React.js frontend, the C# .NET backend and the MySQL database.

### React

I honestly didn't spend that much time on the React side of things at my internship but it was crucial for implementing the promotion banners and fixing bugs on our [search page](https://www.speedwaymotors.com/Search?query=shocks) that were affecting real world customers. I learned through [this tutorial on Scrimba](https://v2.scrimba.com/learn-react-c0e), which I feel is a great way to learn the framework. I also had the pleasure of working with Speedway Motors's in-house React design library which trivialized adding new components to the site. Overall, I think I got a good experience for what React is by reading over existing code and making my own changes even if I didn't make that many.

### .NET

I spent most of my internship in the many different repositories on Speedway Motors's backend. This is where your search and recommendations and anything else [dynamic](https://blog.hubspot.com/website/static-vs-dynamic-website) goes through. I mainly dealt with ensuring that our fitment rules were applied across the site and also helped with the tooling that allowed other departments inside of Speedway Motors to do their job and upload that data easier. When I was developing my improved promotion banners I had to work through many of these repos and had to deal with dependency trees where one service had to come out before the other otherwise I would break that dependent service. This taught me a lot about how to do [proper rollouts of software](https://en.wikipedia.org/wiki/2024_CrowdStrike_incident) and how to ensure that there is no interruption for the end user. I created new repos to add additional functionality to our internal reporting to make sure that.

### SQL

I dabbled a bit in the databases when I was creating my additional repos to grab the data I needed using the [.NET Entity Framework](https://learn.microsoft.com/en-us/ef/). I learned a lot about the benefits and also the limitations of using an [ORM](https://www.prisma.io/dataguide/types/relational/what-is-an-orm) like Entity. One of the major advantages of using an ORM is not having to write out each and every SQL statement. Instead you can write in code making it easier to actually get the data you want and not be bogged down in writing `SELECT * FROM table` for the tenth time. One of the downsides of an ORM like this though is the lack of adjustability. There were multiple times where there was something that I wanted to do that I knew I could do in a SQL query but I couldn't quite figure out how to do it with Entity. This is where I had to work with my coworkers and my mentor to figure out the best way to approach the problem.

## Teamwork

One of the best things about Speedway Motors is the team. The whole tech team is ~30 people but the specific team I was on had ~8 people which made the culture such an amazing fit for me. We would all work from home but that didn't limit our ability to communicate and pair program. There was many times I would work with my mentor to fix a problem especially in the early days of my internship by screen sharing and pair programming. Sure it doesn't beat the real thing but being able to have my massive triple monitor setup without concern about if I will be able to have that same setup in the office definitely outweighed that.
{{ dimmable_image(src="img/deskRender.png", alt="A Fusion 360 view of my desk setup") }}
I also had my amazing manager which made sure that I always had the tools and information to do my job correctly the first time so I didn't have to worry about refactoring code and wasting mine and the company's time. I also had great experiences with the other developers on the team who helped me in fields they specialized in like [Split](https://www.split.io/) and [Miso](https://miso.ai/).

## My Future

I couldn't have asked for a better first internship from Speedway Motors. Everyone along the line from the HR that screened me and set me up with payroll to the IT team that helped setup all the different accounts to the technology team that made me feel welcomed and let me contribute to useful features on the live site were wonderful. They allowed me to get up and running as fast as possible so I could start making customer facing changes that improved the lives of our users and along the way I was able to learn so many useful technologies that I will be able to use in future experiences. I will be able to use my new knowledge at the next [hackathon](https://hackmidwest.com/) I am going to (expect a blog post after) and future internships I plan on doing. Overall, I am immensely grateful for what Speedway Motors has done for me and I am happy to announce that I am staying on for the fall! I hope to continue to deliver value continuously and expand my knowledge of technology!
