---
layout: post
title: Book review "Migrating Legacy Systems"
subtitle: Michael L. Brodie, Michael Stonebraker, 1995
bigimg: /img/michal-parzuchowski-224092-unsplash.png
tags: [book, migration, gateway]
---

You might ask yourself what a 30 year old book on information systems has to offer. I first read the book during literature research for my masters thesis in 2001. At the time I already had a few years of experience delivering custom made IT systems to enterprise customers. From that I had first hand experience what it meant to gather a bunch of programmers to work on a one-off solution before everybody moved on to the next gig. The traditional approach to "Migrating Legacy Systems" is a Big-Bang migration which is unfeasible and failure is inevitable. An incremental approach using Baby-Steps is the only way. I am sure this book is one of a few that had a profound and lasting influence on my own work. 

Many big (international) organizations are captured by technical debt. Often they look back on more than 50 years of centralized mainframe based development. 80-90 % of the IT budgets are eaten up to keep the system running. Cost and technical challenges limit the scope of action.

Migrating a legacy system is one of the riskiest IT project endeavors one can partake. So the key aspect in such an endeavor is project steering and management. It is most important is to address the risk by applying an incremental approach which is clearly defined and communicated. And this exactly is what the book delivers.

The goal of a legacy system migration in many cases is to break down a monolithic application which is costly to operate and resistant to changes into maintainable independent components that allows to add new features efficiently. The IT system is operational and fully functional during the whole migration process (no parallel operation of two systems, no switch over on launch-date!).

Brodie and Stonebraker propose an evolutionary, incremental approach which they call Chicken-Little. Each increment consists of up to eleven steps some of which can be carried out in parallel.

The Chicken-Little Steps:

1. Incrementally Analyze the Legacy IS
2. Incrementally Decompose the legacy IS Structure
3. Incrementally Design the Target Interfaces
4. Incrementally Design the Target Applications
5. Incrementally Design the Target Database
6. Incrementally Install the Target Environment
7. Incrementally Create and Install the Necessary Gateways
8. Incrementally Migrate the Legacy Database
9. Incrementally Migrate the Legacy Applications
10. Incrementally Migrate the Legacy Interfaces
11. Incrementally Cut Over to the Target IS

The two case studies (chapters 3 and 4) show the size and effort required in a real legacy system migration.

Given Dr. Stonebraker authored the book it comes as no surprise that the book dedicates a lot of attention on the discussion of different data- and database-migration strategies.

The book has a dedicated chapter on technical options available at the time for implementing client-server architectures like CORBA and DCOM, distributed databases and transaction monitors. Todays cloud age offers additional options like NoSQL database technologies, API specifications, gateways, etc.

Brodie and Stonebraker's book is honest and upfront about the difficulties involved in migrating large legacy systems, the Chicken-Little approach is quite common sensical and easy to read. In my opinion core parts and case studies of the book are still worth reading. You will get a good introduction to the topic if you are not getting distracted by references to old software environments and tools.
