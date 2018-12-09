---
layout: post
title: Query AWS Athena
subtitle: from Jupyter Notebooks
bigimg: /img/jamie-street-382722-unsplash.png
tags: [visualization, iot, amazon aws, python, metrics]
---

Jupyter is a powerful tool that should be part of almost anyone's toolbox. At first it might seem like Jupyter is a tool that is focused on Data Science and Machine Learning, but actual it is way more than that. Jupyter can be a teaching tool, a presentation tool, a documentation tool, a collaborative tool, and much more. With tools like Jupyter Lab that are easily extensible, there is almost nothing that you couldn't do directly in it. One example I am particularily fond of is given by this great talk on [flipped learning experiences with Jupyter](https://www.youtube.com/watch?v=UpWEUXiPG4k) at the Jupyter Notebook conference that took place in New York a few weeks ago.

There are many different ways to host your Jupyter notebooks. I like to run them on my laptop but you can easily host them yourself. But why bother? Just use [Google Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb)!

I am working on an [IoT solution based on ESP-32](https://www.mark-fink.de/2018-11-03-esp32-aws-iot-mqtt/) that collects sensor measurements and stores the data on Amazon S3. Today I show you how I use Jupyter to analyse that data.

First of all I need to run a SQL query against AWS Athena to get the data I want:

![Screenshot make menuconfig](/media/jupyter_athena/athena_sql_query.png)

In case you get an error during notebook execution like "An error occurred (ExpiredToken) when calling the GetCallerIdentity operation: The security token included in the request is expired", one way to fix that is to renew the token usings AWS-MFA:

{% highlight bash %}
$ aws-mfa --duration 1800
{% endhighlight %}

When I started out it was not at all obvious to me how to structure the data, partion the table etc. [I asked for help on SO](https://stackoverflow.com/questions/53570456/aws-athena-create-table-and-partition).

Now I visualize that data (you see the temperature fluctuations duing the day):

![Screenshot make menuconfig](/media/jupyter_athena/jupyter_one_week_of_data.png)

The orange temperature curve is inside the chicken stable, blue curve plots outside temperature (in celsius).

I like to check if the stable protects my chickens enough during the night. We drill into the plot we can see that the temperature is at least 2 degrees higher during the night. Chickens are pretty hardy birds at least old breeds like mine but they do not like draft.

![Screenshot make menuconfig](/media/jupyter_athena/jupyter_zoom_in.png)

I hope this demonstrates some of the possibilities Jupyter brings to you. You could literally run your entire business through Jupyter and I think you should!

Why am I doing this? I want to keep my chickens happy during winter...

![Happy chickens](/media/jupyter_athena/happy_chickens.png =300x)


I hope this post is helpful to you.

All the best, Mark


## Resources

* [Jupyter Notebook](https://github.com/jupyter/notebook)
* [Athena Extension for Jupyter Notebooks](https://github.com/finklabs/jupyter-athena-sql)
* [Google Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb)
* [Athena demo notebook used in this post](https://github.com/finklabs/jupyter-athena-sql/blob/develop/athena_interactive_visualization.ipynb)
* [AWS-MFA](https://pypi.org/project/aws-mfa/)
