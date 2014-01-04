

Before you run this script, you'll need R and you'll need to run a few commands from the command shell and in R. First, clone this repository. Then open a command shell in this directory and extract some lines from /var/log/syslog:

```bash
sudo cat /var/log/syslog        | grep wpa_supplicant >  wpa_log.txt
sudo cat /var/log/syslog.1      | grep wpa_supplicant >> wpa_log.txt
sudo zcat /var/log/syslog.*.gz  | grep wpa_supplicant >> wpa_log.txt
```


Then, in R:

```
# Make sure ggplot2 (and plyr) are installed
if (!require('ggplot2')) install.packages('ggplot2')

# Run the script
source('wifi.R')
```

At the end, you should have a couple CSV and PNG files of the processed data in your directory.


## Notes
This script scans the syslog for three different types of events, which I categorized like so:

  * success: when text is `CTRL-EVENT-CONNECTED - Connection to e0:1c:41:1e:8b:a8
completed (auth)`
  * disconnect: when text is `CTRL-EVENT-DISCONNECTED bssid=e0:1c:41:1e:8a:e8 reason=4`
  * timeout: when text is `Authentication with e0:1c:41:1e:8b:e8 timed out.`

There are a couple other little details, and there may well be other types of events that I didn't find, but this seems to cover most cases.
