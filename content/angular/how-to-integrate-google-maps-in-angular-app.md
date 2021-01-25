---
title: "How to Integrate Google Maps in Angular App"
date: 2021-01-22T21:09:09+05:30
draft: false


weight: 1
author: Pankaj Prakash
authorLink: https://jsguru.org
description: "In this tutorial series, I will explain you how easily you can integrate google maps in your angular application."
images: []

tags: ["Angular", "Google Maps"]
categories: ["Angular"]
featuredImage: "/images/how-to-integrate-google-maps-in-angular-app/feature.png"

lightgallery: true
---

You might have came across several applications with maps. From open source to subscription based, there are several maps options available over internet. In this tutorial series, I will explain you how easily you can integrate [google maps](https://www.google.com/maps) in your angular application.

<!-- more -->

{{< admonition info >}}
Google Maps is a subscription based maps solution. You must create a billing account to integrate google maps in your app.

Please read the [Google Maps Platform starter guide](https://developers.google.com/maps/gmp-get-started). It will help you to get started with a new google **billing account** and **API key**, which you will require later in this project.
{{< /admonition >}}

## Create an angular app
Let us create a new angular app. We will use this app for this tutorial series. Open terminal and hit following command.

```bash
ng new maps-guru
```

**Note:** This is optional step if you want to integrate google maps in your existing angular app.

## Install types
Installing types support for google maps helps immensely with intellisense in most of the modern code editors and IDE. 

Open your angular project root directory and install following package. 

```bash
npm i -D @types/googlemaps
```

Let the typescript server know about the new typings. Open `tsconfig.json` and add a new item to `"compilerOptions.types"` array.
Ensure your `tsconfig.json` file looks similar to following.

```json
{
  "compilerOptions": {
    ...,
    "types": [
      "googlemaps"
    ]
  }
}
```

One final step to ensure your typescript server knows about the typings. Add following line at the beginning of `main.ts` file.

```ts
/// <reference types="googlemaps" />
```

## Load Google Maps JS API
Before continuing to this step ensure you have created a new google billing account. If not, at least you have generated a new API key.

There are different ways to load google maps JS API. However, for the sake of simplicity we will go with the easiest solution.

We will load our google maps JS API in `index.html` file. Add following line to your `index.html` file. Ensure you replace `API_KEY` with **your google maps API key**.

```html
<script src="https://maps.googleapis.com/maps/api/js?key=API_KEY" defer></script>
```

## Google Maps API
Google Maps provides `google.maps.Map` class. Using this we can create a new instance of map and render to the DOM. The class excepts two parameters.
  1. Instance of DOM element where we want to render our map.
  2. Object of type `google.maps.MapOptions` that defines extra properties used to customize the map. You must provide at least two params as `MapOptions` i.e. `center` and `zoom`.

      - `center` Object specifying initial latitude and longitude for the map to focus.
      - `zoom` An integer that specifies the initial resolution for the map. You can specify a zoom level between 0-20. 
      
The below list shows approximate level of detail you can expect to see at each zoom level.
 - 1: World
 - 5: Landmass/continent
 - 10: City
 - 15: Streets
 - 20: Buildings 

## Integrate in your app
Keeping the legacy intact, let us start with a hello world example. Run below command to generate `hello-world` component. 
```bash
ng g c components/hello-world
```

### Create DOM element to render map
Add a new `div` to our `hello-world.component.html`. This is the place where our map gets rendered.
```html
<div #googleMap id="hello-world-map"></div>
``` 

**Note:** We will use `#googleMap` as a reference point to get the instance of `div` element later.

For now let us adjust the height and width of the map. Open `hello-world.component.scss` and add below lines.
```css
#hello-world-map {
  height: 100vh;
  width: 100vw;
}
```

### Render map to DOM
To render a map we will use below `MapOptions` object.
```ts
const mapOptions: google.maps.MapOptions = {
  // Centered to Hyderabad, India
  center: new google.maps.LatLng(17.412127, 78.474921),
  zoom: 15,
};
```

You can get the instance of DOM element using `@ViewChild` in angular.
```ts
@ViewChild('googleMap', { static: true })
googleMapRef: ElementRef;

// Use `this.googleMapRef.nativeElement` to get instance of google map DOM element
```

Let's bring it all together. 

{{< highlight ts "hl_lines=22-31 10-14 19" >}}
import { Component, ElementRef, OnInit, ViewChild } from '@angular/core';

@Component({
  selector: 'app-hello-world',
  templateUrl: './hello-world.component.html',
  styleUrls: ['./hello-world.component.scss']
})
export class HelloWorldComponent implements OnInit {

  @ViewChild('googleMap', { static: true })
  googleMapRef: ElementRef;

  // Will contain the reference of rendered map instance 
  map: google.maps.Map;

  constructor() { }

  ngOnInit(): void {
    this.initMap();
  }

  private initMap(): void {

    const mapOptions: google.maps.MapOptions = {
      // Centered to Hyderabad, India
      center: new google.maps.LatLng(17.412127, 78.474921),
      zoom: 15,
    };

    this.map = new google.maps.Map(this.googleMapRef.nativeElement, mapOptions);
  }

}
{{< / highlight >}}

### Run application
{{< iframe src="https://stackblitz.com/edit/maps-guru-hello-world?ctl=1&embed=1&file=src/app/components/hello-world/hello-world.component.ts&hideExplorer=1&hideNavigation=1&view=preview" width="100%" height="400px">}}

&nbsp;  
&nbsp;  
Happy Coding :man_technologist:

&nbsp;  
&nbsp;  
**References**
  - [Google Maps JS API documentation](https://developers.google.com/maps/documentation/javascript/overview)
  - [Source code](https://github.com/PankajPrakashh/googlemaps.projects.jsguru.org/releases/tag/hello-world)