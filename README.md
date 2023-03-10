# GTFS to Nodes and Edges in a daterange
Parses GTFS files and generates appropriate routes information for each dates in a range


## To Run
The base workbook "gtfs_process_workspace.ipynb" can be run fully. The ./utils/ python code will handle the download & processing of files.

If one prefers to use the notebooks intead they can be found under ./_ipynb_notebooks_moved_From_base/. They will need to be placed back into the parent folder in them to run properly.

## Logic
The point of the program is to compile total number of station stops in a node-and-edge method.

In order to limit the scope of data extrapolation, the data will be organized as follows

1) Total number of node and edges in context of directional Station-To-Station data parsed per trip_id
    a) Requires Stop-To-Stop analysis via stop_times.txt (from & to & transit_duration (weight) info via trip_id)
    b) Requires Stop-To-Parent_Stop analysis via stops.txt (parent stop)
    c) Requires Parent_Stop-To-Station analysis via transfers.txt (clustered parent stops)

2) When each directional edge & their weights are calculated per each trip_id, a mapping can consolidate all trip node and edges

3) From the mapping tables I should be able to calculate the station-to-station, total count, and transit duration for every day

4) From the daily data, I can query data for sum based on each node-edge or else I can generate a table that displays total stops per date

## Example output text
### ./results/networkx_analysis.csv
station,degrees,closeness,betweenness\
101,0.004866180048661801,0.052557544757033246,0.0\
103,0.009732360097323601,0.055465587044534415,0.004866180048661801\
104,0.009732360097323601,0.05869751499571551,0.009708622633671593\
106,0.009732360097323601,0.062310491206791996,0.014527327755029377\
107,0.009732360097323601,0.06637596899224807,0.01932229541273515\
108,0.009732360097323601,0.07098445595854923,0.024093525606788915\
109,0.009732360097323601,0.07625231910946197,0.02884101833719067\
110,0.009732360097323601,0.08233173076923077,0.03356477360394042

### ./results/aggregated_daily.csv
date,total_stops\
20200101,136532\
20200102,216241\
20200103,216241\
20200104,149635\
20200105,136532\
20200106,216241\
20200107,216241\
20200108,216241\
20200109,432482
