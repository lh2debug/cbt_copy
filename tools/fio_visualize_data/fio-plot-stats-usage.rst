====================
Visualize Fio Output
====================

Motivation
==========

Fio generates quite a bit of output that is sometimes hard to decipher
and understand. This problem is exacerbated further if one is running
multiple tests with different ceph options to tune ceph performance.
It would be good to have a tool that decodes the data from the log files
created by Fio and generate meaningful graphs that provide insight into
ceph performance.

The attempt here is to start with some basic scripts that parse Fio
output and generate plots like average client latencies and completion
latency percentiles.

Going further the idea is to enhance the scripts to generate more meaningful
graphs, tighter integration with cbt to generate graphs via yaml
specification as part of the test itself.

Usage
=====
.. code-block:: console


    $ ./fio-plot-stats.py -h
    usage: fio-plot-stats.py [-h] -f {json,csv} -s SRCDIR -d DESTDIR -o
                             {read,write} -m {bw,lat,pct} [-i {pdf,png}]
                             [-n FILENAME] [-r TIMERANGE TIMERANGE] [-p]

    Generate plots from fio output

    optional arguments:
      -h, --help            show this help message and exit
      -f {json,csv}, --filetype {json,csv}
                            type of file to parse
      -s SRCDIR, --source SRCDIR
                            source directory containing fio output files
      -d DESTDIR, --destination DESTDIR
                            destination directory to save generated plots
      -o {read,write}, --optype {read,write}
                            plot read or write stats
      -m {bw,lat,pct}, --metric {bw,lat,pct}
                            metric to analyze/plot
      -i {pdf,png}, --imgformat {pdf,png}
                            plot image format
      -n FILENAME, --filename FILENAME
                            source file containing CSV data to analyze/plot
      -r TIMERANGE TIMERANGE, --timerange TIMERANGE TIMERANGE
                            time range to plot/calculate stats for CSV data
      -p, --subplot         create a subplot with provided timerange

Working Details
===============
The input file format option ``-f/--filetype`` is mandatory. Depending on
this, additonal options if preferred may be provided to override the default
behavior.  For JSON file type, the tool scans for the files in the source
directory and generates graphs. For CSV file type, an additional
parameter called ``-n/--filename`` needs to be specified.

The option ``-o/--optype`` tells the script to scan read or write statistcs in
the Fio files and generate the graphs.

An additional artifact (apart from charts) of parsing JSON data is a
CSV file containing the stats from the parsed files.

NOTE: All fio files in the source directory having 'json' string in filename are
treated as JSON files and are scanned automatically. Therefore, it is important
to have 'json' string in the filename if JSON data is required to be visualized.

Examples
========
**Example 1**

The following commands scan the source directory for files having
string 'json' in the filenames and parses specfied stats (lat, bw or pct)
from the files to generate comparison graphs in the destination folder:

.. code-block:: console

    $python3 fio-plot-stats.py -s ~/cbt_logs/json_logs -f json -o write -d ~/cbt_logs/json_logs -m lat
    $python3 fio-plot-stats.py -s ~/cbt_logs/json_logs -f json -o write -d ~/cbt_logs/json_logs -m bw
    $python3 fio-plot-stats.py -s ~/cbt_logs/json_logs -f json -o write -d ~/cbt_logs/json_logs -m pct

**Example 2**

The following command uses the specified CSV file containing write latency
stats generated by fio and generates a chart of latency distribution across
the entire duration of the test:

.. code-block:: console

    $python3 fio-plot-stats.py -f csv -s ~/cbt_logs -d ~/cbt_logs -o write -n wpq_clat_Run7 -m lat

**Example 3**

The following command is similar to Example 2, except that additionally a
subplot is generated in the same chart showing the latency distribution
in the specified time range:

.. code-block:: console

    $python3 fio-plot-stats.py -f csv -s ~/cbt_logs -d ~/cbt_logs -o write -n wpq_clat_Run7 -m lat -r 0 160 -p

Note that if the '-p/--subplot' option is not specified in example 3, a
chart with a single graph is generated for the time range specified.

Plots may be generated for 'bandwidth' metric by specifying 'bw' for the
'-m' parameter in the above examples.

Additionally, percentile data and charts may be generated by specifying 'pct'
for the '-m' parameter. The raw clat latency data captured by fio must be
provided as an input using the '-n' option. This uses pandas and numpy module
to generate percentile table and charts for the average, 50th, 95th, 99th and
99.5th percentiles. Given a time range, samples are analyzed for each second in
between and the above percentiles are saved into a new pandas dataframe. A csv
file is generated in addition to the chart for the time range specified.

NOTE: Logging the histogram data generated by fio and running the analysis on
it would provide more accurate information about percentile distribution.
Please see fio source repository for more information on this.
