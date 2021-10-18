# Need For Logging

Most applications require logging and tracing capabilities. One can usually use ColdFusion's standard `cflog` or `cftrace` tags but you can reach a limitation very fast.

* What if you needed to log only certain severity levels for a particular CFC or piece of code? 
* What if you needed that severity to advise you via SMS or Twitter (yes Twitter)? 
* What if you wanted to turn it off easily or reconfigure your logging levels?

You would have to build all of these advising and logging capabilities yourself. Also, inserting log statements is tedious, time consuming and frequently pollutes your real code. You can understand the pain and complexity required to properly deal with these situations. These reasons (and more) are why the ColdBox team has invested in building LogBox.
