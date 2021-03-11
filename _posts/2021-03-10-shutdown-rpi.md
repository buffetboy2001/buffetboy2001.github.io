---
layout: single
title:  "Hey Pi, Shutdown!"
date:  2020-03-10
tags: ['robotics']
excerpt: I needed them to learn to shutdown their Raspberry Pi the safe way. 
---

An important lesson I've learned the hard way in teaching robotics is that you've got to give the students a simple way to shutdown their Raspberry Pi. At first, I just foolishly assumed that the Pi could handle some hard shutdowns, so I told my students to unplug the Pi when class was over.

Duh. Big mistake.

Of course, the Raspberry Pi isn't fault tolerant like that at all! Why should I expect it to be. If it happens to be writing system files when the power gets cut...yeah.

I soon found that the operating systems were getting corrupted and those cute little computers refused to boot. After re-building the operating system a few times -- not to mention students losing their hard-typed code -- I decided I needed a better system.

I needed them to learn to shutdown their Raspberry Pi the safe way. And I needed it to be done in software. Here's what [I gave them](https://github.com/buffetboy2001/ccr_robotics_fall_2020/blob/4c7a38c89b91596ff1a56c46cb097edf9fb2c9a7/src/shutdown.py#L1).

```python
#!/usr/bin/env python3

'''
Shut down the Raspberry Pi
'''

import time
import os, sys

time.sleep(3)
os.system("sudo poweroff")
```

The code we write in robotics class is all Python. My new shutdown solution had to be a fit to what the students already knew. Now, I didn't come up with this myself. But, a little internet searching was all it took. And it's fairly intuitive once you look at it. Hope you find it useful too!