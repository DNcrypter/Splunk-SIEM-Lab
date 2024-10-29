# Splunk-Home-Lab

Splunk is a powerful platform for searching, monitoring, and analyzing machine-generated big logs data in real-time. The Splunk Indexer processes incoming data, transforming it into searchable events, while the Forwarder collects and forwards log data to the Indexer for analysis. Together, they provide comprehensive insights into your systems and applications.  

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
        [![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
        [![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)

## 🍁Introduction
This lab is design to practice log analysis using universal forwarder and indexer. We will Install and Configure Splunk Indexer and Forwarder on Ubuntu linux machine.

![](https://github.com/DNcrypter/Splunk-SIEM-Lab/blob/main/splunk_2.png)

## 🔗Prerequisites
- basic understanding of command-line
- internet connectivity
- familiar with linux system.

## 📝Requirements:
- Vmware
- Ubuntu 22.04 installed on Virtual machine.

## 👩🏻‍🔬🧪Lab set-up
**⚙️ Splunk indexer installation**  

**Step 1** : Register on splunk website. you can use tempmail service inplace of your mail_id. then, to download splunk enter below commands in your terminal.
```
wget -O splunk-9.3.1-0b8d769cb912-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.3.1/linux/splunk-9.3.1-0b8d769cb912-Linux-x86_64.tgz"

```

**Step 2** : Go to directory where you download splunk. Enter below command in terminal.
```
sudo tar -xvzf splunk-9.1.0-linux-64.tgz -C /opt
```

**Step 3** : run splunk by accepting license agreement.
```
sudo /opt/splunk/bin/splunk start --accept-license
```

**Step 4** : Press space button till reach bottom. Create your username and password. Go to http:localhost:8000/ and login.
```
http:localhost:8000/
```



**⚙️ Cofiguration and error handling**  

**Step 1** : To access splunk from anywhere with your terminal create link using below command.
```
sudo ln -O /opt/splunk/bin/splunk /local/bin/splunk

```
**Step 2** : Now you are ready with splunk index. start splunk or stop splunk with below cammands.
```
splunk start
splunk stop
```

**Step 3** : Enter login Credintials in login page of splunk on browser.
```
http:localhost:8000/
```

**Step 4** : After login, Setup listener in splunk indexer. Go to **setting > forwarding and receiving>configure receiving** click on add new and enter port (9997) we will use further it to add in forwarder.

**⚙️ Splunk Universal Forwarder installation**  

While installing fowarder in same machine we have to be careful that it can create conflict. Yes, I stuck there with config problem for 2 hours. specially with error as $SPLUNK_HOME and $SPLUNK_ETC not define? ,etc.

**Step 1** : Download splunk forwarder using command below or you can install from its website.
```
wget -O splunkforwarder-9.3.1-0b8d769cb912-Linux-x86_64.tgz "https://download.splunk.com/products/universalforwarder/releases/9.3.1/linux/splunkforwarder-9.3.1-0b8d769cb912-Linux-x86_64.tgz"

```
**Step 2** : unzip the tar file and move it to /opt directory.
```
sudo tar -xvzf splunkforwarder-9.3.1-0b8d769cb912-Linux-x86_64.tgz -C /opt

```
**Step 3** : Go to /opt/splunkforwarder/bin directory.
```
cd /opt/splunkforwarder/bin
```

**Step 4** : Start Splunk Forwarder and accept license agreement.
```
sudo /opt/splunkforwarder/bin/splunk start --accept-license

```
**Step 5** : Run splunk forwarder after every boot-start.
```
 ./splunk enable boot-start
 ```
**Step 6** : Now, we configure universal forwarder to send data to over receiving indexer. as i install both in same machine i used same ip you can use of splunk indexer.
```
./splunk add forward-server 127.0.0.1:9997

```
**Step 7** : After enter prompted with username and password enter there.
```
./splunk add monitor -auth username:password /var/log
```
**Note** : As i am using ubuntu linux i enter /var/log, you can change with your logs stores.

**⚙️ Configuring and Error handling**

While configuring forwarder specially in same machine you could face error like $SPLUNK_HOME and $SPLUNK_ETC variable on setup, etc

**Tip** : while handling error try solve by searching on internet if not ,solved, then use chat-gpt that can solve problem. if you still face same problem again and again shutdown machine and restart after 5 minutes. Start again from first step. it worked for me.

Go to splunk indexer app and enter to “search and reporting section >> Data Summary”.

Bhoom…💥🎉😎… You setup your splunk with full on live log analysis. whenver logs are update in your machine you can access and analyse it from splunk indexer.

## 🚩Conclusion
Intension of this lab is to learn how splunk enterprise system works and how we can configure & install them. I will show you how to analyse http_logs, DNS_logs, smtp_logs,etc in Next project.


