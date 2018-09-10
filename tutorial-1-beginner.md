author: Stamen Design
summary: Make a map in XYZ Studio
id: 1
categories: map
environments: js
status: draft
feedback link: https://github.com/here-xyz-codelabs/here-xyz-codelabs.github.io/issues
analytics account: 0

# Make a map in XYZ Studio

## Introduction

This tutorial shows you how to create a simple map in XYZ studio.

### What you'll learn
* The basics of XYZ Studio
* How to upload a GeoJSON file to XYZ Studio
* How to add your new dataset to an XYZ project
* How to style the map with colors and symbols
* How to add interactivity with pop-ups
* How to publish and share your map

### Prerequisites
* None

In this demo we’ll download a public GeoJSON file from the Los Angeles County open data website, then upload it to XYZ Studio.



## Downloading the data

Go to https://data.lacounty.gov/ and search for “restaurant inventory”.

Click on "LOS ANGELES COUNTY RESTAURANT AND MARKET INVENTORY"

It should take you to this page: https://data.lacounty.gov/Health/LOS-ANGELES-COUNTY-RESTAURANT-AND-MARKET-INVENTORY/jf4j-8it9

By default, it will try to export as a CSV, but in our case we want it as a GeoJSON. To do this, click the "API" button. Then where it says "JSON", click and change this to "GeoJSON".

Then copy the URL (which should be this: https://data.lacounty.gov/resource/46rk-iuuu.geojson) 

But we want to download all the records, so let's add something to that URL here: 

https://data.lacounty.gov/resource/46rk-iuuu.geojson?$limit=50000

(you can learn more about the API options from these docs: https://dev.socrata.com/foundry/data.lacounty.gov/46rk-iuuu)

![download geojson](images/tutorial-1-download.png)

You can open up this restaurants-data.geojson file if you’re curious about the GeoJSON file format… [but need suggestions on what software will show it nicely-formatted, since it doesn’t have line breaks]

## Uploading to XYZ Studio

Now let’s open up XYZ Studio. https://xyz.here.com/studio

When you open XYZ Studio you’ll see your Dashboard. There is one tab for “Projects” (you can think of these as “maps”) and another tab for “Data Hub” (which is where you can manage data layers to add to your maps).

At first you’ll see your dashboard, with the “Projects” tab active. If you’re just getting started with Studio, you probably don’t have any projects or data yet.

Let’s go to Data Hub first, by clicking on that tab. Then click the “Create new dataset” button.


![XYZ Studio Data Hub](images/tutorial-1-datahub.png)

This will bring you to a list of your datasets and a “Upload new dataset” button. Here you can upload the GeoJSON file that you downloaded to your computer.

Here we could create a new "Project" with the dataset, or we could go to the Projects tab and create one there. Let's click on the Projects tab now.

Now we’ll see the project’s page. Let’s give this project a name, something like “LA Restaurants”.

Right now, there’s no data in our map. All we have is a “basemap”, which is the background map that we will layer our data on top of. You have a few color options for your basemap. Feel free to pick whichever one you like.

But now we need to add a layer to our map. Click the `+ Add` button, and a new window will open up, prompting you to add some data from your “Data Hub”. Here we can select the GeoJSON layer that we just uploaded.

## Style the data

Now let’s navigate back to our Projects and view our “LA Restaurants” project. Use the `+ Add` button to add a layer to the map, if you haven’t already.

Adjust the style of the points (currently all the points have to have the same style, but we’re working on attribute-based styling). You can adjust the size, color, stroke, etc.

You can also customize your pop-up window (called “Cards”) by dragging the fields into a meaningful order, and choosing which field should be the title in the pop-up.

## Share the map
We’re almost ready to publish our map, but first we have to set the default view. This is called a “bookmark” and we can make one by clicking the bookmark icon near the top.

Now let's share the map! Click the “Project Settings” button in the lower left corner of the window. Here you can publish your Project, and get sharable links that anyone can view online or embed in a webpage.

![XYZ Studio Publish window](images/tutorial-1-publish.png)


The sharable URL will look something like this: https://xyz.here.com/viewer/?project_id=cbb04410-a112-11e8-a434-db0102d2f39c
