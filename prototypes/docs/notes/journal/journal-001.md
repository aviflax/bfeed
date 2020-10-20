# Journal 001: How might this thing work?

At a high level, I feel like there are two containers:

1. Editor: The dynamic Web app for writing and managing posts
2. Publisher: The static site generator (SSG) that’s invoked to build each feed site, and the mechanism that invokes it, orchestrates the output, etc

But are they really discrete? I mean, doesn’t the dynamic Web app need to invoke the SSG?

Not necessarily… they could be discrete, and loosely coupled. Maybe the Web app just writes to the files. And then some kind of event is generated... maybe it's implicit, like an S3 file modification event. Or maybe it's explicit, with the app emitting an event that's then picked up by the publisher.

Also, what about a server?

Well, if we use Netlify, then maybe it’s both the publisher and the server.
