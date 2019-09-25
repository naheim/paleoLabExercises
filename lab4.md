# Lab Exercise 4: Introduction to Macrostratigraphy & the Macrostrat Database

## Instructions

Complete the following lab exercise and submit your answers as Word, Pages, or PDF document and your R script as a .r file by the start of lab on October 3, 2019. Please submit your files by email to noel.heim@tufts.edu.

## Objectives
The purpose of this lab is to introduce you to the concepts of macrostratigraphy and the Macrostrat database. By the end of this lab you should be able to download Macrostrat data using the API. You will also be able to calculate macrostratigraphic parameters and compare the fossil and geological record using R.  

## Introduction
In the 1970s and 1980s the Geological Survey of Canada and the American Association of Petroleum Geologists produced a series of stratigraphic correlation charts that show the geology of North America from the crystalline basement to the surface at over 800 locations. These charts were indented to standardize the stratigraphic nomenclature of geologic units and allow geologists to easily determine which units are roughly equivalent. However, these charts also contain a wealth of information on the geology of North America, including lithology, thickness, paleoenvironments, and economic minerals. Although the effort that went into producing these charts have gone largely unnoticed by geologists, the Macrostrat database has digitized these, and similar, records in order to leverage for purposes other than correlation and name standardization. In this laboratory exercise you will use Macrostrat to explore the spatial and temporal dynamics of North American geology.


## The Nomenclature of Macrostratigraphy
* **Units**: In Macrostrat, the finest division is called a unit and roughly corresponds to a formation-level lithostratigraphic unit. The colored boxes on figure 1 below are units.
* **Packages**: The key to macrostratigraphic analysis is recognizing unconformities, or 'gaps' in the geological record. Units are stacked into gap-bound packages--a vertical sequence of units with unconformities above and below that are resolvable to approximately 1 million years. In reality, most sedimentary units will have internal unconformities that are much shorter in duration than one million years, but these are not resolvalbe in the data used to construct Macrostrat. 
* **Columns**: Packages are stacked to form stratigraphic columns that summarize the geological history of a region.
* **Initiation**: The term used to describe what happens at the FAD of a package--the initiation of rock accumulation.
* **Truncation**: The term used to describe what happens at a package's LAD--the truncation of that package.

![macrostrat columns](lab4Figs/chart_columns.png)
**Figure 1** *Example of Macrostrat columns, packages, and units. The key to macrostratigraphy is that packages, because they are bound above and bleow by undonformities, or 'gaps', can be treated analytically in the same way we treat species in the fossil record. Namely, each package has times of first and last appearance.*


## Finding the Macrostrat Website
The URL for the Macrostrat is [macrostrat.org](https://macrostrat.org). Go there now in your web browser. The first thing that you should see is the **SPLASH** page. 

![splash page](lab4Figs/splashpage.png)

The Macrostrat splash page has a lot of information packed into it. At the bottom of the screen you will see some basic stats on the types and quantity of data located in the database.

Data Type | Definition
--------- | ----------
**Regional Rock Columns** | Regional summaries of the rock record in a particular place. In nearly all cases, the columns describe the record from the surface down to crystalline basement rock.
**Rock Units** | A formation-level lithostratigraphic unit. Columns are composed of units. 
**Geologic Map Polygons** | Macrostrat also has global and regional geologic maps. Each map polygon corresponds to a colored geological map unit.

If you scroll down, you will see the four major projects currently part of Macrostrat.

## Macrostrat Units & Columns

Click on the *Search* button near underneath the Macrostrat stats on the splash page.

The page you get will be a randomly selected macrostrat column, and should look something like this.
![random column](lab4Figs/random_column.png)

You are presented with the location of the stratigraphic column on a maps as wells as some summary statistics about the column, including the numbers of units and packages, the distribution of lithologies, age range, total thickness, and area. You are also presented with the number of collections. This refers to the the number of paleobiology Database collections that have been matched to units in the column.

#### Exercise Questions 1
Search for 'Hindsville' in the search bar at the upper right. This will take you to the summary page for the units named Hindsville.

1. Where is the Hindsville located?

2. What age is the Hindsville? Give the period and stage names.

3. How thick is the Hindsville?

4. Why are there three columns that have Hindsville units?  

5. What proportion of the Hindsville is sandstone?

6. What are the prevalent taxa found in the Hindsville?

Click on the gray polygon that contains the city of Fayetteville. This will take you to the summary page for that column.

7. What is the name of the column?

8. How thick is the column?

9. How many PBDB collections have been matched to units in this column and what are the prevalent taxa?

At the bottom of the page is a graphical rendering of the units within the column.

10. How many packages are in this column and how are the delineated on the figure?

11. How many units have PBDB collections?

12. What are the units above and below the Hindsville? Are each of these units in the same or different packages?


## Macrostrat API

Unlike the PBDB, Macrostrat does not provide a form for downloading data. However, like the PBDB, it does have an API. The API has the general form as the PBDB API, but the documentation is not nearly as verbose. To get to the API, click on the API link on the splash page. You should end up at a splash screen for the API documentation that looks like this.

![api splash screen](lab4Figs/api_splash.png)

To get to the main documentation click on **API root** or go directly to [macrostrat.org/api](http://macrostrat.org/api). You should see something that looks like this.

![api documentation](lab4Figs/API_documentation.png)

The documentation is formatted in JSON. You may want to add a free JSON parser extension for your browser. For Macs, I like JSON Peep for Safari and JSON Lite for Firefox, but there are others for other browsers and operating systems.

We want to download all the data for North America and the Caribbean. In order to do this, we need to look their project ID numbers. We can do this via the *defs* route. For the *defs* route, it is sometimes useful to have all the records returned. To do this, simply include the single parameter *all*: [https://macrostrat.org/api/defs/projects?all](https://macrostrat.org/api/defs/projects?all)

**Paste this URL into your browser and make note of the IDs for the North America and Caribbean projects.**

## Plotting marine rocks in North America & Caribbean
Now we want to look at the history of marine sedimentation and the fossil record in North America and the Caribbean. You will do this in R drawing on your knowledge from last week's lab on using APIs to plot data in R. 

In addition to answering the questions below, you will also need to submit a .r script containing your code for downloading data, calculations, and generating your plots. This script should be well documented (i.e., explanatory comments) and should run without error. You may need to review loops and plotting from [Getting Started with R](https://github.com/naheim/rTutorials/blob/master/manipulatedf.md) and you will use skills you learned last week in [Lab 3](lab3.md).

### Step 1: Download marine packages from Macrostrat
Use the API to download the data. For our analyses here we will only be examining packages in North America and the Caribbean that contain only sedimentary rocks of marine origin. For historical reasons, the route to examine packages is called sections. Look at the documentation for the *sections* route to construct your call to the API. The parameters you want to retrieve only marine and only sedimentary rocks are *environ_class* and *lith_class*. If you are unsure what the parameter values should be, you can look up the possible values in the *defs* route (but your first guess will probably work :wink:). 

Macrostrat only offers two output formats for the sections route: JSON and csv. You can read JSON into R, but it will require additional processing. Since csv is essentially a "native" format for R, we'll use that. Make sure you include the parameter *format* and set the value to *csv*. Last week when working with PBDB downloads in R, we downloaded files with tab-delimited values (tsv). To get csv files, you'll need to use the ``read.csv`` instead of ``read.tsv()``, otherwise the two functions work the same.

### Step 2: Download the timescale
As in the PBDB, Macrostrat also has information on the geological timescale. Use the *intervals* route to get the time intervals of interest. You will need to specify a timescale. The timescale we are interested in is the *international ages*. Use the *defs* route to see the other available timescales. Also be sure to specify that you want a csv.

An important thing to note about web addresses is that they can only have letters, numbers, and 4 special characters (- _ . ~). In order to put any other characters, including spaces, into a web address, those characters need to be encoded as % plus a two-digit hexadecimal representation--when the web address is being read by the server, the % indicates that the next two characters should be interpreted as special characters. This is important, because when we put the timescale name, *international ages*, into our URL it has a space that needs to be encoded. The code for a space is *%20*. However, you don't need to remember this. When you put the URL with spaces or other characters directly in your web browser, the browser does the encoding for you. Likewise, R has a nifty function called ``URLencode()`` that will encode all special characters before passing it to a web server--but you have to use this function or you will get an error. Here's an example of how the function works.

````r
myWebAddress <- "https://paleobiodb.org/data1.2/taxa/single.tsv?name=Elrathia kingii"
myWebAddress # this will print the exact string with a space between the species and genus names.
# if we try to download data with this URL we will get an error
e.kingii <- read.delim(myWebAddress) # download the data--it should work

# now let's encode
myWebAddress <- URLencode("https://paleobiodb.org/data1.2/taxa/single.tsv?name=Elrathia kingii")
myWebAddress # now note that the space has been encoded.

e.kingii <- read.delim(myWebAddress) # download the data--it should work
e.kingii
````

* Download pbdb collections
* Plot history of rock quantity
* Plot number of collections
* Plot proportion of matched packages


The best way to think about using an API is to imagine it as a map to all the data stored online. You need to use this map to give the computer directions on how to find the particular data you want and access it. When we give directions to a location in the real world, we generally do so in two ways. We either give geographic coordinates (i.e., latitude, longitude, elevation) that specify the destination, or a set of routes to get somewhere (e.g., Take I-90 E to Chicago, then I-80 W to Joliet).

When we access data in R via **subscripting** (`Object[ ]`), we are using a coordinate system to point out the data in our object. In contrast, when we access data through an API we are defining a **route**. In fact, route is the formal terminology. Depending on the size of an API there may be dozens of routes, which may feel overwhelming at first. However, remember that a car map has thousands or hundreds of thousands of roads, most of which you will never travel upon, but you still know how to use a map. It is the same way with an API.