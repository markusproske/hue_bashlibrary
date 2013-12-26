## The unofficial Philips Hue Bash Library

This library allows **local** control of your Philips Hue system. The Hue BashLibrary uses curl to communicate with your Hue bridge. You can use this library with several Linux-based systems, Mac OS X, Raspberry (Raspbian) and many more. 

The library offers bridge functions, light functions and some logging capabilities. Bridge functions are link / unlink, output the configuration and a lookup with meethue.com to obtain the IP of your bridge (if available). Light functions include on/off, all lights off, on with a specified hue/saturation/brightness or mired value, functions to change hue/saturation, brightness and mired (without touching the on/off state) and the alert functionality (lights will blink). Finally, there is a special function that reports if a specific light is currently on or off, the result is delivered in a global variable named "$result_hue_is_on". Please note that not all functions of the Philips Hue API are available, however, additional functions can be added easily using the implemented wrappers for get, put, post and delete. Take a look at the source of "hue_bashlibrary.sh" to see all functions and their parameters!

The file demo.sh provides a starting point for your own applications. It provides a very basic argument processing to link/unlink your bridge and runs a demo function from the library. Follow the steps below to get started:

1. Get the IP of your Hue bridge. If it is connected to the Internet "./demo.sh discover" might work. Otherwise you can get the information via your router's interface.
2. Edit the file "demo.sh" and enter the IP of your Hue bridge in the configuration section on top
3. Use "./demo.sh link" to link the computer/app with your Hue bridge.
4. Run "./demo.sh", lights 3 and 4 will show off. You can change the lights used in the configuration section of the file.
5. Enjoy!

For real-world usage see Hue WakeUpLight and Hue Sunset (coming to G+ and GitHub soon).


## Examples

**Function to show a couple of commands of the hue bash library for up to 8 lights:**
```bash
function hue_demo() {
	lights="$1 $2 $3 $4 $5 $6 $7 $8"
	delay=10
	
	hue_alloff
	
	hue_on_hue_sat_brightness 25500 50 50 $lights
	sleep $delay	
	hue_onoff off $lights
	sleep $delay	
		
	hue_on_mired 500 $lights
	sleep $delay	
	hue_onoff off $lights
	sleep $delay	
			
	hue_onoff "on" $lights

	hue_setstate_mired 153 $lights	
	sleep $delay
	
	hue_setstate_brightness 255 $lights	
	sleep $delay
	
	hue_setstate_brightness 1 $lights	
	sleep $delay
	
	hue_setstate_hue_sat 46902 255 $lights
	sleep $delay
	
	hue_alert single $lights
	sleep $delay
		
	hue_onoff off $lights
}
```

**Usage of hue_is_on:**

```bash
hue_is_on 3
echo "Result variable is: $result_hue_is_on"
```


**Configuration section (demo.sh):**

```bash
# import my hue bash library
source hue_bashlibrary.sh


# CONFIGURATION
# -----------------------------------------------------------------------------------------

# Mind the gap: do not change the names of these variables, the bash_library needs those...
ip='10.0.1.8'								# IP of hue bridge
devicetype='raspberry'						# Link with bridge: type of device
username='huelibrary'						# Link with bridge: username / app name
loglevel=1									# 0 all logging off, # 1 gossip, # 2 verbose, # 3 errors


# Variables of this scripts
lights='3 4'								# Define the lights you want to use, e.g. '3' or '3 4' or '3 4 7 9'
```