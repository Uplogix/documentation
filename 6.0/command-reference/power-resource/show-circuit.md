<!-- 5.4 -->

Displays status and amp draw for the specified circuit of an APC power controller.

# Command availability

CLI resource: powercontrol

Uplogix system: All

LMS offerings: All

#Syntax 

```
show circuit <circuit> [-n <"number">]
```

**circuit** is the circuit for which you wish to display information. You may use a wildcard character * to display all circuit information.

**number** is the maximum number of messages to display.

# Usage 

```
[admin@UplogixLM (powercontrol)]# show circuit *
circuit     amps     status     time
-------     ----     ------     ----------------
1           0.0      OK         Aug 07 18:28 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:31 UTC
-------     ----     ------     ----------------
2           0.0      OK         Aug 07 18:28 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:31 UTC
-------     ----     ------     ----------------
3           0.0      OK         Aug 07 18:28 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:29 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:30 UTC
            0.0      OK         Aug 07 18:31 UTC
```
# History 

3.5 - This command was introduced.

# Related commands 
--
