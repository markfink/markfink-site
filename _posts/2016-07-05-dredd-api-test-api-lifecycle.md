---
layout: post
title: DREDD API Tester works with API Blueprints
subtitle: 
bigimg: /img/frank-vex-1123999-unsplash.png
tags: [software engineering, test automation, microservice]
---

For many years SOAP was the predominant technology in the enterprise world used for exposing data and application functionality as webservices. Even when better (and simpler) technologies like REST became available during the last 10 years, their adoption was slow. In my opinion the lack of proper API tooling was the main reason for that. Nowadays the situation has changed since adequate tools and workflows are ready available. I want to share with you some of the great things I recently learned.


## API Blueprints

Besides the many technical challenges you face in enterprise software, managing your APIs is one of the most important tasks, especially if you want to maintain a stack of dozens of even hundreds of services. One way of looking at the API documentation of your service is to basically treat it like a signed contract between your service and its clients.

Today there are different tooling options available to document your REST service API like swagger, RAML, and API Blueprint. I am not promoting any of them. I just want to share some ideas and show how you can improve the quality of your services by using these tools.

In case you want to learn more about the available tool options, you might want to start by viewing the following video. Laura Heritage (SOA software) goes in great length into some of the pros and cons of the different tooling options:

[![Laura Heritage, API Description Language](https://img.youtube.com/vi/vu8_QLkW1mg/0.jpg)](https://www.youtube.com/watch?v=vu8_QLkW1mg)


I have the supercars toy sample that I use to explore and demonstrate various tools. I used API Blueprint to document its service API. Please take a look if you like to see how the HTML documentation for the supercars API looks like: [Documentation for supercars API](http://docs.supercarsapi.apiary.io/#reference/0/supercars-collection/list-all-supercars)


## DREDD API Tester

apiary.io the company behind API Blueprint open sourced many of the tools that you need to facilitate the API workflow for your services. With the DREDD API tester they push this even further.

![REDD API test tool](/media/dredd/dredd.png){: width=400}

In a nutshell, DREDD API Tester does following:

* Takes your API Blueprint document
* Creates expectations based on sample requests and responses documented in the API documentation
* Send requests to your service API and checks whether your service responses match the documented sample data
* Reports the results in Junit and other formats

The following diagram shows how you can use DREDD as a center piece in testing you service APIs:

![DREDD API test lifecycle](/media/dredd/dredd-api-test-api-lifecycle.png){: width=450}

DREDD really enables you to take up test driven development (TDD) for your service.

You need a dredd.yml configuration file:

{% highlight yaml %}
dry-run: null
hookfiles: 'dreddhooks.js'
language: nodejs
sandbox: false
server: python supercars/restserver.py
server-wait: 3
init: false
custom: {}
names: false
only: []
reporter: [junit]
output: []
header: []
sorted: false
user: null
inline-errors: false
details: false
method: []
color: true
level: info
timestamp: false
silent: false
path: []
hooks-worker-timeout: 5000
hooks-worker-connect-timeout: 1500
hooks-worker-connect-retry: 500
hooks-worker-after-connect-wait: 100
hooks-worker-term-timeout: 5000
hooks-worker-term-retry: 500
hooks-worker-handler-host: localhost
hooks-worker-handler-port: 61321
blueprint: supercarsapi.apib
endpoint: 'http://localhost:8080'
{% endhighlight %}

## Design-First API lifecycle

The approach to REST webservices I describe here is called Design-First API lifecycle. In the video below Honza Javorek (apiary.io) goes into more details what that means. He also gives an overview on how to use API Blueprint and apiary.io tools: 

[![Honza Javorek, Design-First API lifecycle](https://img.youtube.com/vi/sdlQvTWVQ_M/0.jpg)](https://www.youtube.com/watch?v=sdlQvTWVQ_M)


## Many tools

The tool ecosystem around API Blueprint is already amazing (just a few highlights):

* [Iglo - Generate static HTML documentation from API Blueprint](https://github.com/subosito/iglo)
* [Blueman - Convert an API Blueprint into a Postman collection](http://git.io/blueman)
* [Sublime text plugin](https://github.com/apiaryio/api-blueprint-sublime-plugin)
* [generate json_schema - I have not tried it (yet)](https://github.com/pushred/gulp-mson-to-json-schema)

On top of all that additional (pay per use) services are available from apiary.io. They build their tooling in a way so it integrates perfectly into a Github workflow. I really like that.

I hope this information is helpful to you.

All the best,
Mark


## Resources

* [SOAP](http://en.wikipedia.org/wiki/SOAP)
* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [API Blueprint tutorial](https://apiblueprint.org/documentation/advanced-tutorial.html)
* [Apiary](https://apiary.io/)
* [SWAGGER](http://swagger.io/)
* [RAML](http://raml.org/)
* [Supercars example](https://github.com/finklabs/supercars-service)
* [DREDD](https://dredd.readthedocs.io/en/latest/)
