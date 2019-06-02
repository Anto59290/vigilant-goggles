---
published: true
layout: post
title: "FOSDEM 2019 — Why you should come next year!"
category: jekyll
---

This weekend was held in Brussels the 2019 edition of FOSDEM.

**FOSDEM is a yearly gathering of people to meet and discuss about free software and open source**. One of the main attractions are the conferences that take place during the two days. FLOSS activism, Python, database, monitoring, architecture and so on, pick your favorite topic. Indeed dozens of conferences are taking place in different rooms at the same time. This event is held at the ULB of Bruxelles and all talks are live-streamed and available on the website.

In addition to this, FOSDEM is probably one of the few places in Europe where you can see people wearing VLC logo shaped hats. This year, Back Market was honored to sponsor the event financially and happy to send 4 engineers to Brussels to attend the conferences.

![The great city of Brussels](https://cdn-images-1.medium.com/max/2000/1*g5lKp_xtAZpu4KP_P9QCzQ.jpeg)*The great city of Brussels*

### Saturday talks — ⛄️

One of the first remarkable talks was the one given by Mitchell Baker (president of the Mozilla Foundation) **about how free and open-source software is evolving and playing a bigger role in our society**. It was also the occasion to hear about one of Mozilla’s research projects called “Ad Analysis for Facebook”. By using this Firefox extension you can get a closer idea of why you are being targeted for a specific ad on Facebook. As most of the things done by Mozilla, the code is open-source (under Mozilla Public License Version 2.0) and available on GitHub:
[**mozilla/ad-analysis-for-facebook**
*Ad Analysis for Facebook. Contribute to mozilla/ad-analysis-for-facebook development by creating an account on GitHub.*github.com](https://github.com/mozilla/ad-analysis-for-facebook/)

Another interesting talk was presented by Maxime Guyot about how to **handle a multi-cloud infrastructure** with CI and Kubernetes. He went through a collection of tools that would help you managing big cloud infrastructures. The demo was quite impressive: with a simple commit on Gitlab the whole CI was triggered and the project was deployed across 18 cloud providers in 2 regions of the world within minutes. The good news is the setup and the source code are available online:
[**multicloud-openstack-k8s**
*Multicloud CI/CD with OpenStack and Kubernetes OpenStack Nordic Days 2018 & OpenStack Summit Berlin [Get…*gitlab.com](https://gitlab.com/multicloud-openstack-k8s)

### Sunday talks — 🐍

After some waffles, beers and mussels Sunday came, and Sunday was the day we were looking forward to the most. Indeed Sunday was the day for the Python conferences. Python is the main technology we use on an everyday basis at Back Market and therefore we are always eager to learn new skills.

We spent many hours in the Python devroom and had the chance to listen to various topics. One of those that caught our attention was the “Making your Python code write your Python code” talk by [Marcin Sobczyk](https://fosdem.org/2019/schedule/speaker/marcin_sobczyk/). We liked that it was a very **didactic approach to abstract syntax trees and the AST** module in Python: in 25 minutes he went though both theory and practice, and the result was an AST transformer able to print how much time it takes to execute every line of your code. Let us also mention a talk by [Alexander Todorov](https://fosdem.org/2019/schedule/speaker/alexander_todorov/) on how to write pylint plugins using the Astroid module, which is built on top of AST. The AST module of Python is generally not so well-known and it looks like these kind of talks will help it become more popular in the community.
[**PyCQA/astroid**
*A common base representation of python source code for pylint and other projects - PyCQA/astroid*github.com](https://github.com/PyCQA/astroid)

On the other hand, there was also many exciting talks in the PostgreSQL devroom and much to hear and learn. The last talk we had before leaving was the “Data modelling, Normalization, and Denormalization” by Dimitri Fontaine. It was one of those talks that doesn’t only make you question if you spent enough time thinking about your model design, but also if just depending on your ORM is enough for your scale. Should we abandon the ORM, and move to just using a bare-metal driver, or work on improving the ORM so it can handle what it currently can’t? This is probably one of the most controversial talks between Python -or more specifically- Django developers. But, in any case, what can’t be denied is the fact that -as Dimitri explained- you can never think the same when you’re writing with ORM the same as when you write SQL.

In a nutshell, this is why **going to a conference like this is really worth the time for our developers**. Watching an online video is good, but being on location, getting the chance to talk and give your own opinion — as well as considering new possibilities and ideas outside the context of solving a problem — is one of the most eye-opening and creative experiences one could have. It’s an opportunity to think and have fun outside of our comfort zones. 😃

### What’s Next ? — 🔥

That’s all for this year’s FOSDEM, the next big events for the Python community will be the DjangoCon ([https://2019.djangocon.eu/](https://2019.djangocon.eu/)) and the EuroPython ([https://ep2019.europython.eu/](https://ep2019.europython.eu/)). For their part our frontend team will be going in a few weeks to Vue.js Amsterdam. If, like us, you enjoy **being part of great community and like attending these kinds of events**, know [that we are currently hiring.](https://jobs.lever.co/backmarket?lever-via=pbP3Q65Krj)

As always the recordings of the presentations will soon be available on the FOSDEM website. Most of the speakers also link resources (repos, slides, etc.) in their abstract so that you can start digging.

We would like to thank all the FOSDEM team and all the volunteers as well as all the speakers and sponsors. 

