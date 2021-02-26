<!-- 5.4 -->

Jobs are discrete tasks that the Local Manager uses to collect information about the device it is managing. Jobs can include the collection of device info or the pull or push of a configuration or OS. Many jobs on the Local Manager are scheduled automatically during the initial **config init** process, but it is also possible to schedule additional jobs at any time.

# Schedule a Job 

To schedule a job, use the **config schedule** command:

```
config schedule <crontab> <job [job args]>
```

Command parameter definitions: 

 - **Crontab**: Set the timing of when the job will run. The job can run once, run at a specific time and repeat with a delay, or run during an interval of time. The following formats are used: 
  - **One time**: Schedule a job to run one time with the â€“o flag: <-o execution time>
  - **Cron schedule**: Schedule a job to run at a specific time and repeat at a specific interval. Define the start time and interval time with the following flags: <[-m 0-59] [-h 0-23] [-D 1-31] [-M 1-12] [-W 0-6]> [-d delay]
  - **Interval schedule**: Schedule a job to run during a period of time with a specific delay between repetitions. Define the interval and delay with the following flags: [-s startTime] [-e endTime] <-d delay>
All times are MM/dd/yy-HH&#58;mm:ss format
-M <month>		month range (1 - 12)
-h <hour>		hour range (0 - 23)
-D <day>			day range (1 - 31)
-m <minute>		minute range (0 - 59)
-W <week>		week day (0 - 6)
-d <delay>		delay between 2 consecutive executions of the job in seconds
-e <end time>		end time after which the job is removed from the scheduler
-o <one time>		the one time at which the job should run
-s <start time>	start time for the job
 - **job** [job args]: The job the Local Manager will run on the defined schedule. Jobs available for use with this command include:
  - **clearCounters**: Clears all interface counters
  - **clearServiceModule**: Clears service module
  - **deviceInfo**: Collects Serial#/Make/Model/OS information
  - **interfaceCycle**: Cycles the interface specified
  - **interfaceOff**: Turns off the interface specified
  - **interfaceOn**: Turns on the interface specified
  - **powerCycle**: Cycle device power
  - **powerOff**: Turn device power off
  - **powerOn**: Turn device power on
  - **pullOS**: Copies an OS image from the device
  - **pullRunningConfig**: Pull a running config from a device
  - **pullSftp**: Pull a file using SFTP/SCP
  - **pullStartupConfig**: Pull a startup config from a device
  - **pullTftp**: Pull a file using TFTP
  - **pullVlanConfig**: Pull a VLAN database from a device
  - **pushOS**: Push an OS Image to a device
  - **pushRunningConfig**: Push a running config to a device
  - **pushSftp**: Push a file using SFTP/SCP
  - **pushStartupConfig**: Push a startup config to a device
  - **pushTftp**: Push a file using TFTP
  - **reboot**: Reboot the device connected to this port
  - **showTech**: Retrieve tech-support info from a device

**Schedule Job Examples**

Here are some examples of job schedules:

| Command | Execution |
|:---|:---|
|config schedule -s 01/03/14-10&#58;30:00 -e 02/03/14-10&#58;29:59 -d 30 deviceInfo|Executes the deviceInfo job every 30 seconds between Jan 3 and Feb 3, 2014|
|config schedule -o 01/03/14-10&#58;30:00 deviceInfo|Executes the deviceInfo job once on Jan 3, 2014|
|config schedule -M 3 -m 30 deviceInfo|Executes the deviceInfo job every half hour in March|

Issue the **show schedule** command at the managed device port to see the scheduled job.

```
[admin@UplogixLM (port1/1)]# show schedule
Listing currently scheduled jobs for device: port1/1  All times shown in UTC.
6: [Interval: 03:00:00 Mask: * * * * *] pullRunningConfig
8: [Interval: 336:00:00 Mask: * * * * *] pullOS
3: [Interval: 00:05:00 Mask: * * * * *] deviceInfo
```

# Delete a Scheduled Job

Use the **show schedule** and **config removejob {job ID}** commands to find the scheduled job number and then remove that job from port. Note that the pullOS job number in the **show schedule** example above is job 3. To delete this scheduled job from the Local Manager port, issue the following command:

```
[admin@UplogixLM (port1/1)]# config removejob 3
Job 3 has been removed from the scheduler queue.
```

# Schedule a Monitor

A monitor is a set of instructions to collect data at regular intervals. The Local Manager can collect certain data from any supported device. The available data depends on the device. 

By default, monitors run every 30 seconds. When you create a monitor, you can specify how frequently the monitor runs. Many monitors may be scheduled automatically during the config init process. Monitors may include rules that specify how to evaluate the collected data. Rules give the monitor the ability to respond to changes or trends.

To schedule a monitor, use the **config monitor** command. 

```
config monitor <monitor> <ruleList> <:[delay seconds>
```

Command Parameters: 

 - **monitor**: The type of monitor. Options include: chassis, consoleLog, interface, ping or terminal
 - **rulelist**: The list of rules or rulesets that define when to alarm and what actions to take based on the data collected. The list of rules and rulesets are separated by a comma or bar. 
 - **delay**: Delay time in seconds between monitor executions.

Schedule Monitor Examples

Here are some examples of simple monitor schedules:

| Monitor | Execution | 
|:---|:---|
|config monitor interface Ethernet0/0 interfaceBasic :30|Schedules an interface monitor on Ethernet 0/0 applying the interfaceBasic ruleset with a delay of 30 seconds.|
|config monitor ping 203.0.113.225 OOB-ping 30|	Schedules a monitor to ping 203.0.113.225 applying the OOB-ping rule with a delay of 30 seconds.|
|config monitor chassis :30|	Schedules a chassis monitor with a delay of 30 seconds.|