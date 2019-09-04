Dependencies:

mysql.connector : will allow us to connect to our database
sys: will allow us to get arguments
os: will allow us to go through directories
xml.etree.ElementTree: XML parsing
datetime import datetime, timedelta This will facilitate the adding and substracting of dates ( +- 10 mins )
subprocess: will allow us to get the commands running ( zgrep / grep ) to search in the nat.csv archive
netaddr import IPAddress: easy way to transform IPs into their decimal values.

The code runs casually as any python script. we just need to run the command:
python3 automator.py ../testcases
If the nat.csv. ... file isn't found while doing the zgrep command the output will be:"No file found" 
If there is no log whithin +- 10 mins, the output will be "No file found"
If there is no match in the radius logs with out timestamp and preNATIP, this will be considered as "False Positive"
if we find no user attached to a MAC Address the output will be "No such user"
If everything goes well, the output will be: "Username: %username"
A line will be printed before going to the next notice.


Assumptions:
Sometimes getting the MAC Address from the database returns multiple values. Since it wasn't precised that we may get different MAC values while defining a specific time + ipdecimal. We presumed that any of those values will be good and we didn't do a second check ( get the value with the closest timestamp ). And same goes for the Radius Logs. 

Interesting facts:

Subprocess returns a byte array, so in order to make it a string, we need to decode it with utf-8

Timedate allows us to add, substract, get absolute value and compare between dates. this is very useful to get the closest date and to get the +- 10 mins from a date and to change timezone.

When looking for an element in an XML tree, we need to add the xmlns value to it. 
Example: if we want to look for <Source> we need to look for {http://www.acns.net/ACNS}Source
