# DSC - Decline Spam Caller

_DSC_ is a tailored [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) project to automatically decline robocalls and spam calls.

If you receive a lot of genuine calls from numbers you don't know (e.g., from random clients) then _DSC_ **will not help**.

## Lore
I live in Italy, and the spam and robocalls are unbearable. They somehow manage to use unlimited/spoofed phone numbers, so most of the time [Phone by Google](https://play.google.com/store/apps/details?id=com.google.android.dialer) app fails to block them. In my case, about 95% of calls from numbers not in my contacts are just a waste of time.

## Requirements
- Android
- [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) (*trialware*)
 
## Features
- Scheduled activation
- Silently let the call "ring" in background
- Optional check of the caller score via [Tellows](https://tellows.com)
- Optional bypass of the filter on multiple calls from the same number over a time limit

## Android Call Screening
The good thing of Call Screening is that the "_default caller ID and spam app_" is triggered **before** your smartphone starts ringing.

This allow us to set Tasker as the "_default caller ID and spam app_" and apply the filtering of _DSC_ as soon as possible.

## How it works
First of all, your contact list is the whitelist; every number in you contact list will bypass _DSC_ and you will receive the call.

All the other (not-saved-contacts) numbers will succesfully pass the _DSC_ "screening process" only if (one of the following is true):
- Tellows returns a score from 1 to 4. Then the call is probably safe and will not be declined
- The number has called X times within N seconds (X & N are configurable)

For the calls that don't pass the "screening process", _DSC_ will let the phone ring silently in the background (your smartphone will show nothing).

You'll see a missed call notification only once the caller gives up.

_(Tasker has an option to hide this notification but it doesn't seem to be working at the moment.)_

## To decline or not to decline
The options we have:
- (_good_) Not answer / do nothing
- (_bad_) Decline the call
- (_worst_) Answer the call

If you answer, the pesky spammers will (probably) flag your number as active (and may resell your data to other spammers), which could increase the number of calls.

If, instead, you decline, it sadly doesn't make much difference -> it still indicates that someone was "actively there", so your number may still be flagged as active.
Because of this, our best bet is to not answer!

## Installation
Install [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) and configure it properly (permissions, unrestricted backgroud activity, set it as 'default caller ID and spam' app etc...).

Check the [official documentation](https://tasker.joaoapps.com/) for more information! _DSC_ is a Tasker project, not a tutorial on how to use Tasker.

###### TaskerNet (easy way)
[_TaskerNet Link_](https://taskernet.com/shares/?user=AS35m8m%2B3NlqE3hjJHjTs0ZoGxQVx9O7awY9kn9bI0ezvr0d4q%2BlW4bQgZf%2B503WdmgmaA%3D%3D&id=Project%3Adecline-spam-call)

###### XML (manual way)
Download the XML project file from this repository to your smartphone.

Open Tasker and go to "Import Project" (hold the house icon, bottom left)

Select the XML and import it!

## _DSC_ Configurations

#### Tasks
Open the _DSC_ project (bottom row of Tasker)

Open the "**TASKS**" tab and check the one named: "**DSC - Set Configs**"

###### *%dsc_cfg_treshold* & *%dsc_cfg_bypass*
Here you can configure the "X times within N seconds"

Example: If you set the *threshold* to **900** and the *bypass* to **2**, it means that if someone calls you **2** times within **900** seconds, your smartphone will only ring for the **second** call. In other words, _DSC_ will *block* the **first** call within the **900** seconds window but let the second one *through*.

This feature is handy when someone you don't know needs to urgently contact you, as they'll probably call multiple times within a short timeframe.

If you don't want this "repeat to bypass" feature then just set any unreachable amount like *threshold* **1** and *bypass* to **100**

###### *%dsc_cfg_tellows_enabled*
Set this to 0 if you don't want to use the [Tellows](https://tellows.com) score feature.

Set to 1 to enable the feature.

Having it enabled means that the caller phone number will be sent to [Tellows](https://tellows.com) to get the score.

###### *%dsc_cfg_debug* & *%dsc_cfg_debug_phonenumber*
There's no need to edit these; they're used to test and bugfix stuff.

#### Profiles
Open the _DSC_ project (bottom row of Tasker)
Open the "**PROFILES**" tab, you will find two modes "Screened" & "Call" and the "Scheduler"

###### *DSC Mode - Screened* & *DSC Mode - Call*
The **screened** mode is the most recent one, allow to silently let the call "ring" in background (_good_).

The **call** mode is the old one, no longer works on recent Android versions and is only able to decline the call (_bad_). I strongly suggest to not use this.

You can't have **screened** & **call** enabled together, you must choose one.

A "*DSC Mode*" profile is a global switch, having both off will turn off the whole _DSC_, this means that any call you receive will **not** be filtered.

###### *DSC Schedule 1*
Open *DSC Schedule 1* to edit the date and time when _DSC_ will be active, then turn it on.

I usually keep it active during work hours, the pesky spammers don't call outside those times and I don't want _DSC_ running in the evenings or on the weekends.

You you want multiple schedules: duplicate *DSC Schedule 1*, rename it *DSC Schedule 2* and configure it as you like.

> NOTE: If all "*DSC Schedule*" profiles are turned off, then _DSC_ will always be active.
