INTRODUCTION:

When pen-testing login credentials many websites implement network defences against such repeated login requests to prevent misuse and this often comes into play after the user has tried a set number of login attempts (eg 10 or 20 etc). The user, after a set period of not making any further requests (usually a few minutes to one hour), is often then permitted by the application to resume making credential-guessing requests.

This script allows the tester to try and circumvent any application server login attempt protection which may be more likely to happen with repeated login attempts of the same username. This script allows several username and counterpart passwords lists to be tried in turn and so in this respect it is useful if there are login credentials for several users on the same site which need to be tested.

During the running of Burp Intruder, this script takes a username and password from multiple username and (counterpart) password lists and iterates through these lists one after the other until all the words on the lists are tried. In this example there are 4 different usernames contained in one list, and 4 separate lists of passwords - each specific username having its own counterpart password list:

Username 1 in users.txt has counterpart passwords in the file words1.txt
Username 2 in users.txt has counterpart passwords in the file words2.txt
Username 3 in users.txt has counterpart passwords in the file words3.txt
Username 4 in users.txt has counterpart passwords in the file words4.txt

This is what some example requests would look like:

Request 1: tries the first username in the file users.txt against the first password in the file words1.txt
Request 2: tries the second username in the file users.txt against the first password in the file words2.txt
Request 3: tries the third username in the file users.txt against the first password in the file words3.txt
Request 4: tries the fourth username in the file users.txt against the first password in the file words4.txt
Request 5: tries the first username in the file users.txt against the second password in the file words1.txt
Request 6: tries the second username in the file users.txt against the second password in the file words2.txt
etc
etc   
The requests will continue until all the usernames in the users.txt file have been paired with all the passwords in their associated words(number).txt file.


REQUIREMENTS:

A free or paid version of BurpSuite with Turbo-Intruder installed.


USAGE INSTRUCTIONS: 

Download the script2_0.py from this repo. Right click on the login request to be tested (either within the proxy tab in Burp or within the Intruder tab) and select Turbo Intruder which should open another window showing the request to be tested. In the top half of the Turbo-Intruder window (within the `Raw' tab) replace the password string by entering "%s" (without the quotes) e.g password=%s. Also place a "%s" in the username string eg username=%s  

On the bottom half of the same window you will see the default Turbo script. Copy & paste the content of script2_0.py, replacing the whole content in this part of the window. Within the first lines of the pasted script you will see "#Parameters to configure", where the following can be edited:

concurrentConnections=number of concurrent connections. Example usage: concurrentConnections=5 
throttleMillisecs=number of milliseconds to wait before each request. Example usage: throttleMillisecs=200
 
Create a users.txt file in the main BurpSuite directory where the Burp.exe is located. In this users.txt file, list in a column all the usernames to be tested. For the number of usernames listed, create the same number of password files in the format words(number).txt. For example if there are 3 usernames to test, there will also be words1.txt, words2.txt and words3.txt files - all saved to the same Burp directory where the burp.exe file is located. Each words.txt file should list the passwords to be tested in a column. 
For every username listed there needs to be the the same number of words.txt files, so if there are 20 users in the username list, there should be 20 words.txt files containing the passwords. In this respect nothing in the script needs to be altered to reflect the number of users or password lists.


Click on `Attack' at the bottom of the Turbo window to execute the script. Note this has only been tested on the `sniper' attack type within Burp Intruder. Some tweaking of the parameters described above may be needed to ensure this script works against the particular target to be tested.







