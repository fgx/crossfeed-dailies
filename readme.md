Crossfeed Dailies Read Me
===

This is an effort to gather some statistical information about [FlightGear](http://www.flightgear.org/) [MultiPlayer](http://wiki.flightgear.org/Howto:Multiplayer) [Server](http://wiki.flightgear.org/FlightGear_Multiplayer_Server) usage, through sampling the [json](http://crossfeed.freeflightsim.org/flights.json) feed from a [crossfeed](https://gitlab.com/fgtools/crossfeed) client, connected to server `mpserver#14`...

At present this is achieved by running a perl script, [cfjsonlog.pl](https://github.com/geoffmcl/scripts/blob/master/cfjsonlog.pl) 24/7, sampling the `crossfeed` json each 5 seconds, some filtering for movement and time, but each flight is written to a daily csv file.

The CSV header line is -

````
fid,callsign,lat,lon,alt_ft,model,spd_kts,hdg,dist_nm,update,tot_secs
````

where the `fid` is a unique flight ID issued by crossfeed. 

The CSV records need to be thought of as a json blocks of flights, sampled each 5 seconds, thus each daily CSV will contain 17,280 such blocks of flights. The block can be separated on the value of the `update`, the UTC date/time that the json crossfeed sample was taken.

The size of each json block will depend on the number of `multiplayer` flights, visible to `crossfeed` at that time. At any moment this could be zero, but to date the lowest value seen was 3... so far the maximum has been up to 54 active flights. So the number of active flights per block times 17,280 means each CSV daily file will contain 300 to 400 thousand records, a total of 25 to 40 MB per file.

The daily CSV files are presently manually copied to this repo.

With a little effort this presently rather manual process could be auotmated...

### Summary of Data ###

In an attempt to make this mass of data collected more meaningful, the CSV daily logs can be processed with a WIP perl script, [cfcsvlogs.pl](https://github.com/geoffmcl/scripts/blob/master/cfcsvlogs.pl), which outputs a crude HTML summary.

Presently, this WIP script, can summarize one file, or a group of csv daily log files in a directory... and generate HTML like [flights-2016-07-30.htm](http://htmlpreview.github.io/?https://github.com/fgx/crossfeed-dailies/blob/gh-pages/html/flights-2016-07-30.htm), for 1, or [20160806.htm](http://htmlpreview.github.io/?https://github.com/fgx/crossfeed-dailies/blob/gh-pages/html/20160806.htm) for a group of file...

While the above will always work, gh-page has it own (minimal) web server, and you can use - https://fgx.github.io/crossfeed-dailies/ - where there is now a beginning index page, leading to most other pages available... this will develop, over time...

**WARNING:** The times and distance flown can be greatly influenced by sim time warping, and sim time speed up and slow down, so are always only estimates! And this is only the results of one particular, specific crossfeed. That is, no prizes will be awarded on these results. ;=)) And as such, also should not be taken as an general indication of FlightGear usage, and is just a sub-set of MultiPlayer usage.

Enjoy...

; eof - 20160806
