# How do you KNOW your code is working in production RIGHT NOW?

You write your tests and you ship your code, but many teams stop there - "our tests are green, it's in production, let's get onto the next ticket!".

But then alarms go off. "But our tests were green! It can't be OUR code... Can it?"

Sure it can. Production is a sensitive complicated place. There are loads of variables. Load balancing, numerous servers, different servers, network outages, transient slow downs for no apparent reason, databases with more than a hundred things in them, data that shouldn't be possible, third party dependencies (you know, those things you mocked out)... Oh, and customers - they do really strange things too.

When it goes wrong, it costs money per minute. It's a high-stress, high-pressure environment, and continuous delivery can make it worse.

I'm going to talk about some of the things you can do to tame the chaos that continuous delivery can enable

* alerts demystified - they're just test automation that runs all the time in production
* make your applications tell you whether they’re working or not
* enhance your pipeline as a consequence - you will end up with tests that can run continuously  in production as well as on the way there​
