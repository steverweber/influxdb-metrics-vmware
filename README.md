Installing
=============

Drop this file onto a server that has access to vmware powershell tools.


If using telegraf exec
----------------------
untested
``` 
[[inputs.exec]]
  # Shell/commands array
  commands = ["c:\metrics-vmware.ps"]
  data_format = "influx"
  interval = "30m"
```


If using a windows task
-----------------------

setup a windows task to run the powershell program every ~30min

```
schtasks /create /sc minute /mo 30 /tn "metrics-vmware" /tr "\"c:\metrics-vmware.ps" \"http://127.0.0.1:8086/write?db=vmware\""
```
