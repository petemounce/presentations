# Windows at scale

^^
<!-- .slide: class="shell" -->
`$ whoami`

[@petemounce](https://twitter.com/petemounce)

`$ echo $JOB`

[`@justeat_tech 2010-2016`](https://twitter.com/justeat_tech)

`$ export JOB="`[`@improbableio 2016-now"`](https://twitter.com/Improbableio)

Notes:
I found that from 2012 I started using the command line a lot more because pointing and clicking on things had become old.
In 2014 I started using a real shell.


^^
## Questions

Ask them when you have them.

Notes:
Please ask anything as we go.

Content will be mostly at a high level, but happy to get into detail.


^^
## State of the world

It's possible to do DevOps with a Windows platform at scale in the cloud.

Notes:
This is a set of things we did at JUST EAT. They mostly worked well after some bleeding - pretty standard software experience really.


^^
## JUST EAT

Order your takeaway food online.

Notes:
* ran several hundred AWS instances in one country of 14 or so.
* 70searches/sec at mouth of funnel
* 1.2k orders per minute at peak time. Fake load another 600/min.
* Scheduled scaling - crude. 
* Losing an instance was not an interesting event (except when maybe I did it too much on stage).


^^
## How out of date am I?

Notes:
* .NET Core v1 shipped.
  * Modern command-line-first toolchain
  * Dependency management that works (better)
* Windows 2016 came out Oct/2016.
  * Nanoserver
  * [native ssh](https://github.com/PowerShell/Win32-OpenSSH)
  * Dockerize Windows applications


^^
## "Servers == cattle" is possible

Notes:
* Deployment automation should be "table stakes"
* Golden images are a solved problem; build scripts for servers
* It should not be an event when a server dies


^^
## Deployment - one box

There are only so many ways to deploy a Windows website or service.

At JUST EAT, we tried all of them. <!-- .element: class="fragment" -->

Notes:
* 2010: Created contract for a package produced by build automation. Remains today, largely unchanged.
* 2011: Remote execution of ruby+rake with ssh in QA environments, still manual to production
* 2012: Bespoke windows service triggered by bespoke deployment API via winrm
* 2013: AWS + S3 + Seppuku
* 2015: Start to consolidate per-app deployment automation to a single dependency
* 2016: 3rd iteration of deployment service can ... deploy


^^
## Deployment - clusters

Notes:
At JE, we tried to apply SOLID principles at the environment level as well as within codebases.
Each feature of the platform was essentially
* a DNS name
* a load balancer
* a cluster of servers
* a codebase running there


^^
## Deployment - pipeline stage

Elapsed time from "deploy" clicked to live in production?

Notes:
* 2013-2016 - deployment cycle time 20min (scale up new, wait, scale down old)
* 2016+ - deployment cycle time ~2min (update-in-place)

But, don't forget the bit of the pipeline before production.


^^
## Deployment - environments

Notes:
Infrastructure automation is necessary if you want to not lose time debugging environments and third party software

At JE, we spun up QA environments each morning and tore them down every evening. Blessing, because it proved we could do it. Curse, because we didn't have good enough test coverage to avoid breaking the world if a mistake was merged. Just like any other software.


^^
## Application coupling

Notes:
http applications declare and embed their contracts via Swagger.

Increasingly, applications would follow the unified log pattern for integration.
React to input by publishing events.
Other applications, independently, subscribe to those events and do interesting things.
Leads to strong input/output contracts for applications, which leads to looser coupled applications that are much easier to operate and test.


^^
## Monitoring and alerting doesn't have a safe easy option so far

Notes:
At JE, statsd + graphite + seyren

Good
* no operations involvement to start tracking a metric
* very simple to instrument apps
* scalable

Bad
* no consistency in metric naming between apps / teams, so impossible to generate common alerts / dashboards or move between teams easily
* not trivial to scale past single server (_certainly_ not impossible)
* lack of guidance to teams regarding alerting best practises


^^
## Log aggregation is now a much more solved problem

```
nxlog -> logstash -> elasticsearch -> kibana

elastalert
```

Notes:
elastalert gives you the ability to take automatic action based on log events. This gives very flexible operational response until one can trap the problem via code "properly", if at all.

Level up with structured logs.


^^
## Cluster scheduling == still witchcraft

Notes:
This is not something I have direct experience with.
Essentially - get better utilisation from your servers by running several applications on each, and dynamically balancing which jobs run on which hosts according to load.
However - maintain isolation between jobs by running them within containers.

nomad, kubernetes, fleet


^^
## Serverless is promising

aka, "dodging the issue of caring about the OS of your platform."

Notes:
Shipped a thing with Lambda inside 3 months (operating in production, continuously delivered).
One part 80x cheaper than with servers.


^^
## Hiring is still hard

Notes:
* Windows developers with operating-in-production experience are rare
* Make onboarding simpler by making practises conventional across apps and teams
* Be up-front about on-call
* Train deliberately, during peace time, not on the job during incidents


^^
## Windows platforms

Much easier than they used to be.

Notes:


^^
## Thanks for listening!

@petemounce on [twitter](https://twitter.com/petemounce) / [github](https://github.com/petemounce)

[Slides on github](https://github.com/petemounce/presentations)

Notes:
