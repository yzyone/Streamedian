### Fedora/CentOS Installer

You install on your PC the restricted proxy server for streaming RTSP over websockets and the free RTSP Player.

If you would like to test our software in the simplest way, then we advice you to use the following way:

1. Run the script /usr/share/wsp/nginx/nginx_setup.sh.  
   It will install the NGINX web server and setup your environment.

2. Open a web browser on some PC in your local subnet.  
   And type "<u>IP_ADDRESS:8088</u>", where 'IP_ADDRESS' is the IP of PC, where the proxy server was installed.

3. Then you can set a RTSP link, for example: <u>rtsp://&lt;your's local PC ip address&gt;:554/h264</u>,  
   and watch a RTSP stream in your browser. In the text field you can type your own RTSP source url.

The configuration file is placed here:

`/etc/ws_rtsp.ini`

If you will change **ws_rtsp.ini** or **wsp.lic** files, be sure that you save in **UTF8** encoding.

If you would like to use the Apache web server for testing, just type in your browser "localhost:8088" (without quotes).  
If you have installed the Apache web server after this package, please type in the Terminal:

`sudo a2enconf ws_rtsp_proxy_stream.conf
sudo service apache2 reload`

**To watch stream inside local network need to change the ws url in html file**

1. Need to turn off your firewall.  
2. Find the string "127.0.0.1" in the "index.html" file and replace on an actual IP of PC, where the Proxy server was installed and launched.

`Streamedian.player('test_video', {socket:"ws://<your's local PC ip address>:8088/ws/"});`

The file is here:

`/var/www/ws_rtsp_proxy/index.html`

**Note**: In the example uses webserver Nginx which forwards all requests from port 8088 to websocket proxy server port 8080. To connect the player to websocket server directly change port number in socket address from 8088 to 8080. Also webscoket proxy port maybe changed in "ws_rtsp.ini" file.  

**Use in global and local networks**

In common case, to connect Proxy and HTML5 RTSP Player (global or local networks) it is necessary to use the valid license file for Proxy. With the valid license file you could use proxy for private and open networks according to your project architecture.

During license activation you have to set an IP address or domain name where your web page with HTML5 RTSP Player is deployed. Subdomains will be allowed, for example *<your subdomain>.streamedian.com* is allowed if you will registry the license for *streamedian.com*

Note for developers and researchers. How to work for free

1. Use the installed empty license file to be able to develop or research without purchasing a license.  
   The empty license file allows you to watch the stream on the same local host only (proxy and player is installed to the same computer).
2. To get a time limited free license file it is necessary to registry the personal cabinet on the website.  
   After sign-up on the website the personal test key is available in the personal cabinet.  
   Use this personal test key to activate the license for 180 days per for 1 domain name with up to 3 connections at the same time.
3. To get an annual free license file it is necessary to registry the personal cabinet on the website.  
   After sign-up on the website the personal free key is available in the pricing table to select.  
   Use this personal free key to activate the annual license for 1 domain name with up to 2 connections at the same time. Free licenses can be renewed each year.

To activate the key select "online" or "offline" method and follow the steps

[Steps to offline activation](https://streamedian.com/docs/#collapse-rpm-offline-activation)

1. To activate key, please, run the activation application tool that is placed:

`/usr/bin/wsp/activation_app`

2. Entry number 2 to select offline activation. If the machine info file generated successfully we saw a message with file location![](https://streamedian.com/static/img/offline-activation/step2-inv.png)
3. Go to the personal cabinet([www.stremedian.com/cabinet](https://streamedian.com/cabinet/))  
   
   
4. Choose "Offline activation" tab
   
   ![](https://streamedian.com/static/img/offline-activation/step4.png)
5. Select the key which you will activate![](https://streamedian.com/static/img/offline-activation/step5.png)
6. Upload "machine_info.bin"
   
   ![](https://streamedian.com/static/img/offline-activation/step6.png)
7. Enter domain name or IP of player host  
   ![](https://streamedian.com/static/img/offline-activation/step7.png)
8. Click "Activate" button  
   ![](https://streamedian.com/static/img/offline-activation/step8.png)
9. Download the ws.lic file
   
   ![](https://streamedian.com/static/img/offline-activation/step9.png)
10. And copy the wsp.lic file here:

`/usr/share/wsp/wsp.lic`

11. To restart the service run:

`/usr/share/wsp/restart_service.sh`

Please note that you can activate a key a limited number of times. The number of remaining activation attempts can be seen when choosing a license.![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-rpm-online-activation)

1. To activate key, please, run the activation application tool that is placed:

/usr/bin/wsp/activation_app

2. Entry number 1 to select online activation![](https://streamedian.com/static/img/online-activation/step2-inv.png)
3. Log in to streamedian account, user:psw is the same as you registered on the website
   
   ![](https://streamedian.com/static/img/online-activation/step3-inv.png)
   
   After successful login, you can see the list of available licenses and their parameters by selecting "Available licenses list"  
4. To activate the key select point "Activate"![](https://streamedian.com/static/img/online-activation/step4-inv.png)
5. And Select the key from the list![](https://streamedian.com/static/img/online-activation/step5-inv.png)
6. Enter your domain
   
   ![](https://streamedian.com/static/img/online-activation/step6-inv.png)
7. The license file will be uploaded to your server automatically and placed in the license proxy folder. The proxy will be restarting.  
   Please note that you can activate a key a limited number of times. The number of remaining activation attempts can be seen when choosing a license.![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)




