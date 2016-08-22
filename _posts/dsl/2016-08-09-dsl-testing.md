---
layout:     post
title:      "DSL Testing (2016-08-09)"
date:       2016-08-09 15:00:00 +1200
categories: dsl
published:  true
---

## Pre-incident information
* Last [SpeedTest](http://www.speedtest.net/my-result/5461434787) before incident (2016-07-08 - approx one month previous)
* Last sync recording (2016-01-24) - after installation
  * ADSL Sync Type: ADSL2+
  * Sync Rates:
    * Upstream: 1328 Kbps
    * Downstream: 19848 Kbps
  * SNR Margin (dB):
    * Upstream: 8.3
    * Downstream: 6
  * Line Attenuation (dB):
    * Upstream: 10.5
    * Downstream: 22


## 2016-08-06
Initial problems occur late evening.
ADSL connection drops entirely, and then comes up with a much lower sync rate (~3-4Mbps down, ~100Kpbs up).


## 2016-08-07
Vodafone contacted via Twitter handle.
ADSL connection auto-syncs as ADSL2+, at higher rate (~5Mbps down, ~175Kbps up).
It had the following [sync speed](https://pbs.twimg.com/media/CpOuGhIUMAAlSzg.jpg), and [SpeedTest](http://www.speedtest.net/my-result/5534293693) results.


## 2016-08-08
Vodafone notifies via Twitter that it had made a change on their end (exchange I assume).
This increases the sync down speed by ~1Mb.

### Isolation test
Vodafone also asked for an [Isolation Test](https://community.vodafone.co.nz/t5/Modems-Wi-Fi/Read-Me-Broadband-Troubleshooting-amp-Isolation-Test/td-p/90598).

In my case this included:

* Connect directly in to master phone socket, bypassing short in-wall cable (20cm approx)
* Use BT to RJ11+BT ADSL line filter
* Use short RJ11 cable to the ADSL router, from original ADSL router package

This did not significantly (<1Mbps down) increase the sync, or SpeedTest results.

The router was returned to the previous configuration.
It had the following [sync speed](https://s3-ap-southeast-2.amazonaws.com/neilramsay-public/dsl/2016-08-08_18-52-20.png), and [SpeedTest](http://www.speedtest.net/my-result/5536476887)


### Sync issues
After the isolation test (15-20 minutes?), the router lost DSL sync.
When it did resync, it was to a much slower speed, and would not load speed test.
It synched with the most basic DSL modulation type, T1.413 Annex A.

After multiple DSL setting reloads, and router restarts, the router refused to connect in either ADSL2, or ADSL2+ mode.
The 'highest' mode connected was with G.dmt, but only through auto-detection.

Forcing ADSL2, or ADSL2+, did not work until about 11pm.
This was a greatly improved connection ([SpeedTest](http://www.speedtest.net/my-result/5536926940)).
It is not entirely clear what caused the improvement.


## 2016-08-09
The connection has had a stable sync in ADSL2+ Annex A/L/M, with a sync speed of ~9.5Mbps down, and ~400Kbps up.
[SpeedTest confirms similar speeds](http://www.speedtest.net/my-result/5538689779).

However, many webpage loads fail. This may be because packets are being dropped - this still needs to be investigated.

## 2016-08-11
Vodafone requested that, if possible, I try a different modem.
The current modem is a TP-Link Archer D7 (ADSL2+), and the old modem is a 3Com OfficeConnect 11g (ADSL1).

With the ADSL1 modem, I got the following results:

* Isolation Test - [Sync Speed](https://s3-ap-southeast-2.amazonaws.com/neilramsay-public/dsl/2016-08-11_16-57-36.png), [SpeedTest](http://www.speedtest.net/my-result/5544419227)
* Regular Cabling - [Sync Speed](https://s3-ap-southeast-2.amazonaws.com/neilramsay-public/dsl/2016-08-11_16-46-57.png), [SpeedTest](http://www.speedtest.net/my-result/5544406812)

The above tests produced similar speed results to my current modem, but a higher attenuation reading for the upstream bands.
This difference appears to be a result of how ADSL1, and ADSL2 modems measure the attenuation ([reference](http://www.speedguide.net/faq/what-is-considered-good-dsl-line-attenuation-371)).
The original measurements were from the ADSL2+ modem, so I will use those measurements in comparing attenuation changes.

The key concern is that the line attenuation reading difference between pre-incident, and post-incident (based off my current router), is double for upstream, and is 50% greater for downstream.
As line attenuation is a logarithmic function, each 3dB increase reduces the signal strength by half.
With an attenuation increase of about 10dB, it means that we have lost 7/8ths of our previous signal strength ([reference](http://www.speedguide.net/faq/what-is-considered-good-dsl-line-attenuation-371)).

I suspect that a wiring degradation (conductor damage, punch-down block, etc), somewhere between the exchange, and the jack-point in our house, has been stretched in the recent weather.
This would reduce its conductivity, and increase the attenuation.

## 2016-08-17
Chorus technician made contact.
The technician noted that Vodafone advised him that the connection had been receiving pre-incident speeds for the previous 4 days (I had not checked recently) of about 19Mb down, 1Mb up.
The technician will get in touch in a few days, where he may inspect the insulation between the aerial line connection to the house, and the master jackpoint. There may be some insulation problems there (based off basic visual inspections).

The results from the next day testing were; [sync speed](https://s3-ap-southeast-2.amazonaws.com/neilramsay-public/dsl/2016-08-18_18-09-45.png), and [speed test](http://www.speedtest.net/my-result/5561133541).

## 2016-08-22
Chorus technician made contact again.
The connection has been stable for a while, so he has asked me to contact Chorus again if there is a problem.
I suspect it is weather dependent (rain, and strong northerlies), and there is no point attempting to locate a fault if it is not present and measurable.

