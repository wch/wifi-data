

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
