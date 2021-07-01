# SPACE4GOOD

## "A customized route planner for East Kalimantan, Indonesia"


## Contributors:
Mc Cabe, Andrew <andrew.mccabe@wur.nl>,
Harteveld, Damiaan van <damiaan.vanharteveld@wur.nl>,
Lossou, Etse <etse.lossou@wur.nl>,
Molewijk, Isa <isa.molewijk@wur.nl>,
Llort Marin, Julia <julia.llortmarin@wur.nl>.


    ----------------------
    This script is designed as part of an ACT project to produce a shortest 
    route to fire and/or deforestation incident locations in East Kalimantan.
    Indonesia.
    -------------
    
## Getting Started

### Setting up the environment
 
The script is entirely written in Python. The coding was performed in Jupyter Lab and Spyder 5.0.4. 
To set up the environment you need to do the following:

#### In anaconda:
    conda create --name nameofenv
    conda activate nameofenv
    conda install jupyterlab spyder
    conda install "osmnx<1.0"
    conda install -c conda-forge "networkx>2.5"
    conda install momepy
    
#### In Jupyter Lab or Spyder

Run the script!

The necessary packages are:

    folium, geopandas, momepy, networkx, numpy, os, osmnx, pandas, 
    pyproj and requests
    
The script is based on the [OSMnx 0.16.2](https://github.com/gboeing/osmnx/blob/main/CHANGELOG.md) , a depracated version of [OSMnx](https://osmnx.readthedocs.io/en/stable/). This script relied on the OSMnx 0.16.2 version due to the unavailability of OpenStreetMap data fo the study. Transforming a geojson file to a graph in OSMnx requires attribute information such as osmid, starting node and end note, all of which were not provided. We performed a workaround with the road network provided and tested it with OSMnx 1.1.1 but it did not work out.It was only possible with the OSMnx package.The steps involved in generating a shortest path within the study area from any two random points are as follow:

1. The script first creates an output folder if it does not exist.
2. The script checks whether or not there is an existing road network in a geojson format.
3. If yes, it transforms the the geojson file into an undirected graph using the momepy package.
4. If no, it downloads the road network and then transforms it into an undirected graph.
5. This is followed by the conversion from undirected graph to directed graph.
6. the script then retains only the largest connected graph in the network.
7. The next step is the extraction of **nodes** and **edges** from the graph.
8. The script then:
	1. Transforms the starting node and end node of the edges into u and v attributes.
           These attributes are essential for the creation of a graph in OSMnx.
	2. Creates three (3) additional attributes for the nodes namely Longitude (X), Latitude (Y) 
           and street_count and automatically assign values to the columns.	  
9. The derived nodes and edges are then used to generate a functional graph in OSMnx.
10. The OSMnx graph is used to derive the shortest path.


## Output
The script requests latitudes and longitudes of the origin and destination
from the user and produces a shortest route and saves the output in a geojson format.
For quick visualisation, a copy of the shortest route is available in Jupyter Lab. The user 
has to open it with a browser if he/she run the scrip in Spyder. This file is located in 
the output folder that was created by the script and can be found in the directory.
To check the currecnt directory, the user can run this code: **os.getcwd()**


## Acknowledgement
Our thanks goes to Nandika Tsendbazar, for her advisory role. Special thanks to Corné Vreugdenhil for providing expert advice with the use Networkx and OSMnx packages Python expert,  and Dainius Masiliunas who was of great help when we seemed irretrievably stuck (as it goes with scripting).

## Reference

Citation info: Boeing, G. 2017. "OSMnx: New Methods for Acquiring, Constructing, Analyzing, and Visualizing Complex Street Networks." Computers, Environment and Urban Systems 65, 126-139. doi:10.1016/j.compenvurbsys.2017.05.004
