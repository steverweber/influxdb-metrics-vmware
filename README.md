Installing
=============

Drop this file onto a server that has access to vmware powershell tools.


If using telegraf exec
----------------------
requires telegraf >= v1.2 with patch (https://github.com/influxdata/telegraf/commit/4886109d9caab081f64b46e7c87d50824f4ead6b)
``` 
[agent]
    # make large because vmware powershell script can fill a small buffer passed limit
    metric_buffer_limit = 10000

# Assumes the execution policy is unrestricted. Use the -ExecutionPolicy ByPass option if required
[[inputs.exec]]
    commands = [
        '"C:\windows\system32\WindowsPowerShell\v1.0\powershell.exe" -File "C:\Program Files\Telegraf\vmware_collect_stats.ps1"',
    ]
    data_format = "influx"
    timeout = "25m"
    interval = "30m"
```


If using a windows task
-----------------------

setup a windows task to run the powershell program every ~30min

```
schtasks /create /sc minute /mo 30 /tn "metrics-vmware" /tr "\"c:\metrics-vmware.ps" \"http://127.0.0.1:8086/write?db=vmware&u=user&p=password&precision=s\""
```
