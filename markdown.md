class: center, middle
<!-- background-image: url(images/patrick-tomasso-151382-unsplash.jpg) -->
background-image: url(images/dardan-mu-268794-unsplash.jpg)

# The Continuous Journey from a software developer’s perspective

## Adam Beres-Deak (AutoScout24)

<!-- .photo-credit[ [Photo by Patrick Tomasso](https://unsplash.com/photos/5hvn-2WW6rY) ] -->
.photo-credit[ [photo: Dardan Mu](https://unsplash.com/photos/Jz4tCJMKFLg) ]

---

class: middle

<img src="images/autoscout24.svg" width="400" alt="Logo of AutoScout24" style="display: block; margin: 40px auto;">

10 million users per month and more than 2.4 million vehicle offers – AutoScout24 is the largest online car marketplace in Europe. With a market presence in 18 countries and more than 55,000 associated dealers, AutoScout24 is represented in all important European markets.

----

<small>
[autoscout24.com](https://www.autoscout24.com) &middot;
[autoscout24.de](https://www.autoscout24.de) &middot;
[autoscout24.at](https://www.autoscout24.at) &middot;
[autoscout24.it](https://www.autoscout24.it) &middot;
[autoscout24.be](https://www.autoscout24.be) &middot;
[autoscout24.fr](https://www.autoscout24.fr) &middot;
[autoscout24.lu](https://www.autoscout24.lu) &middot;
[autoscout24.nl](https://www.autoscout24.nl)  
[autoscout24.es](https://www.autoscout24.es) &middot;
[autoscout24.hu](https://www.autoscout24.hu) &middot;
[autoscout24.pl](https://www.autoscout24.pl) &middot;
[autoscout24.bg](https://www.autoscout24.bg) &middot;
[autoscout24.cz](https://www.autoscout24.cz) &middot;
[autoscout24.ro](https://www.autoscout24.ro) &middot;
[autoscout24.hr](https://www.autoscout24.hr) &middot;
[autoscout24.ru](https://www.autoscout24.ru)  
[autoscout24.se](https://www.autoscout24.se) &middot;
[autoscout24.com.tr](https://www.autoscout24.com.tr) &middot;
[autoscout24.com.ua](https://www.autoscout24.com.ua)
</small>

---

[www.autoscout24.de - traffic estimate by SimilarWeb - Feb 2018](https://www.similarweb.com/website/autoscout24.de)

.center[![Estimated Traffic of autoscout24.de](images/as24-traffic-estimate.png)]

---

class: center, middle, white-headline
background-image: url(images/brina-blum-112501-unsplash.jpg)
.photo-credit[ [photo: Brina Blum](https://unsplash.com/photos/_fBturNUtd8) ]

# Where are we coming from?

---

# Where are we coming from?

Ca. 6 years ago we had
- ... a few monolithic ASP.Net/C# projects
- ... ca. 10 engineering and operations teams
- ... ca. 2000 servers in own datacenter
- ... continuous integration pipelines (TeamCity, ~4 stages)
- ... automated unit tests and browser tests
- ... a lot of manual testing
- ... from commit to release in under an hour (sometimes)
- ... some projects were released (almost) daily

???
- releases were announced via email
- somebody from ops monitoring releases
- teams blocked by other teams
- getting new servers was painful and slow process
- throw software over the fence to the ops team
- communication between ops and devs was slow and rare

---

background-image: url(images/samuele-errico-piccarini-197299-unsplash.jpg)
.photo-credit[ [photo: Samuele Errico Piccarini](https://unsplash.com/photos/MyjVReZ5GLQ) ]

???
fast-forward to now

---

class: center, white-headline
background-image: url(images/allen-cai-106401-unsplash.jpg)
.photo-credit[ [photo: Allen Cai](https://unsplash.com/photos/Y4RxCIaYaSk) ]

# Where are we now?

---

# Where are we now?

- ... ca. 30 independent teams
- ... uncountable micro services and projects
- ... polyglot architecture (Node.js, Scala, JVM, static pages)
- ... teams are responsible for their infrastructure + code + features
- ... teams release independently of other teams
- ... in the cloud

???

- most teams do Continuous Deployment
- releases are quick and "no big deals"
- my team has ca. 10 services - all of them release under 10 minutes

---

# You built it - you run it!

- The team is responsible for implementation and operation of the service
- No more throwing over the fence

???

- there are services shifted from team to team but with the whole responsibility

---

class: center, white-headline, white-text
background-image: url(images/andrik-langfield-petrides-512923-unsplash.jpg)
.photo-credit[ [photo: ANDRIK LANGFIELD PETRIDES](https://unsplash.com/photos/TyIx-Hyyki0) ]

# Embrace the Cloud

- Wide range of services - database, computing, networking, streaming, etc.
- Scales well for low and high demand

???
- you can use just a little bit or everything
- multicloud possible
- we are on Amazon Web Services
-  EC2, Lambda, ECS, ELB, ALB
- sometimes things just fail => retry, cache, leave it out

---

# Managed services

- Our principle: prefer manged services over self-hosted
- Teams are more independent
- Teams can choose technology more freely
- E.g. no integration on the database level
- No need to take care of the hardware

???

- no-one maintains DynamoDB
- no physical hardware
- no VMWare or other virtualization => we know what we get from an EC2 server
- No common dependency on the database

---

class: center, middle, white-headline
background-image: url(images/chris-liverani-552652-unsplash.jpg)
.photo-credit[ [photo: Chris Liverani](https://unsplash.com/photos/dBI_My696Rk) ]

# Data-driven

???

- tracking
- data analytics

---

# Cost awareness

- Cost is not hidden anymore
- Cost can be estimated in advance
- Cost is monitored on a service level

???

---

class: center, middle
.photo-credit[ [photo: Wikipedia](https://en.wikipedia.org/wiki/Mean_time_between_failures) ]

# MTBF vs MTTR

Mean Time Between Failures vs. Mean Time To Recovery

![MTBF](images/time_between_failures.svg)

---

# Infrastructure as Code

---

# Feature toggles

- Every commit can go into production
- No feature branches
- We ship inactive code
- Can be enabled on a request/user/language basis

```js
if (toggle('shiny-new-feature').isOn) {
    // make the World a better place
} else {
    // let the World stay as it was before
}
```

---

# Ops toggles

e.g. ads can be switched off if they are causing problems

```js
if (opsToggle('ads').isOn) {
    showAds();
}
```

---

class: middle, center

# A/B Testing

---

class: center, middle, white-headline, white-text
background-image: url(images/chuttersnap-255215-unsplash.jpg)
.photo-credit[ [photo: chuttersnap](https://unsplash.com/photos/fN603qcEA7g) ]

# Continuous Integration and Deployment

---

class: center, middle

# Continuous Integration and Deployment

- Infrastructure as code
- Master branch based development
- Feature toggling
- Most teams not just do CI but also CD
- Contributions from external teams through Pull Requests

???
- no server re-use / servers are recreated on all deployments
- every commit goes live unless they fail the tests

---

.center[![Agile without empowerment is just waterfall with more meetings...](images/tweet-agile-without-empowerment.png)]

---

class: center, middle, white-headline
background-image: url(images/american-public-power-association-430863-unsplash.jpg)
.photo-credit[ [photo: American Public Power Association](https://unsplash.com/photos/AA5v6sMcalY) ]

# Power to the Teams
<!-- # Empowerment -->

---

class: center, middle, white-headline
background-image: url(images/jair-lazaro-480021-unsplash.jpg)
.photo-credit[ [photo: Jair Lázaro](https://unsplash.com/photos/0lrJo37r6Nk) ]

# Monitoring

---

- CloudWatch and DataDog for monitoring and dashboards
- OpsGenie for alarming
- Every team has on-call duty for their services

???
- false alarms are rare -> nobody likes to be woken up in the night
- it costs money but we consider it like an insurance
- on-call is supposed to be temporary => recovery should be automated in future

---

background-image: url(images/datadog-2.png)

---

class: center, middle, white-headline
background-image: url(images/denys-argyriou-453348-unsplash.jpg)
.photo-credit[ [photo: Denys Argyriou](https://unsplash.com/photos/VU03qDREAgU) ]

# Incident handling

- fix the error vs. bring back the system to a healthy state
- on-call duty and free hunting

???

---

# Unexpected Production Change

- AWS CloudTrail
- Monitoring that no manual changes are done to our production environment

---

class: center, middle
background-image: url(images/pete-bellis-395558-unsplash.jpg)
.photo-credit[ [photo: Pete Bellis](https://unsplash.com/photos/FIMTCLmEhFE) ]

# Take aways

---

# Take aways

- Embrace the cloud
- Power to the teams
- Make deployments a "no-brainer"
- Have good monitoring and alarming
