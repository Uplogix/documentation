<!-- 5.4 -->

Removes a job or monitor from the schedule.

# Command availability 

CLI resource: system, port, modem

Device makes: All

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config removejob <"jobID" | -all>
```

The -all option removes all jobs and monitors on the device.

# Usage 

Use show schedules or show monitors to determine the job number before removing it.

```
[admin@UplogixLM (port1/1)]# config removejob 14
Job 14 has been removed from the scheduler queue.
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment on which this job is scheduled

# History 

--

# Related commands 

- **show schedules**
- **show monitors**
