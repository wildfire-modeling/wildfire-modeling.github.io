## Welcome to the Data page of Uncertainty Aware Wildfire Management

![Recent Wildfires in California (Source: Wikipedia)](/images/wildfire.jpg?raw=true)

Recent wildfires in the United States, Australia, and Brazil have resulted in loss of life and billions of dollars, destroying countless structures and forests.  Fighting wildfires is extremely complex. A major problem in using data-driven models to combat wildfires is the lack of comprehensive data sources that relate fires with relevant covariates. We present the first open-source wildfire dataset that combines historical wildifre occurrences with relevant features extracted from satellite imagery. Our dataset, with over 2 million data points, is created using a novel approach to process large-scale raster and vector data. 

Our data can be accessed [here](https://drive.google.com/file/d/1B582y8_cPWxNuevpm3ZM-SZf_23HRUAQ/view?usp=sharing). Currently, we have mapped historical fire data in California, USA through the years 2012 to 2018. Our spatial resolution is in the form of 375-meter square polygons. Indication of wildfire is captured through fire radiative power (FPR). Additionally, each fire occurrence includes relevant information like type of vegetation, fuel type, and topography. The dataset can be used to learn data-driven models for fire spread as well as agent-driven approaches for fire suppression. We will present details about the database at the AI for Earth Sciences workshop at NeurIPS 2020. See the paper [here](https://ayanmukhopadhyay.github.io/files/neurips20.pdf). We have also explored how uncertainty aware wildfire management strategies can be used to suppress the spread of wildfires. Our paper, accepted at the AAAI Fall Symposium Series Workshop on AI for Social Good 2020 can be accessed [here](https://ayanmukhopadhyay.github.io/files/aaai_wildfire.pdf).

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
<th>Canopy Base Density sum</th>
<th>Canopy Base Density mode</th>
<th>Canopy Base Density count</th>
<th>Canopy Base Density mean</th>
<th> ... </th>
<th>Neighbor Slope max.</th>
<th>Neighbor Slope min.</th>
<th>Neighbor Slope median</th>
<th>Neighbor Slope sum</th>
<th>Neighbor Slope mode</th>
<th>Neighbor Slope count</th>
<th>Neighbor Slope mean</th>
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
<th>37.0</th>
<th>3.0</th>
<th>17.0</th>
<th>3109.0</th>
<th>24.0</th>
<th>169.0</th>
<th>18.396450</th>
</tr>
</tbody>
</table>

### Data Processing
To reconcile the different spatial resolutions in the different (raster and vector) forms, we divide the state of California into a 375-meter by 375-meter grid. The center of each fire pixel from the vector data can overlap with exactly one cell. We compute the *zonal statistics* for the vector data using the raster data. (Zonal statistics are summary statistics calculated using a raster dataset within zones defined by another dataset, typically in vector form.) The approach is fully decentralized and does not require data to be converted from one form to another. It computes an intermediate data structure, called an *intersections file*, between the two file formats. Leveraging parallel computing additionally, we assemble large geo-spatial data in a tractable manner.

### Cite
If you want to use this data for research, please cite it as follows:
["Diao, T., Singla, S., Mukhopadhyay, A., Eldawy, A., Shachter, R., & Kochenderfer, M. (2020). Uncertainty Aware Wildfire Management. arXiv preprint arXiv:2010.07915."](https://arxiv.org/abs/2010.07915) 
 Also forthcoming at NeurIPS AI for Earth Sciences Workshop December 2020.

### Contact
For any questions or comments, please contact us [Tina Diao](mailto:tdiao@stanford.edu), [Ayan Mukhopadhyay](mailto:ayan.mukhopadhyay@vanderbilt.edu), or [Samriddhi Singla](mailto:ssing068@ucr.edu).
