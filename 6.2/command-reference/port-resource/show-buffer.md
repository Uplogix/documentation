<!-- 5.4 -->

Displays buffer data from the modem or device. This can be helpful in debugging device issues. Data is stored in a 1 MB **current** buffer; when this buffer fills, it is renamed **previous** and a new **current** buffer is created.  A timestamp is added to the log when more than 5 minutes has occurred between entries. The buffers are memory-resident and reset when the Uplogix is restarted.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: All

Modem: All

Power controllers: All

Uplogix system: All

LMS offerings: All

# Syntax

```
show buffer [-raw | -previous]
```

The command **show buffer** displays the most recent 1 MB of data. Use the optional **-previous** parameter to view the previous buffer. 

Use the optional **-raw** parameter to display the buffer contents without additional formatting.

You may wish to redirect the output of this command to a file copied to an external system.

```
show buffer [| <scp | ftp | mailto>  username@host:/filepath/ ]
```

# Usage

```
[admin@UplogixLM (port1/1)]# show buffer
------------------------------------------------------------
> ==== Began Wed Mar 21 10:38:52 UTC 2017 ====
> 3/19/2017-20:25:15.433 -10- CT3 CONFIG ICSLOT TE1[5] timeslotMap changed
>
> 3/19/2017-20:25:15.333 -10- CT3 CONFIG ICSLOT TE1[4] timeslotMap changed
>
> 3/19/2017-20:25:15.299 -10- CT3 CONFIG ICSLOT TE1[3] timeslotMap changed
>
> 3/19/2017-20:25:15.199 -10- CT3 STATUS ICSLOT TE1[28] lineStatus : RAIS (end)
>
> 3/19/2017-20:25:15. 83 -10- CT3 STATUS ICSLOT TE1[27] lineStatus : RAIS (end)
>
> 3/19/2017-20:25:14.983 -10- CT3 STATUS ICSLOT TE1[26] lineStatus : RAIS (end)
>
> 3/19/2017-20:25:14.883 -10- CT3 STATUS ICSLOT TE1[25] lineStatus : RAIS (end)
>
> 3/19/2017-20:25:14.799 -10- CT3 STATUS ICSLOT TE1[24] lineStatus : RAIS (end)
>
---Press 'q' to quit, any other key to continue--- [1/971]
```
# History

3.1 - This command was introduced.

3.2 - The -previous option was added.

# Related Commands
--
