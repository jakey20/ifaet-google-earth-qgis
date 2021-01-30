Converting .jpg files from Google Earth to GeoTIFF files for WED.

I do not recommend using this for entire airports. You should use this for small areas along with SASPlanet imagery.

## You Will Need
1. Google Earth Pro (https://www.google.com/earth/versions/#earth-pro)
2. QGIS (https://qgis.org/en/site/forusers/download.html)

## Export an image from Google Earth

First, find the airport or area you wish to use. Zoom the map so that you can see only the area you wish to download. 
In the top right, you will see a circle with an N and a small eye. This aligns how you see the image. In the eye, press the left mouse button and drag down until the view is looking **straight down**. After you do this, click the N to align the image perfectly. Lastly, uncheck 3D Buildings and Places under the "Layers" Tab.

Next, you need to save the image. 
To do this, go to "File" click "Save" and choose "Save as Image"
Click the "Map Options" Menu and uncheck all boxes for the clearest image. Click "Resolution" and choose Maximum. Finally, you will save your image. Click "Save Image" and save it somewhere on your computer.

## Importing Imagery to QGIS

To convert this imagery to be useable for our purposes, we will be using QGIS. 

When you first open QGIS, you should see a screen with a "News" tab. On the left side, you should see a tab called XYZ Tiles. Expand this. 

These are XYZ Layers. These are maps that you will need to align your imagery correctly.

> If you don't have the Browser panel, you can select **View > Panels > Browser** to make it appear.

You will need satellite imagery to make this work for airport editing.

Right-click **XYZ Tiles** and click **New Connection**. You will be using ESRI Imagery, this is the same imagery as the default WED imagery.

```
https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}
```

Fill in the name box with any name. I named mine "ESRI Imagery". Under the URL Tab, paste the link above. Finalluy, up the maximum zoom level. I recommend something over 21 as it will be helpful when aligning your imagery.

Finally, click "Ok" and then drag your new map down to the "Layers" tab.

Now we need to georeference the image. This will make your image look correct when you import it into WED.

Go to **Raster > Georeferencer**
Click the box in the top left to add a new raster image. This is the image you saved in Google Earth.

Now, you will need to select points on your google earth image to match it with the ESRI imagery.

You should see a + sign when you hover over the image. Zoom into your image, and pick a easy to see point that you can easily match on ESRI. Click this spot.
A box that asks you to enter map coordinates should appear. You will not be entering coordinates by hand, so click "From Map Canvas". This will bring you to your ESRI imagery. On your ESRI imagery, locate the *exact* same point you located on your google earth imagery. You want to match this as closely as possible for the most accurate imagery. 
Repeat this many times, the more points, the more accurate the imagery. I used 50+ on my first test run, but you may want more or less depending on the size of your image. I find that using easy to replicate areas such as taxiway edges, line intersections, and buildings is easiest. You also will want several points on the edges of the image.

Next, click the **gear icon**.

You should see several boxes. For the top box, choose "Polynomial 3". For the second box, choose "Lanczos". For the third box, Choose "Default CRS: EPSG:4326 - WGS 84"

Under "Output Raser" make sure you have selected the area you want to export your GeoTIFF file to. I export them to my Satellite Images folder.

Next, click the green **play button**. This may take a minute. Once it is finished, minimize the georferencer tab. You will see that your image has been overlayed onto the ESRI imagery. Under the "Layers" tab, right click your Google Earth imagery. Choose the "Transparency" tab. Move the slider down to about 50%. Click Apply, and then OK. Check it. Is it accurate? If not, head back over to the georeferencer and add more points. Repeat the above processes until you are satisfied with your imagery.

Once you are satisfied, you can close the georeferencer window. Whether or not you want to save the points is up to you. 

## Exporting Our Imagery

To export our imagery, navigate to the "Layers" tab. Right click your Google Earth layer and choose "Export". From here, choose "Save As". You should see a window with several settings.

At the very top you will see "Output Mode". You want to choose **Rendered Image**. Below, you will see Format. Leave this as GeoTIFF. Next, you will name your file. Click the 3 dots next to the name if you wish to change where you want to export it. Next, click the "CRS" tab. You will choose "Default CRS: EPSG:4326 - WGS 84"

All you need to do now is export your image and load it into WED. 

Congratulations! You've successfully taken Google Earth Imagery and imported it into World Editor.




