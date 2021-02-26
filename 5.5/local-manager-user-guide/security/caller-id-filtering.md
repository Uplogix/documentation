<!-- 5.4 -->

By default, the modem refuses all incoming calls. Dial-in capability must be enabled from the command line before use. Use the **config answer** command to specify phone numbers from which the modem will accept calls.

If Caller ID is available, you can allow or deny calls from specific phone numbers. Prefix masking can be used, which allows the following:

- permit or deny all of a given area code, such as 512
- permit or deny numbers beginning with a given string, such as 512555
- permit or deny specific numbers such as 5125551212

```
[config answer]# deny 512
[config answer]# allow 512555
[config answer]# deny 5125551212
```

> You may need to configure the modem initialization string to turn on caller ID delivery.

> Do not use dashes or dots between numbers.

To remove previously configured behavior, the **no** modifier can be used with most commands.

```
[config answer]# no deny 5125551212
```

The Local Manager relies on Caller ID information to identify incoming calls. If Caller ID is not available, use the **allow all** subcommand to override the default deny.

```
[config answer]# allow all
```