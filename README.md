# Blacklist
This repository contains a PHP application that allows users to scan multiple blacklist with an IP or FQDN. A shell script is also provided for cron automation with support for smtp reporting.

I saw a similar shell script at https://github.com/adionditsak/blacklist-check-unix-linux-utility and wanted to add reporting to it. I ended up rewriting the script entirely to my flavor. So I could also use the same settings and lists in a PHP version of the shell. This way I was able to provide support for any type of devices for a quick check by using a web server.

Why should I use something like this? If you have a web server or just a mail server, you may want to monitor if the public IP of the server ever gets blocked on a public listing. Since a lot of mail servers uses those public listing. It is quite usefull to monitor if your server ever gets blocked. This facilitates investigations related to undeliverable emails.

## Changelog
 * [2021-07-23] => Added support for brew
 * [2020-07-20] => Renamed debug mode to reporting mode. Kept the same switch (-v)
 * [2020-07-20] => Updated README.MD File
 * [2020-07-20] => Fix an issue with a unary operator in shell when executing without the debug switch.

## Installation
```bash
git clone https://github.com/LouisOuellet/blacklist.git
```

## Configuration
### Blacklists
Blacklists can be updated in the list.json file using your favorite editor.
### Settings
Create a settings.json file with your favorite editor. This is required for email reporting.
#### Sample
```json
{
    "smtp":{
        "host": "smtp.domain.com",
        "port": "465",
        "username": "smtp@domain.com",
        "password": "password"
    },
    "send":{
        "name": "Monitoring",
        "from": "monitoring@domain.com",
        "to": "mailinglist@domain.com"
    },
    "logs":{
        "directory": "/tmp/"
    }
}
```

## Tutorial
A tutorial to setup a cron will come later.

## PHP Application
Simply clone the repository onto a web server that supports PHP and enjoy!

## Shell
Shell script supports any distribution as long as the packages jq and s-nail are installed.
On debian based distribution, the script will attempt to install them if they are missing during the first use.
### Usage
```bash
Usage: ./blacklist [options] IP/FQDN

Options:

-v                     => Enable Reporting Mode
                          Input commands sent are stored in [log file]
-e                     => Compile errors and warnings after execution
-s                     => Send report via email
-f                     => Disable all formatting
```
### Sample
```bash
$ ./blacklist -vesf 8.8.8.8
[i][2020-07-20 09:54:44][START] pkg jq
[i][2020-07-20 09:54:44][START] pkg s-nail
8.8.8.8 name dns.google.
[✓][2020-07-20 09:54:44][ RUN ] dig +short -t a 8.8.8.8.0spam.fusionzero.com =>
[✓][2020-07-20 09:54:44][ RUN ] dig +short -t a 8.8.8.8.access.redhawk.org =>
[✗][2020-07-20 09:54:44][ RUN ] dig +short -t a 8.8.8.8.all.s5h.net => 127.0.0.2
[✓][2020-07-20 09:54:45][ RUN ] dig +short -t a 8.8.8.8.all.spamrats.com =>
[✓][2020-07-20 09:54:45][ RUN ] dig +short -t a 8.8.8.8.aspews.ext.sorbs.net =>
[!][2020-07-20 09:55:00][ RUN ] dig +short -t a 8.8.8.8.babl.rbl.webiron.net => ;; connection timed out; no servers could be reached
[✓][2020-07-20 09:55:00][ RUN ] dig +short -t a 8.8.8.8.backscatter.spameatingmonkey.net =>
[✓][2020-07-20 09:55:00][ RUN ] dig +short -t a 8.8.8.8.b.barracudacentral.org =>
[✓][2020-07-20 09:55:00][ RUN ] dig +short -t a 8.8.8.8.bb.barracudacentral.org =>
[✓][2020-07-20 09:55:01][ RUN ] dig +short -t a 8.8.8.8.black.junkemailfilter.com =>
[✓][2020-07-20 09:55:02][ RUN ] dig +short -t a 8.8.8.8.bl.blocklist.de =>
[✓][2020-07-20 09:55:02][ RUN ] dig +short -t a 8.8.8.8.bl.drmx.org =>
[✓][2020-07-20 09:55:02][ RUN ] dig +short -t a 8.8.8.8.bl.konstant.no =>
[✓][2020-07-20 09:55:02][ RUN ] dig +short -t a 8.8.8.8.bl.mailspike.net =>
[✓][2020-07-20 09:55:02][ RUN ] dig +short -t a 8.8.8.8.bl.nosolicitado.org =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.block.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.rbl.scrolloutf1.com =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.scientificspam.net =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.score.senderscore.com =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.spamcop.net =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.spameatingmonkey.net =>
[✓][2020-07-20 09:55:03][ RUN ] dig +short -t a 8.8.8.8.bl.suomispam.net =>
[✓][2020-07-20 09:55:05][ RUN ] dig +short -t a 8.8.8.8.bsb.empty.us =>
[✓][2020-07-20 09:55:06][ RUN ] dig +short -t a 8.8.8.8.cart00ney.surriel.com =>
[✓][2020-07-20 09:55:06][ RUN ] dig +short -t a 8.8.8.8.cbl.abuseat.org =>
[✓][2020-07-20 09:55:07][ RUN ] dig +short -t a 8.8.8.8.cbl.anti-spam.org.cn =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.cblless.anti-spam.org.cn =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.cblplus.anti-spam.org.cn =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.cdl.anti-spam.org.cn =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.combined.rbl.msrbl.net =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.db.wpbl.info =>
[✓][2020-07-20 09:55:08][ RUN ] dig +short -t a 8.8.8.8.dnsbl-1.uceprotect.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl-2.uceprotect.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl-3.uceprotect.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.cobion.com =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.dronebl.org =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.justspam.org =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.kempt.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.net.ua =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.rv-soft.info =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.rymsho.ru =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.spfbl.net =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.tornevall.org =>
[✓][2020-07-20 09:55:09][ RUN ] dig +short -t a 8.8.8.8.dnsbl.zapbl.net =>
[✓][2020-07-20 09:55:14][ RUN ] dig +short -t a 8.8.8.8.dnsrbl.org =>
[✓][2020-07-20 09:55:14][ RUN ] dig +short -t a 8.8.8.8.dnsrbl.swinog.ch =>
[✓][2020-07-20 09:55:15][ RUN ] dig +short -t a 8.8.8.8.dul.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:15][ RUN ] dig +short -t a 8.8.8.8.dyna.spamrats.com =>
[✓][2020-07-20 09:55:16][ RUN ] dig +short -t a 8.8.8.8.dyn.nszones.com =>
[✓][2020-07-20 09:55:16][ RUN ] dig +short -t a 8.8.8.8.escalations.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:16][ RUN ] dig +short -t a 8.8.8.8.fnrbl.fast.net =>
[✓][2020-07-20 09:55:16][ RUN ] dig +short -t a 8.8.8.8.hostkarma.junkemailfilter.com =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.http.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.images.rbl.msrbl.net =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.invaluement =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.ips.backscatterer.org =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.ix.dnsbl.manitu.net =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.l1.bbfh.ext.sorbs.net =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.l2.bbfh.ext.sorbs.net =>
[✓][2020-07-20 09:55:18][ RUN ] dig +short -t a 8.8.8.8.l4.bbfh.ext.sorbs.net =>
[✓][2020-07-20 09:55:19][ RUN ] dig +short -t a 8.8.8.8.list.bbfh.org =>
[✓][2020-07-20 09:55:19][ RUN ] dig +short -t a 8.8.8.8.mail-abuse.blacklist.jippg.org =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.misc.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.multi.surbl.org =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.netscan.rbl.blockedservers.com =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.new.spam.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.noptr.spamrats.com =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.old.spam.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:20][ RUN ] dig +short -t a 8.8.8.8.pbl.spamhaus.org =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.phishing.rbl.msrbl.net =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.pofon.foobar.hu =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.problems.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.proxies.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.psbl.surriel.com =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl2.triumf.ca =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.abuse.ro =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.blockedservers.com =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.dns-servicios.com =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.efnet.org =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.efnetrbl.org =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.interserver.net =>
[✓][2020-07-20 09:55:21][ RUN ] dig +short -t a 8.8.8.8.rbl.realtimeblacklist.com =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.recent.spam.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.relays.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.rep.mailspike.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.safe.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.sbl.spamhaus.org =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.smtp.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.socks.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.dnsbl.anonmails.de =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spamlist.or.kr =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.pedantic.org =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.rbl.blockedservers.com =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spamrbl.imp.ch =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.rbl.msrbl.net =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spamsources.fabel.dk =>
[✓][2020-07-20 09:55:22][ RUN ] dig +short -t a 8.8.8.8.spam.spamrats.com =>
[✓][2020-07-20 09:55:28][ RUN ] dig +short -t a 8.8.8.8.srn.surgate.net =>
[!][2020-07-20 09:55:43][ RUN ] dig +short -t a 8.8.8.8.stabl.rbl.webiron.net => ;; connection timed out; no servers could be reached
[✓][2020-07-20 09:55:44][ RUN ] dig +short -t a 8.8.8.8.st.technovision.dk =>
[✓][2020-07-20 09:55:44][ RUN ] dig +short -t a 8.8.8.8.talosintelligence.com =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.torexit.dan.me.uk =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.truncate.gbudb.net =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.ubl.unsubscore.com =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.virus.rbl.msrbl.net =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.web.dnsbl.sorbs.net =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.web.rbl.msrbl.net =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.xbl.spamhaus.org =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.zen.spamhaus.org =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.z.mailspike.net =>
[✓][2020-07-20 09:55:45][ RUN ] dig +short -t a 8.8.8.8.zombie.dnsbl.sorbs.net =>
[i][2020-07-20 09:55:45][     ] #############################################################
[i][2020-07-20 09:55:45][ VAR ] log file.......: /tmp/1595253284462648046.log
[i][2020-07-20 09:55:45][ VAR ] 1 minutes and 1 seconds elapsed.
[i][2020-07-20 09:55:45][     ] #############################################################
[i][2020-07-20 09:55:45][START] exec echo "Blacklist Scan of 8.8.8.8 was completed. See attached report." | s-nail -s "IP/FQDN: 8.8.8.8" -S smtp-use-ssl -S ssl-rand-file=/tmp/mail.entropy -S smtp-auth=login -S smtp="smtps://smtp.domain.com:465" -S from="monitoring@domain.com(Monitoring)" -S smtp-auth-user="smtp@domain.com" -S smtp-auth-password="password" -S ssl-verify=ignore -a "/tmp/1595253284462648046.log" maillist@domain.com
[✓][2020-07-20 09:55:46][ RUN ] echo "Blacklist Scan of 8.8.8.8 was completed. See attached report." | s-nail -s "IP/FQDN: 8.8.8.8" -S smtp-use-ssl -S ssl-rand-file=/tmp/mail.entropy -S smtp-auth=login -S smtp="smtps://smtp.domain.com:465" -S from="monitoring@domain.com(Monitoring)" -S smtp-auth-user="smtp@domain.com" -S smtp-auth-password="password" -S ssl-verify=ignore -a "/tmp/1595253284462648046.log" maillist@domain.com
[✗][2020-07-20 09:54:44][ RUN ] dig +short -t a 8.8.8.8.all.s5h.net => 127.0.0.2
[!][2020-07-20 09:55:00][ RUN ] dig +short -t a 8.8.8.8.babl.rbl.webiron.net => ;; connection timed out; no servers could be reached
[!][2020-07-20 09:55:43][ RUN ] dig +short -t a 8.8.8.8.stabl.rbl.webiron.net => ;; connection timed out; no servers could be reached
```

## Enjoy!
