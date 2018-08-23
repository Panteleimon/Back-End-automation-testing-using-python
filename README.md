# Back-End-automation-testing-using-python

I was recently in the proccess of designing and creating a BaaS server and subsequently searched a lot in order to find the easiest way to create and maintain it while keeping the procedure as simple as possible for someone else to swiftly understand and maintain. Remember that servers do not have a GUI and unless you are really familiar using the terminal you are gonna have a hard time finding what's going on. Which is bad in production scenarios because downtime or slow implementation of features/changes equals to loss of money and user dissatifaction.

This guide is what I wished was out there when I was desperately searching so... LUCKY YOU!

The bigger and the more complex a procedure is, the bigger the chances are that something will go wrong because there are more points of failure present. On the other hand when something is as easy as pressing a button or copy-pasting a simple command, what can go wrong, right? Well this is the logic behind a production scenario since, as time passes by in order to stay competent more and more needs emerge subsequently more and more changes are being made and extra features added. System adminstrators and software engineers try to find ways in order for the things they implement, to be bullet-proof and ,at the same time, simple for someone other than them to understand, maintain and modify if need be in the future as fast and as securely as possible.

Lets create 2 hypothetical scenarios. One is that we have a new machine which has to be configured as a backend server by setuping programs, updates, services etc... The second scenario is already having a configured machine that has to be drastically altered to a new state (due to legacy support or incompatibility with new client software).

Those 2 scenarios may be daily routine depending on the nature of a company. Setuping new machines to be part of a cluster or constantly patching an eshop to include new technologies like "Apple pay" or "Chat with our experts" are some examples. 

I think it is self explanatory why things like that must be first tested in a simulation environment and then implemented on the production one. But even then, after spending time "trialing and erroring" in the simulation environment the correct procedure, although now known, still has some obscure and uncertain steps that must be tested from the beggining. If something seems to be wrong when said procedure is tested, modifications that will possible solve the problem are made and then... everything again from the beggining! And so on. On top of that, the human factor of implementation adheres to the time being wasted. And we haven't even mentioned the fact that every time a step is altered in the procedure it must be written down (version control). So others after us must know how to, what has been done and how to modify further. The whole thing seems pretty intricate and complicated, right?

Here's where python comes in. There is a way to eliminate the human factor from the procedural scenario by having python do it and at the same time not having to document anything because the python code itself is the documentation. Moreover, testing a whole scenario which may include millions of steps in a simulation environment is actually typing one command and pressing 'enter'. Seriously, no kidding. That's it:

        wget www.where_file_is_located.com/magical-python-file.zip && sudo python magical-python-file.zip

Which means that if the simulation environments are tested at hosting company (like DigitaOcean, Azure or Amazon), which they should, having a freshly installed operating system is a matter of seconds. Copy pasting the command is also a matter of seconds. And since there is no human implementation and python does it all, the procedure that python has to accomplish is a matter of seconds (or hardly ever minutes) too. Unless you're a huge company having servers/clusters with tons of data leading to the procedure taking hours, which you're not because you wouldn't be reading this article. Subsequently testing a feature in simulation is a matter of seconds or minutes in some cases. And it doesn't matter if that procedure is setuping something new or altering something that already exists. The file remains the same! Lets see how and why.

Imagine that among the many steps of a procedure is installing VLC Media Plyer on an ubuntu server. If a human was to do it he would have to write to the terminal:

        sudo apt-get install vlc
        
Seems pretty easy as a standalone command but what if it was way bigger and among million other commands and had to be executed before a specific file transfer and after a specific security update? Now if we were to do that with a python script the part where the python script executes that command would look like this:
                              
        // security update
                                
        vlc_installation = "sudo apt-get install vlc"
                                
        os.system(vlc_installation)
                                
        // file transfer

Why the same file in all situations you may be wondering. Well you can have the script check whether this is a new server or an allready configured one and if so if changes are needed based on the version, say by checking the existence of a text file somewhere. Confused? Lets take it step by step :)

A fresh version of Ubuntu 16 LTS has just finished intalling on our test server. When we enter our one magic command and the script executes it must realise that this is a new server that needs configuration. There are a number of ways to do this. One of them is to have "main()"or some other function check for a specific txt file in a specific directory, at the beggining of the execution. If the txt is present this isn't a new server and vice-versa. Lets say that this file name is "Crazy_Penguin_v1.txt". v1 because this is the first python script we have made. So the script will start taking neccessary action and after having finished it will create the txt at the specific directory. If we execute the script again nothing will happen because "Crazy_Penguin_v1.txt" now exists.

Now 6 months after having configured the server our boss informs us that because some deals were made we need to change the software we use for a specific task and install one of another company. This procedure may include again hunderds of steps and may happen month after month after month. How do we cope? Well we have the script check for the existence of "Crazy_Penguin_v2.txt", "v3", "v4" and act accordingly based on the existence of the txt version.

You can also have the script execute at every startup or have specific functions triggered after specific events or on specific hours following a schedule. You can have the script do pretty much everything you want and just download it and run it with one command, testing simulation scenarios one after the other. 

But you must have noticed that the way this solves things is bound to become messy after some time. Using a single file containing all those functions for maintenance, version control, security checks etc. accumulates to a really long file (spaghetti code) being really difficult to understand, maintain and adhere to, if need be. Well this is where Python shines bright!

Did you notice that at the single command that we saw at the beggining of this tutorial, was executing a zip file and not a python one? (Python files have a '.py' extension)

That's because Python enables you to package up a multi-module program into a ZIP file that can be run directly by the Python interpreter!
Which means that you can have a lot of little cleanly written and tidied up python scripts inside a single file and just tell python to execute that very same zip file. Which means that regardless the structure and the changes among testing phases you will always run a single command!

For example, we could have a zip file containing the following:

        example_v1.zip
                |  - '__main__.py'              # Check whether this is a new setup and accordingly calls new_server or existin_server
                |  - 'new_server.py'            # Installs programs, makes changes and applies updates required
                |  - 'existing_server.py'       # Does daily or hourly maintenance, like installing security updates or monitoring

Now imagine that this script has been run once and part of the "new_server.py" procedure required the server to reboot. Suppose that  the'new_server.py' also made sure that the '.zip' file will run on every startup. That means that after the reboot the script will check again what the situation is and now the "existing_server.py" will run and so on. From this point onward sky is the limit. You could have another python file checking on which version the server is and if not the latest apply required changes or updates.

You can do whatever you want following this abstract implementation saving you both time and money.
Happy python meddling !!!
![Come to the dark side, we have cookies](https://memegenerator.net/img/instances/60614099/now-witness-the-power-of-our-fully-operational-test-automation-framework.jpg)

