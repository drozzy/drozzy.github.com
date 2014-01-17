---
layout: post
title: Composing WCF and ASP.NET MVC4 Applications
---

You decided to use Dependency Injection in your application. Unfortunately, your application is not a simple console app that has a main method. It is a complex mess of stuff, including things like WCF and ASP.NET MVC (version 4 in our case). How and where do you compose your application?

Composition Root
==================
The first thing you need to do is have a composition root. This is a place where all your dependencies will be specified. Here, you specify that "this implementation" provides "this interface". You should have one composition root per application. If your code consists of multiple applications, like WCF services or ASP.NET MVC web applications---then you need to have multiple composition roots. Of course, you could create some shared code and reuse it in each, but ultimately each application will need to compose itself.


To be continued... (pending examples, di framework recommendation, book recommendation)

References
============
1. Dependency Injection in .NET, Seemann, M., 2011, Manning Publications Company.
