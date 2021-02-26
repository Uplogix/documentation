<!-- 5.4 -->

This ruleset monitors the iDirect for various states, such as TX mute, RX lock, acquisition status, and others, and reports them as alarms or events as appropriate.

The iDirectBasic ruleset is to be scheduled as a remotestate monitor on the iDirect.

```
config ruleset iDirectNative 
description null 
rules 
iDirectTxMute, iDirectLinkLayerInDataTransfer, iDirectModemInAcquisition, iDirectModemDetected, iDirectTxerStateOn, iDirectModemInNetwork, iDirectRXLocked, iDirectRXUnlocked 
exit 
exit 
```

The following are the rules that are part of the ruleset.

```

config rule iDirectTxMute 
action writeStatus "TX MUTE" 
action alarm GENERIC -a "TX MUTE" 
conditions 
remotestate.transmitterMute equals true 
exit 
exit 

config rule iDirectLinkLayerInDataTransfer 
action writeStatus "In Data Transfer" 
conditions 
remotestate.linkLayerState matches "In Data Transfer" 
exit 
exit 

config rule iDirectModemDetected 
action writeStatus "Modem State Detected" 
action alarm GENERIC -a "DEVICE_MODEM_STATE_DETECTED" 
conditions 
remotestate.modemState matches "Detected" 
exit 
exit 

config rule iDirectModemInAcquisition 
action writeStatus "In Acquisition" 
action alarm GENERIC -a "DEVICE_IN_NETWORK_ACQUISITION" 
conditions 
remotestate.modemState matches "In Acquisition" 
exit 
exit 

config rule iDirectModemInNetwork 
action writeStatus "In Network w/o Data" 
action alarm GENERIC -a "DEVICE_IN_NETWORK_NO_DATA" 
conditions 
remotestate.modemState matches "In Network" 
exit 
exit 

config rule iDirectRXLocked 
action writeStatus "Receive Locked" 
action alarm GENERIC -a "RX Locked" 
conditions 
remotestate.receiverLock matches "LOCKED" 
exit 
exit 

config rule iDirectRXUnlocked 
action writeStatus "Receive Unlocked" 
action alarm GENERIC -a "RX unlocked" 
conditions 
remotestate.receiverLock matches "UNLOCKED" 
exit 
exit 

config rule iDirectTxerStateOn 
action writeStatus "Transmit State On" 
action alarm GENERIC -a "TX State ON" 
conditions 
remotestate.transmitterState matches ON 
exit 
exit
```