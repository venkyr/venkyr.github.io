---
layout: post
title: "Choosing a vibe coding tool"
date: 2025-06-14
---

There are several vibe coding tools out there but after some research and tinkering it came down to 
Cursor and Windsurf for me.  One of the factors was that they are both based on VS Code, so that cuts 
down the learning curve.  Like most tool decisions it comes down to what works best for your needs. 
So I decided to put both tools to the test for a scenario I often encounter:  I develop a new gizmo with 
custom or off-the-shelf hardware, a Raspberry Pi, PLC, or other embedded controller, and write custom 
software in C or Python to interface with the hardware.  But then I want to wrap it up in a nice bow 
and send data to my Influx dashboard for monitoring, or a web page for interactive control.  This is 
where I want vibe coding as this stuff is well documented and the coding agent ***should not*** make 
mistakes.

During the pandemic I made a Tesla Powerwall clone with an off-the-shelf inverter, a charger, a 
LiFePO4 battery pack, a 3rd party battery monitoring system (BMS), some relays, and a Raspberry Pi
controller.  I designed custom A/D converter circuitry to measure various AC currents and battery 
parameters and wrote python code for the Raspberry Pi to interface with the hardware.  I also wrote
the code to send the data to InfluxDB but it was messy and has been on my TODO list to clean up 
for several months.  What better way to take care of this technical debt than to use vibe coding, 
and put both Cursor and Windsurf to the test!

I created a project directory for each tool and placed my low-level python modules in both. I then 
gave both tools the following prompt:

```

I have 4 python files here I need you to analyze.

    1. ac_currents.py has a get function that returns a named tuple with 
       AC current values.

    2. batt_status.py has a get function that returns a named tuple with 
       various battery parameters.

    3. inverter.py has a is_on() function that returns True if the inverter is 
       running, false otherwise.

    4. charger.py has a is_on() function that returns True if the charger is 
       running, false otherwise.

I need a new python script that does the following:

    1. Read a config.ini file containing influxdb configuration parameters.
       The name of the influxdb bucket should also be in the config file.

    2. Every minute (configurable in the config file), use the functions described 
       above to read the AC currents, battery parameters, charger and inverter states,
       and send them to my influxdb instance.

    3. Use the name of the named tuples for measurement fields, and the tuple value
       names for the fields.

    4. For the inverter and charger, use a measurement called "Controllers" and the 
       fields to "inverter" and "charger".  Use 0 and 1 for False and True respectively.
```

Both tools generated a new python module, a config file for InfluxDB, and a requirements.txt file 
for pip. However, Windsurf was disappointing from the start:

- The python code it generated had a syntax error (I mean, really!)
- After a prompt to fix the error, the new script generated a runtime error.  Another prompt fixed this error.

After testing and validating the results on the Influx dashboard I asked both tools to create a local github 
repo, generate a README.md file, check-in and commit the code, and finally push it to my public github repo. 
Both tools fared equally in these tasks.

The third strike against Windsurf was that it did not use python's logging module.  Only lazy programmers used 
print() in my humble opinion! Windsurf's README file was more elaborate but it also made an incorrection assumption that my project was a Solar Monitoring system. 

Both repos from this challenge are on my github:

- [Cursor](https://github.com/venkyr/lightning-cursor) 
- [Windsurf](https://github.com/venkyr/lightning-windsurf)

So, for now, I'm going to sign up with Cursor.