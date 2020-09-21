## Welcome to the Data page

We provide a [dataset](https://drive.google.com/file/d/1B582y8_cPWxNuevpm3ZM-SZf_23HRUAQ/view?usp=sharing) of historical fire spread in California, USA through the years 2012 to 2018 in 375-meter polygons. They include the landscape data (vegetation, fuel type, topography) and the indications of wildfire presence in terms of fire radiative power (FPR). 

### Data Sources

We gather the raster dataset of vegation, fuel type, and topography data  of years 2012, 2014, and 2016 from the [LANDFIRE](https://www.landfire.gov/index.php) website. They are in 30-meter square cells. 

The near real-time (NRT) fire occurrence data in vector form are from the [Visible Infrared Imaging Radiometer Suite (VIIRS)](https://earthdata.nasa.gov/earth-observation-data/near-real-time/download-nrt-data/viirs-nrt) thermalanomalies/active fire database. They are in 375-meter square cells.

### Data Description
There are 2,367,209 datapoints for years 2012 through 2018. Each datapoint consists of a polygon cell on fire in a time step, its polygon features (more details below) and its neighbor polygon's FRP in the next time step. A zero-value in FRP indicates that its neighbor is not on fire in the next time step.

The features include the cell's current FRP (a positive value as we condition on on a fire occurring), the count, minimum, maximum, mean, median, mode, and sum values of canopy base density, canopy base height, canopy cover, canopy height, existing vegetation cover, existing vegetation height, existing vegetation type from years 2012, 2014, and 2016, as well as those of elevation and slope from year 2016.

The labels are the neighbor's FRP in the next time step in continuous values.

### Data Processing
To reconcile the different spatial resolutions in the different (raster and vector) forms, we divide the state of California into a 375-m by 375-m grid. The center of each fire pixel from the vector data can overlap with exactly one cell. We compute the *zonal statistics* (calculating summary statistics using a raster dataset within zones defined by another dataset, typically in vecotr form) for the vector data using the raster data. The approach is fully decentralized and does not require data to be converted from one form to another. It computes an intermediate data structure, called *intersections file* between the two file formats. Additionally leveraging parallel computing, we assemble large geo-spatial data in a tractable manner.

### Contact
For any questions or comments, please contact us [here](mailto:wildfire.modeling20@gmail.com).
