# dstat-monitor

Script that uses dstat to aggretate relevant resource statistcs, write them 
to a CSV file and format this file to be directly imported by R scripts.

## Usage

	Usage: dmon [options] command [logfile [duration]]

	Commands:
	dmon start logfile [duration]   Start monitor
	dmon status                     	Verify monitor status
	dmon stop                           Stop monitor
	dmon parse logfile              Convert log file to a R-friendly format
	dmon run						runs the kmeans job, dmon -f start or running flink required
	dmon kmeans  						Start flink, start monitor, run kmeans job, stop monitor, stop flink
	
	Options:
	 -i, --interval INTERVAL Specify monitoring interval in seconds (default: 1)
	 -v, --verbose           Make the operation more talkative
	 -h, --help              Print this help message
	 -f, --flink 			 start/stop flink and run the kmeans job along with monitor

## Example


Start monitor:

	dmon start output.txt

Stop monitor:

	dmon stop

Parse output file:

	dmon parse output.txt

## Flink and kmeans

Requires flink >= 0.7

Replace $FLINK in line 18 of dmon with path to your flink directory including the flink homedirectory, e.g. /home/user/flink-0.9.0

Run everything:
	
	dmon kmeans output.txt

	Flink will be started, the monitor will be started, the kmeans example input data generated and the kmeans job submitted to flink. Afterwards flink and the monitor will be stopped.

Step-by-step:

	dmon -f start output.txt
	dmon run
	dmon -f stop