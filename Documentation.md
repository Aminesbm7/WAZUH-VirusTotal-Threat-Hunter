# Starting Point

Once we have the wazuh installed and configured, with our wazuh-agent on the client, and we are able to see it on the dashboard
we can start with this project.
![imatge](/images/1.png)


# VirusTotal Integration

The first thing we need to do is to add a virustotal integration to our wazuh, in the wazuh machine cli, we add this integration,
with your virustotal api key. (after every change in configuration file restart the wazuh services in case changes not applying)

![imatge](/images/2.png)


Now from our wazuh-dashboard we should be able to see the virustotal module.

![imatge](/images/3.png)



# Wazuh-agent configuration

In order to start monitoring, in the client we must touch a configuration file and indicate a path to monitor, it could be the entire system but in this case, 
since I am only in a test environment, i will indicate the Downloads folder.
File to edit: (C:\Program Files (x86)\ossec-agent\ossec.conf)


![imatge](/images/4.png)

To test that Wazuh is monitoring the Downloads folder, i will download a malware and place it in the folder and see what happens.


![imatge](/images/das.png)


Automatically after, the in the wazuh-dashboard we will see that a malicious file has been detected.


![imatge](/images/6.png)


If we check the details of the alert, we will see a link to virustotal, where we will find the test that virustotal run to verify if the file is malicious or not.


![imatge](/images/7.png)

![imatge](/images/8.png)


# Threat Removal via automated task

We will use a python script, to automate the threat elimination, first we convert the python into exe using this cmd command.
Python script: (https://pastebin.com/4TpkxNKJ)

![imatge](/images/9.png)


Once we have the exe, we place it in this folder where wazuh-agent stores all active-response executables.

![imatge](/images/10.png)


Now we hop on the wazuh machine, and we add this bit of code in the "/var/ossec/etc/ossec.conf".

![imatge](/images/11.png)


We also want to add a set of rules in case the threat has been removed or not, in this file "/var/ossec/etc/rules/local_rules.xml".

![imatge](/images/12.png)


Ok, now we have everything set to go, as a test, again im going to download a malware and place it in the Downloads folder and see what happens.
Now not only the file gets detected, but its being removed automatically, if u look closely in the security alerts, we can see a Virustotal alert and a Defense Evasion Impact.


![imatge](/images/13.png)


As a prof, im gonna leave here a gif on where i show that i place malware on the Downloads folder and automatically gets deleted.


![imatge](/images/15.gif)
