## Welcome to the Data page

We provide a [dataset](https://drive.google.com/file/d/1B582y8_cPWxNuevpm3ZM-SZf_23HRUAQ/view?usp=sharing) of historical fire spread in California, USA through the years 2012 to 2018 in 375-meter polygons. They include the landscape data (vegetation, fuel type, and topography) and the indications of wildfire presence in terms of fire radiative power (FPR). 

### Data Sources

We gather the raster dataset of [vegetation](https://www.landfire.gov/vegetation.php), [fuel type](https://www.landfire.gov/fuel.php), and [topography](https://www.landfire.gov/topographic.php) of years 2012, 2014, and 2016 from the [LANDFIRE](https://www.landfire.gov/index.php) website. They are in 30-meter square cells. 

The near real-time (NRT) [fire occurrence data](https://firms2.modaps.eosdis.nasa.gov/map/#d:2020-09-20..2020-09-21;@0.0,0.0,3z) in vector form are from the [Visible Infrared Imaging Radiometer Suite (VIIRS)](https://earthdata.nasa.gov/earth-observation-data/near-real-time/download-nrt-data/viirs-nrt) thermalanomalies/active fire database. They are in 375-meter square cells.

### Data Description
In our dataset, there are 2,367,209 datapoints which are daily fire occurrences in years 2012 through 2018. Each datapoint consists of a polygon cell on fire in a time step (a day), its polygon features (more details below) and its neighbor polygon's FRP in the next time step (next day). A zero-value in FRP indicates that its neighbor is not on fire.

The features include the cell's current FRP (a positive value as we condition on on a fire occurring), the maximum, minimum, median, mode, sum, mode, and count values of canopy base density, canopy base height, canopy cover, canopy height, existing vegetation cover, existing vegetation height, existing vegetation type from years 2012, 2014, and 2016, as well as those of elevation and slope from year 2016.

The labels are the neighbor's FRP in the next time step in continuous values.

#### Data Example 
<table>
<thead>
<tr>
<th>Polygon ID</th>
<th>Acquisition Date</th>
<th>FRP</th>
<th>Neighbor Polygon ID</th>
<th>Neighbor FRP</th>
<th>Canopy Base Density max.</th>
<th>Canopy Base Density min.</th>
<th>Canopy Base Density median</th>
<th>Canopy Base Density mode</th>
<th>Canopy Base Density sum</th>
<th>Canopy Base Density mode</th>
<th>Canopy Base Density count</th>
<th> ... </th>
</tr>
</thead>
<tbody>
<tr>
<td>7234</td>
<td>2012-01-16</td>
<th>3.20</th>
<th>7233</th>
<th>0.0</th>
<th>0.0</th>
<th>13.0</th>
<th>0.0</th>
<th>9.0</th>
<th>1303.0</th>
<th>0.0</th>
<th>156</th>
<th> ... </th>
</tr>
</tbody>
</table>

### Data Processing
To reconcile the different spatial resolutions in the different (raster and vector) forms, we divide the state of California into a 375-meter by 375-meter grid. The center of each fire pixel from the vector data can overlap with exactly one cell. We compute the *zonal statistics* (calculating summary statistics using a raster dataset within zones defined by another dataset, typically in vecotr form) for the vector data using the raster data. The approach is fully decentralized and does not require data to be converted from one form to another. It computes an intermediate data structure, called *intersections file*, between the two file formats. Leveraging parallel computing additionally, we assemble large geo-spatial data in a tractable manner.

### Contact
For any questions or comments, please contact us [here](mailto:wildfire.modeling20@gmail.com).
