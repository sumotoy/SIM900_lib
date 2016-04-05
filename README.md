# SIM900_lib
A library and how to for SIM900A and Teensy 3
Time ago I buy from a chi-bay a SIM900A module and a week ago I got a sim card laying out table so I decided to test it.
Before connecting any cable I searched the web and discover that this unit doesn't like 5V, it needs 4.45V at max, but the worst has to come, the model SIM900A will not work in Europe or USA, only few countries in asia are enabled!
Ok, it was really cheap, I payed less than 6 US dollars!<br>
The boards communicate with serial but not at TTL level! It has an RS232 chip onboard that it's good only for RS232 but not for Teensy.
Other problem it's the documentation, absolutely useless.<br>
First step, fix the supply problem that was easy, a diode has a dropoff of 0.7V and does the trick! Be careful that this module it's current hungry, it can eat almost 2A accordly datasheet but I personally used 1A and worked, again cannot be sure!<br>
Second setp, fixing the serial. Fortunately the board has 2.8V level serial exposed on a 6 pole pin where normally there are jumpers, this pin seems 3v3 compatible (it worked with my board but I cannot be sure!) so I can use with Teensy.<br>
Now the third step, how to make it work in my country?<br>
I have connected everithing and placed a serial->usb adaptor (that has a switch 3v3,5v, HAS TO BE SET AT 3v3!) and used a terminal.<br>
Sending AT will result in a 'OK' so the board communicate, cool! But as I was suspect it recognize my SIM card but not connect any network!<br>
Digging internet I find that SIM900A it's really similar (or equal?) to a SIM900 but has 2 band support only, the limitation for the countries is in firmware and I find a modified firmware that fix this.<br>
There's an utility for that, SIM900 Series download Tools Develop 1.9.exe (inside utility folder->FirmwareUpdateUtility_win.rar), I have opened it, set the correct serial port and uploaded the new firmware called 1137B01SIM900M64_ST_ENHANCE.cla (inside Utility folder->Firmware folder->Tested.rar->1137B01SIM900M64_ST_ENHANCE).<br>
Hit start, the program wait for a reset or restart...Mmmm, looking my board there's 2 more pin hole exposed but umpopulated, called RST and RESTART, I connected a short cable in the RST hole and touched the antenna connector (that it's connected to Ground) and...voilà, the firmware start to go!<br>
It takes 2 pass so stay quite and do not disturb the uploading or your module will be ready for the trash!<br>
When done, it needs a complete powerdown, powerup, so I disconnect supply, wait 3 sec and reconnected, open terminal and check waht's happen.<br>
Now the board connect my network, however you should know that this is a 2G device and it's NOT compatible with 3G or 4G! So you need a 2G Sim from a company that support 2G network!<br>
In many country Vodaphone has but since I hate them I've choosed Tim (that I hate as well but less than Vodaphone) and worked.
I will publish a step to step procedure with pictures in few days.<br>
The library will come shortly, as always I'm testing for my needs and publish when ready.
