## The unofficial Philips Hue Bash Library

This library allows **local** control of your Philips Hue system. The Hue BashLibrary uses curl to communicate with your Hue bridge. You can use this library with several Linux-based systems, Mac OS X, Raspberry (Raspbian) and many more. 

The library offers bridge functions, light functions and some logging capabilities. Bridge functions are link / unlink, output the configuration and a lookup with meethue.com to obtain the IP of your bridge (if available). Light functions include on/off, all lights off, on with a specified hue/saturation/brightness or mired value, functions to change hue/saturation, brightness and mired (without touching the on/off state) and the alert functionality (lights will blink). Finally, there is a special function that reports if a specific light is currently on or off, the result is delivered in a global variable, 1 is on and 0 is off: 
>hue_is_on 3
>echo "Status of bulb requested: $result_hue_is_on"

Please note that not all functions of the Philips Hue API are available, however, additional functions can be added easily using the implemented wrappers for get, put, post and delete. 


The file demo.sh provides a starting point for your own applications. It provides a very basic argument processing to link/unlink your bridge and runs a demo function from the library. Follow the steps below to get started:

1. Get the IP of your Hue bridge. If it is connected to the Internet "./demo.sh discover" might work. Otherwise you can get the information via your router's interface.
2. Edit the file "demo.sh" and enter the IP of your Hue bridge in the configuration section on top
3. Use "./demo.sh link" to link the computer/app with your Hue bridge.
4. Run "./demo.sh", lights 3 and 4 will show off. You can change the lights used in the configuration section of the file.
5. Enjoy!

For real-world usage see Hue WakeUpLight and Hue Sunset (coming to G+ and GitHub soon).
