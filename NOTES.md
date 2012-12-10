Notes for the presentation.

## Intro

* Nice Ride MN is a bike share company that operates in the Minneapolis/Saint-Paul metro area.  Start in 2009 as a non-profit.  It became operational in June of 2010.
* (show app)
* This is the story of how we built it.  I will describe the code, methods, and libraries used in making this story/application.

## Data

* Nice Ride released their 2011 data.  Not really an official thing, but sent a data dump to someone and said that that person was free to share it.
* The data included the following
    * Names and locations of data.
    * Rental and demographic data on subscribers.
    * All the trips that were taken in 2011.  This included start and stop stations (not routes).
* No GPS units on bikes?  I have heard conflicting things.
 
## Goals

* With any visualization, we first thought about the ideas we wanted to convey.
* Brendan Slotterback did some great analysis to put a static map of route popularity.  This helped shape our vision.
* With a map in mind, we wanted to show the success of Nice Ride by showing bikes riding around the city.
* We decided to show an "Average day" of Nice Ride bikes.

## Data Processing

* First thing to think about was how we would get route data from only having start and end coordinates.  We needed some sort of database of streets, and specificially bike lanes, for the Twin Cities.
* We were in luck!  Open Street Map is just that, and its free!  You can go edit.
* But OSM is for the whole world, and the Twin Cities is just a small part of that.  Luckily, Mike Mugurski produces data exports of metro areas.
* Then we needed a way of finding the best bike route from point A to point B from the OSM data.  Routino is an application that does just that.
* PostGIS offered a geospatial database to store our data and processed data to do more analysis and querying.
* Python scripts were written to do processing and for glue code.
* Utilizing Python and PostGIS, we able to determine the popularity of routes (most traveled).
* Made map layer with TileMill of the routes weighted by popularity.  As well as stations.
* To find an "Average Day" we wanted to determine bike density.
* The most "Average Day" was determined as the day that was closest to the average day, determined by bike density.
* Data exported to JSON to be used in web application.

## Interface

* Undrescore.js is a utility library for Javascript.
* jQuery is "the" DOM manipulation library.
* Leaflet is a web mapping library.
* Wax is a library to help manage map tile sets.
* Layers on top.
* Animator.js is a really small, awesome animation handler in Javascript.
* As a time tracking visualization, we used Flot to show the bike density.
* Backbone.js is a great library to provide MVC in Javascript and helps organize an applicaiton.