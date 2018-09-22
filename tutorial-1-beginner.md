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

In this demo we’ll download a public GeoJSON file of earthquake locations from the USGS, then upload it to XYZ Studio.


## Downloading the data

Go to [https://earthquake.usgs.gov/earthquakes/feed/](https://earthquake.usgs.gov/earthquakes/feed/) and scroll down to "GeoJSON Summary Feed". Click on that link.

![usgs downloads](images/tutorial-1-usgs-download.png)


On the [GeoJSON Summary Format](https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php) page, click "All Earthquakes" for the past 30 days. The link is at the bottom right corner of the page.

![usgs geojson](images/tutorial-1-usgs-geojson.png)

Download the [all_month.geojson](https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_month.geojson) file to your computer. Depending on your browser and your operating system, clicking that link might be enough to start the file downloading. But if you see a bunch of random text on your screen, you might be looking at the raw GeoJSON file. If so, you may need to go to the `File > Save Page As...` menu in your browser to download this file to your computer. If you are a Safari user, you might see the option to save the page as a Web Archive. You don't want that option. Choose "Page Source" instead.

Also, make sure that when you've downloaded the file, the full file name is `all_month.geojson`. If your operating system adds any additional file extension to the end (such as `all_month.geojson.json` or `all_month.geojson.txt`) make sure to remove that extra file extension by renaming the file.

Depending on how many earthquakes have happened in the last month, the file size will be something around 8 megabytes.

You can open up this GeoJSON file if you’re curious about the GeoJSON file format. If you're not curious, you can skip ahead to the next step.

If you open the GeoJSON file, the first few lines should look something like this, which is not particularly easy to read:

```
{"type":"FeatureCollection","metadata":{"generated":1537581272000,"url":"https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_month.geojson","title":"USGS All Earthquakes, Past Month","status":200,"api":"1.5.8","count":9850},"features":[{"type":"Feature","properties":{"mag":null,"place":"14km E of Seven Trees, CA","time":1537581188710,"updated":1537581270267,"tz":null,"url":"https://earthquake.usgs.gov/earthquakes/eventpage/nc73087921","detail":"https://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/nc73087921.geojson","felt":null,"cdi":null,"mmi":null,"alert":null,"status":"automatic","tsunami":0,"sig":0,"net":"nc","code":"73087921","ids":",nc73087921,","sources":",nc,","types":",nearby-cities,origin,phase-data,","nst":19,"dmin":0.04379,"rms":0.02,"gap":70,"magType":null,"type":"earthquake","title":"M ? - 14km E of Seven Trees, CA"},"geometry":{"type":"Point","coordinates":[-121.67733,37.3076668,6.59]},"id":"nc73087921"},
{"type":"Feature","properties":{"mag":1.6,"place":"121km NW of Arctic Village, Alaska","time":1537580268294,"updated":1537580544761,"tz":-540,"url":"https://earthquake.usgs.gov/earthquakes/eventpage/ak20260406","detail":"https://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/ak20260406.geojson","felt":null,"cdi":null,"mmi":null,"alert":null,"status":"automatic","tsunami":0,"sig":39,"net":"ak","code":"20260406","ids":",ak20260406,","sources":",ak,","types":",geoserve,origin,","nst":null,"dmin":null,"rms":0.72,"gap":null,"magType":"ml","type":"earthquake","title":"M 1.6 - 121km NW of Arctic Village, Alaska"},"geometry":{"type":"Point","coordinates":[-147.7682,68.8514,0]},"id":"ak20260406"},
{"type":"Feature","properties":{"mag":0.41,"place":"10km NE of Aguanga, CA","time":1537578694200,"updated":1537578914440,"tz":-480,"url":"https://earthquake.usgs.gov/earthquakes/eventpage/ci37363842","detail":"https://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/ci37363842.geojson","felt":null,"cdi":null,"mmi":null,"alert":null,"status":"automatic","tsunami":0,"sig":3,"net":"ci","code":"37363842","ids":",ci37363842,","sources":",ci,","types":",geoserve,nearby-cities,origin,phase-data,scitech-link,","nst":15,"dmin":0.0803,"rms":0.17,"gap":118,"magType":"ml","type":"earthquake","title":"M 0.4 - 10km NE of Aguanga, CA"},"geometry":{"type":"Point","coordinates":[-116.7776667,33.4923333,4.33]},"id":"ci37363842"},
    ...
    ...
    ...

```

If we want to see the structure more clearly, we can add some linebreaks, shown below.

Positive
: NOTE: linebreaks are completely optional! Computers don't care if their GeoJSON files have linebreaks or not. We're adding them here just to make the file more human-readable.

Now you can see how the GeoJSON features are structured, where each feature has a set of `properties` and also a `geometry`. If you are curious to learn more about GeoJSON, the [Wikipedia article](https://en.wikipedia.org/wiki/GeoJSON) is quite informative.

```
{
  "type": "FeatureCollection",
  "metadata": {
    "generated": 1536625395000,
    "url": "https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_month.geojson",
    "title": "USGS All Earthquakes, Past Month",
    "status": 200,
    "api": "1.5.8",
    "count": 11986
  },
  "features": [
    {
      "type": "Feature",
      "properties": {
        "mag": 0.42,
        "place": "4km WNW of Anza, CA",
        "time": 1536623825450,
        "updated": 1536624040422,
        "tz": -480,
        "url": "https://earthquake.usgs.gov/earthquakes/eventpage/ci38055935",
        "detail": "https://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/ci38055935.geojson",
        "felt": null,
        "cdi": null,
        "mmi": null,
        "alert": null,
        "status": "automatic",
        "tsunami": 0,
        "sig": 3,
        "net": "ci",
        "code": "38055935",
        "ids": ",ci38055935,",
        "sources": ",ci,",
        "types": ",geoserve,nearby-cities,origin,phase-data,scitech-link,",
        "nst": 15,
        "dmin": 0.01985,
        "rms": 0.1,
        "gap": 94,
        "magType": "ml",
        "type": "earthquake",
        "title": "M 0.4 - 4km WNW of Anza, CA"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -116.7155,
          33.5733333,
          11.31
        ]
      },
      "id": "ci38055935"
    },
    ...
    ...
    ...
```

## Uploading to XYZ Studio

Now let’s open up XYZ Studio. [https://xyz.here.com/studio](https://xyz.here.com/studio)

When you open XYZ Studio you’ll see your Dashboard. There is one tab for “Projects” (you can think of these as “maps”) and another tab for “Data Hub” (which is where you can manage data layers to add to your maps).

At first you’ll see your dashboard, with the “Projects” tab active. If you’re just getting started with Studio, you probably don’t have any projects or data yet.

![XYZ Dashboard](images/tutorial-1-dashboard.png)

Let’s go to Data Hub first, by clicking on that tab. Then click the “Create new dataset” button.

![XYZ Studio Data Hub](images/tutorial-1-datahub.png)

This will bring you to a list of your datasets and a “Upload new dataset” button. Here you can upload the GeoJSON file that you downloaded to your computer.

![XYZ Studio Upload Data](images/tutorial-1-upload-data.png)

Here we could create a new "Project" with the dataset, or we could go to the Projects tab and create one there. Let's click on the Projects tab now.

## Creating a project

Now if we click on Projects, we’ll see the project’s page. Let’s give this project a name, something like “Earthquakes”.

![XYZ Studio untitled project](images/tutorial-1-untitled-project.png)

Right now, there’s no data in our map. All we have is a “basemap”, which is the background map that we will layer our data on top of. You have a few color options for your basemap. Feel free to pick whichever one you like. For example, here's a light-colored map:

![XYZ Studio changed basemap](images/tutorial-1-changed-basemap.png)

But now we need to add a layer to our map. Click the `+ Add` button, and a new window will open up, prompting you to add some data from your “Data Hub”. Here we can select the GeoJSON layer that we just uploaded.

![XYZ Studio Add Data](images/tutorial-1-add-data.png)

## Style the data

Now let’s navigate back to our Projects and view our “Earthquakes” project. Use the `+ Add` button to add a layer to the map, if you haven’t already.

Adjust the style of the points (currently all the points have to have the same style, but we’re working on attribute-based styling). You can adjust the size, color, stroke, etc.

![XYZ Studio point styling](images/tutorial-1-point-styling.png)

You can also customize your pop-up window (called “Cards”) by dragging the fields into a meaningful order. The first field will be the title in the pop-up, and any fields below the solid line won't show up in the card at all.

![XYZ Studio cards](images/tutorial-1-cards.png)

## Share the map
We’re almost ready to publish our map, but first we have to set the default view. This is called a “bookmark” and we can make one by clicking the bookmark icon near the top.

![XYZ Studio bookmark](images/tutorial-1-bookmark.png)

Now let's share the map! Click the “Project Settings” button in the lower left corner of the window. Here you can publish your Project, and get sharable links that anyone can view online or embed in a webpage.

![XYZ Studio Publish window](images/tutorial-1-publish.png)


The sharable URL will look something like this: [https://xyz.here.com/viewer/?project_id=ef9c4480-b55a-11e8-875f-e507603e6a20](https://xyz.here.com/viewer/?project_id=ef9c4480-b55a-11e8-875f-e507603e6a20)
