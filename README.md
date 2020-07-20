# Blacklist
This repository contains a PHP application that allows users to scan multiple blacklist with an IP or FQDN. A shell script is also provided for cron automation with support for smtp reporting.

## PHP Application
Simply clone the repository onto a LAMP/WAMP server and enjoy!

## Shell
Shell script supports any distribution as long as the packages dig and s-nail are installed.
On debian based distribution, the script will attempt to install them if they are missing during the first use.
```bash
Usage: ./blacklist [options] IP/FQDN

Options:

-v                     => Enable Debug Mode
                          Input commands sent are stored in 
-e                     => Compile errors and warnings after execution 
-s                     => Send report via email
-f                     => Disable all formatting
```

## Configuration
### Blacklists
Blacklists can be updated in the list.json file.
### Settings
SMTP and other settings can be updated in the settings.json file.
SMTP settings are required if you want to send the report via email.

## Tutorial
A tutorial to setup a cron will come later.

## Enjoy!

