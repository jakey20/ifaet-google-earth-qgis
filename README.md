Converting .jpg files from Google Earth to GeoTIFF files for WED.

I do not recommend using this for entire airports. You should use this for small areas along with SASPlanet imagery.

## Export an image from Google Earth

First, you will need to export an image from google earth.

1. Open Google Earth Pro ([desktop version](https://www.google.com/earth/versions/#earth-pro))
2. Browse to where you want to be.
3. Click the **Save image** button
4. Increase the resolution of your image + remove all of the extraneous elements
5. Click **Save image** to save your image

![Google earth export](images/00-google-earth.png)

## Adding our reference layer

First we need to add an underlay. You will use this to match up where your map belongs.

These are called "XYZ" layers, and they're built into QGIS. You can click and drag them from the **Browser** panel into your **Layers** panel. I'm using OpenStreetMap, because it's apparently the only one already in QGIS.

![XYZ layer](images/01-xyz.png)

> If you don't have the Browser panel, you can select **View > Panels > Browser** to make it appear.

However, you will need satellite imagery to make this work for IFAET.

Right-click **XYZ Tiles** and click **New Connection**. You will use ESRI Imagery, this is the same imagery as the default WED imagery.

```
https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}
```

![XYZ layer new connection](images/01-xyz-new-connection.png)

Fill in the box..

![XYZ layer filled in details](images/01-xyz-filled.png)

And then drag it to your map!

![better XYZ layer from ESRI](images/01-xyz-better.png)

> {z} is zoom, and {x} and {y} are the [coordinates of the file](https://developers.google.com/maps/documentation/javascript/coordinates#tile-coordinates).

## Georeferencing

Now we need to georeference, which is how you give your image a latitude/longitude (and stretch it to make it look 'right').

Go to **Raster > Georeferencer**

![](images/02-georef.png)

Click the box in the top left to add a new raster image. When it asks you for your CRS, pick `WGS 84 EPSG:4326` (I actually don't think it matters).

![](images/02-add-raster.png)

Now you'll need to match up points on your image with points on your basemap. First, click somewhere on your image that is memorable - the edge of a peninsula, or a curve in the land or something.

![](images/02-click-1.png)

QGIS will ask you, where is this?

![](images/02-map-coords.png)

You don't memorize lat and lon of random points in the world, so you click **From map canvas**.

Click the same point in your XYZ layer and _tada!_, it filled the points in for you. Click **OK**.

![](images/02-click-2.png)

![](images/02-post-click.png)

Do this a million times, and eventually you'll have a million georeferenced points. You want as many as possible for airport editing. The more points, the more accurate your image.

![](images/02-lots-of-points.png)

Now click the **gear icon** to change the settings.

![](images/02-gear.png)

According to [this random internet person](https://ieqgis.wordpress.com/2014/05/22/how-to-georeference-a-map-in-qgis/) you should use **Polynomial 3** for Transformation type and **Lanczos** for Resampling method.

Make sure you've selected an output file and **Load in QGIS when done** is checked and click **OK**

![](images/02-settings.png)

Now click the green **play button**. It'll take some time thinking, then..... it'll look like nothing happened! But if you minimize the georeferencer you'll see it got exported and put onto the map.

![](images/02-play.png)

![](images/02-played.png)

To check that it's okay, right click the new layer, select **Properties**, go to the **Transparency** section and dial it down to 50% or so.

![](images/02-properties.png)

![](images/02-transparency.png)

![](images/02-matched.png)

If it doesn't look good, delete the layer, open the georeferencer window (remember you only minimized it!) and add some more points or delete ones you did poorly.

Once you're satisfied, you can close the georeferencing plugin. It'll ask if you want to save the points.... but I say no!

## Clipping our raster

Now we have a beautiful image that is way too big and with all kinds of weird black stuff where it got stretched to fit on the map.

![](images/03-black-stuff.png)







