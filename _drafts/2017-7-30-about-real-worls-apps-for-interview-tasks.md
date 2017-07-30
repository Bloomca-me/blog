---
layout: post
title: Why I created Redux-Tiles library
keywords: react.js, react, redux, redux-tiles, server-side rendering, prefetch, javascript
---

Recently I was in process of finding a new job, and because my main expertise is javascript, all my applications required some test in frontend (usually in React.js) and Node.js. They are not very different -- some basic API in node.js and (sometimes) data crunching, and for frontend it is some small "real world application". I will focus mostly on the latter, because in my applications we paid more attention to it.

Usually you are given some task which somehow reflects domain of the company, so you build small piece of functionality, which theoretically can be reused somewhere in where product. It is the opposite of the whiteboard interview, which has pretty notorious reputation, and supposed to be an interesting experience for both parties -- you solve some more or less "real" problem, and they can evaluate you based on skills you show applied to their tools and problems.
It is a pretty interesting trend, though -- I can only say from experience for front-end and Node.js jobs, but people are tend to ask you more hands-on tasks, rather than just canonical CS questions -- data structures, algorithms, etc.

In reality, though, it is not that good. Definitely, famous [Javascript fatigue]() contributes to it. Such tasks very rarely provide you any boilerplate, usually leaving you with vague phrases like "use whatever you want", but subtly impying that showing your own skills will be appreciated. Also, it is also kind of implied nowadays that you are proficient with modern javascript, so you will need babel -- at least for modules, otherwise it brings too much unnecessary problems, and then webpack-dev-server solves a lot of problems, so it makes sense to use webpack and all that ecosystem.

Here comes the first fun part. What should you choose? Write your own? Use a popular boilerplate? If so, which? I like to understand what is going on, and from my experience building any serious webapp requires "ejecting" configuration, or it complete rewriting, so in test tasks I also start with a blank folder, quickly scaffolding basic configuration (e.g. babel, jsx, hmr, sass, css modules). Although it takes not so long from me to start a new project, at the same time refreshing basics, it takes some -- and some parts, like HMR, are still pretty magical, despite all great efforts -- so, sometimes you have to debug your _configuration_, not _application_ (I definitely made this mistake couple of times, once spending around 25% of coding time on it, which prevented me from implementing couple of things. Everything ended up very well, because it was an on-site interview, but it easily might be not so good). Sometimes just libraries were updated and now are incompatible, but you will spend at least some time trying to figure it out (and debugging experience is not that pleasing in the current state of tools in JS).
The main problem here is expectations. You don't know precisely what do they expect from you here (and as I mentioned before, they rarely give you a clue about it), so it might be considered as a bad thing that you created it by yourself -- same for the opposite case, when you take one! Also, because the application is going to be run, building step is also part of your responsibilities, and there are a lot of possible optimisations, aside from `NODE_ENV=production` -- for instaRecently I was in process of finding a new job, and because my main expertise is javascript, all my applications required some test in frontend (usually in React.js) and Node.js. They are not very different -- some basic API in node.js and (sometimes) data crunching, and for frontend it is some small "real world application". I will focus mostly on the latter, because in my applications we paid more attention to it.

Usually you are given some task which somehow reflects domain of the company, so you build small piece of functionality, which theoretically can be reused somewhere in where product. It is the opposite of the whiteboard interview, which has pretty notorious reputation, and supposed to be an interesting experience for both parties -- you solve some more or less "real" problem, and they can evaluate you based on skills you show applied to their tools and problems.
It is a pretty interesting trend, though -- I can only say from experience for front-end and Node.js jobs, but people are tend to ask you more hands-on tasks, rather than just canonical CS questions -- data structures, algorithms, etc.

In reality, though, it is not that good. Definitely, famous [Javascript fatigue]() contributes to it. Such tasks very rarely provide you any boilerplate, usually leaving you with vague phrases like "use whatever you want", but subtly impying that showing your own skills will be appreciated. Also, it is also kind of implied nowadays that you are proficient with modern javascript, so you will need babel -- at least for modules, otherwise it brings too much unnecessary problems, and then webpack-dev-server solves a lot of problems, so it makes sense to use webpack and all that ecosystem.
nce, you can be asked, why have not you used [cross-env](), why did not you apply babel plugins for react in production mode, and why did not you [optimise SVGs](). The answer for all of these is extremely simple -- time! These all are very important steps and should not be overlooked during deploying real application, but polishing can take too much time.

The second part is an actual application. I personally spend on any test task no more than one working day (so, around 8 hours, and sometimes more, if I tinkered too much around configuration or some specific task sparked my curiousity in implementation details), and if I feel that I don't have enough time, I start to write more general code, omitting some details, putting TODOs and commentaries, explaining how I'd do it, having more time. And here comes the second problem -- usually we have 1/2 screens application, there we can somehow interact with API, and display different results based on that. Again, same problem as I mentioned before -- it is usually pretty unclear, what exactly they mean by "maintainable application, easy to extend and to support". Sometimes they expect you to bring [redux]()/[mobx]() with custom middleware, wrapping everything to the functions (so afterwards, when you will bring [server-side-rendering](), it will be easy to create new store per each request), and creating all sorts of wrappers for everything, which is possible to generalize. Seriously, once I got a feedback, that in a product card component (which had image, title, subtitle, description and other stuff), instead of one component, it should be separated to `ProductBanner` and `ProductDescription`. And don't get me wrong, it is a valid point, but it only _might_ be helpful -- unless they are somewhere reused, it will only add one level of indirection. And again, this might be helpful, especially if there are a lot of logic, tied to banner and description, but this was just purest component ever!
So, this is called `high-level thinking`. Anecdotally, this is what most companies are waiting from you, so after some number I started to skew naturally to more overengineered solutions, 

The last arguable thing is CSS. Ah, beautiful CSS -- so many discussions are about CSS, and so many efforts are made recently to completely omit writing it in the usual way, that sometimes especially progressive companies frown at you when they see it. I personally use [sass]() for that kind of projects, in combination with [css-modules](). The reason why I do that is that I still believe that, in case you don't need dynamic theming, and you are not going to use some sorts of shared packages of components, CSS (or any preprocessor) is a much superior way. First of all, editors have amazing support for it -- emmet, snippets, linting, etc. Second of all, css modules eliminate problem of unique class names -- basically, we just need to choose unique names in the scope of a single file (which, given modular structure of react application, is a pretty small scope), so this problem is also solved.

So, I learned couple of lessons here -- I highly recommend one to start with [create-react-app](), or something similar, but widely recognized and without a lot of additional stuff (so the reviewer won't be lost in different features of boilerplate). It might be not ideal for you, but it will be definitely good enough for your test task. The second lesson is to actually ask people, but very thoroughly, about level of details they want from you -- e.g. do they want from you some sceleton of the application with all correct abstractions, so it will be easy to add server-side rendering, reuse all possible components, add  