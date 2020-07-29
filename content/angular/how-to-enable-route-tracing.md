---
title: "How to enable Route tracing - Angular 2+"
date: 2020-07-27T18:17:25+05:30
lastmod: 2020-07-27T18:17:25+05:30
draft: false


weight: 1
author: Pankaj Prakash
authorLink: https://jsguru.org
description: "Find ways to enable angular route tracing (logs). Easy way to debug angular route configuration."
images: []

tags: ["Angular", "Router", "Debugging", "Tips", "Snippets" ]
categories: ["Angular"]
featuredImage: "/images/theme-documentation-basics/featured-image.jpg"

lightgallery: true
---

Debugging an Angular app route configuration may eat up your costly time. As it may get tricky to enable route logs. Many Angular beginners frequently ask me ways to debug issues with angular routing. In this post I will explain two simple techniques using which you can debug your route issues.

## RouterModule `enableTracing`

Angular has built in feature to log all routing events. However route logs are disabled by default, since it may annoy developers. Set the `enableTracing` flag in the root route configuration, to enable route logs. 

```ts
// Root  router
RouterModule.forRoot(routes, {
  enableTracing: true,
})
```

> **Note:** Generally _app-routing.module.ts_ or _app.module.ts_ file inject root route. But can vary from project to project.

Save it and let angular compile your project again. Tada, you can see group of logs on  the console on each route change. 

![RouterModule enableTracing logs on console output](/images/how-to-enable-route-tracing/router-module-enable-tracing.gif "RouterModule enableTracing logs on console output")


The above method logs all the router event changes to the console. However, you might not always want to see all router logs. Several times you want some specific router event logs. Which calls us for the second way to enable angular router trace.

## Router events

[Router](https://angular.io/api/router/Router "Angular router API") class provides several useful fields and functions. Out of all in this post we will talk about one special member of Router class. `Router.events` provides way to access all router events. You can subscribe to the field to get notified on any route change events.


```ts
constructor(
  private router: Router,
  /* Other dependencies */
) {

  this.router.events.subscribe(event => {
    console.group(`Router event: ${event.constructor.name}`);
    console.log(event);
    console.groupEnd();
  });
}
```

![Router.events logs console output](/images/how-to-enable-route-tracing/router-events.gif "Router.events logs console output")

This too prints the same output on console. But, our intention was to filter specific router event. You can apply filter to the `Router.events` stream using [rxjs filter operator](https://www.learnrxjs.io/learn-rxjs/operators/filtering/filter "RxJs filter operator API"). 

E.g. Following code logs only `NavigationStart` events.

```ts
this.router.events
  .pipe(
    // You can also use traditional if else in the subscribe 
    filter(event => event instanceof NavigationStart)
  )
  .subscribe(event => {
    console.group(`Router event: ${event.constructor.name}`);
    console.log(event);
    console.groupEnd();
  });
```

> **Note:** Since you are subscribing to an observable (`Router.events`) you must unsubscribe to it after the use. Possibly add unsubscription logic when component gets destroyed (`ngOnDestroy`). Otherwise it will cause memory leaks. 

&nbsp;
&nbsp;

Happy coding :man_technologist: