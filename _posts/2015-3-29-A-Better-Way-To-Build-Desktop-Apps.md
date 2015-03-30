---
layout: post
title: A Better Way to Build Desktop Apps
---

This is a work in progress post...so nothing may be in order or make sense yet if you happen to stumble upon this.  It's 
also completly possible that'll I'll never finish this.



##The Vision

Writing quality cross platform desktop apps is somewhat tough.  I want that to be easier.  The development expierience 
just isn't very good when trying to work with different types of graphic libraries.  I know there are cross platform GUI frameworks
like Qt or GTK+, but those have their own problems, as well as a learning curve.

Atom the text editor recently came out and I was pretty impressed with it (along with brackets, and also splat).  These apps all 
utilize a webview to display the UI.  Atom and Brackets both have their 'Shell' available for viewing/copying on github.com as well.

The Atom shell is especially cool as you can pretty much build your whole app with javascript and node, which is awesome, but not 
quite what I'm looking for.

Ideally, I want this.

 1.  Speed.  Loads fast, and app is responsive.
    
    Most technologies will be fast enough, so this I'm hoping will be sortof a non-issue.  In my mind, hosting something like
    a chrome shell shouldn't be too tough, and once that happens we just let chromium do it's work and since our bigger assets 
    will be local, the app should be snappy.
  
 2.  Works on Windows/Linux/OSX
 
  This is a little bit tougher, but since it's a goal from the beginning I think we can avoid a lot of trouble.  If I only wanted 
  to support Windows I could just use WPF and make a beautiful UI in no time, all in C#!  But unfortunatly WPF is not cross platform.
  Also whatever I do in C# will have to be supported by mono, because as of the time of writing, it's pretty much the only way to run C# 
  on Linux.
  
 3.  UI can be made with Html/Sass
  
  So we need a webview control of some kind.
  
 4.  I can use the Chrome Dev Tools to debug and build this application (but can also turn them off for production)
 
 This shortens our list of possible webview controls by a significant amount.
 
 4.  The UI Web frontend supports all the newest latest and greatest html5 stuff.
 
 Same as above, we need a way to get a damn good web view hosted in our app.
 
 5.  I want to be able to make javascript calls back to the app, and have the application backend responses and logic 
 coded in C#.
 
 !!!  Well, this got a lot trickier.


##How I'm planning to accomplish this

  * A C++ shell with Chromium 39 or later embedded (CEF).
  
  More on why I'm choosing C/C++ a bit later, but to embed chromium I think CEF is the clear choice, it's relatively easy
  to get up a basic shell (I did it one night of tinkering).  Also since we're using C/C++ we basically have access to everything.
  This is both a good and a bad thing.
  
  The plan for the C++ Shell is for it to be fairly light, no heavy logic in this layer, especially no application specific logic.
  
*Host mono within the application*

Hosting mono and using the embedded apis is the only way I know of to have our javascript calls handled with managed code.
The setup for this doesn't look too rough, but it may take some time to fully understand how this works.  The goal here is to be able 
to get this working and embedded (with .net 4.5 support or later), and never touch this code.  For windows platforms we may be able
to embed the real .net runtime, maybe use some roslyn somewhere.  I'm unsure how this works and if it's possible.


So TLDR:

I'm going to attempt to create a C++ shell that hosts an embedded chromium web browser that has dev tools support.  It also needs 
to be able to run managed code to respond to javascript events that occur within chromium.  I would like this to be done in such way
whereas there is very little editing/modification that needs to be done on the C++ side.  Once this shell is finished I should be able 
to create different desktop apps with only html/css/javascript/c#.

What I've done so far.

* Cleaned off some C++ cobwebs.
* Successfully embedded chromium using CEF in my own app with minimal code.
* Got the Chrome Developer tools to show up and to close.
* Downloaded mono and made a couple changes to the embedded api and got it to compile (more about this later, basically copied what 
shana did)

What's next

* Build some small proof of concept apps with c# scripts, probably running in two different app domains.
* Mixing all this stuff together
* Refactoring the fuck out of everything so it's not a huge mess.





  
  

 


