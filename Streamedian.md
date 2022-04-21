

### DESCRIPTION&PROXY

- [Home](https://streamedian.com/)>
- [Docs](https://streamedian.com/docs/#)

![](https://streamedian.com/static/img/rtsp.png)

**Streamedian** is a Javascript library which implements RTSP client for watching live streams in your browser that works directly on top of a standard HTML <video> element. It requires support of HTML5 Video with Media Sources Extensions for playback. Also player relies on server-side websocket proxy for retransmitting RTSP streams to browser.

It works by muxing RTP H264 and AAC payload into ISO BMFF (MP4) fragments.

**Streamedian** is written using ECMAScript 2015 standard

### Browser support

- Firefox v.42+
- Chrome v.23+
- OSX Safari v.8+
- MS Edge v.13+
- Opera v.15+
- Android browser v.5.0+
- IE Mobile v.11+

Not supported in iOS Safari and Internet Explorer.

### Install from GitHub

Only player sources

	npm install git://github.com/Streamedian/html5_rtsp_player.git

### Browser side

Attach HTML Video with RTSP URL

	<video id="test_video" controls autoplay src="rtsp://your_rtsp_stream/url"></video>

or

```
<video id="test_video" controls autoplay>
    <source src="rtsp://your_rtsp_stream/url">
</video>
```

You can ignore source by passing data-ignore="true":

```
<video id="test_video" controls autoplay>
    <source src="natively_supported_video_url" data-ignore="true">
    <source src="rtsp://your_rtsp_stream/url">
</video>
```

If browser can play that source, player will not be initialized for this element.

Include compiled script into your HTML:

	<script src="streamedian.js"></script>

The "streamedian.js" file is in the "HTML5 RTSP player" archive. Follow the link to download <u><a href="https://streamedian.com/#downloads">"HTML5 RTSP video player"</a></u>

Setup player in your js:

```
if (window.Streamedian) {
    var playerOptions = {
        socket: "ws://localhost:8088/ws/",            
        redirectNativeMediaErrors : true,
        bufferDuration: 30,
    };
    player = Streamedian.player("test_video", playerOptions);
}
```

### Server side

Follow these links to get the websocket proxy installation instructions for your system:

- [Windows Installer](https://streamedian.com/docs/#wininstall)
- [Mac Installer](https://streamedian.com/docs/#macinstall)
- [Ubuntu/Debian/Raspberry Installer](https://streamedian.com/docs/#debinstall)
- [Fedora/CentOS Installer](https://streamedian.com/docs/#rpminstall)

### Player architecture

Player comprises three main modules: **transport**, **client** and **remuxer**.

**Transport** responsible for data delivery and data queuing. It should fire *connected*, *disconnected* and *data* events. As soon data received, transport should push it into dataQueue and fire *data* event. Base class for transports can be found in core/base_transport. As a default, WebsocketTransport that relies on websocket proxy is implemented.

**Client** listens for data events, parse it into elementary stream packets and enqueue parsed data into it's own queue. Client can pass queued buffer to remuxer with *samples* event. To identify stream track client should fire *tracks* event. When ready, *flush* event can be used to construct media fragment and pass it to video presenter. Base class for transports can be found in core/base_client. Default client is RTSP client over websocket transport.

**Remuxer** prepares media fragment for video presenter and push it. There is only video presenter at the moment, based on media source extensions. Remuxer collects data into mp4 media fragments (moof+mdat) and pass it into source buffer.

### Windows Installer

You install on your PC the restricted proxy server for streaming RTSP over websockets and the free RTSP Player.

We recommend to use the option "Service + NGINX web server" in the installer for testing of our software.  
It allows to launch the RTSP Player in your default browser by double-click on the "Streamedian Player URL.lnk" file from your desktop.

Then you can set a RTSP link, for example: <u>rtsp://&lt;your's local PC ip address&gt;:554/h264</u>, and watch RTSP stream in your browser.  
In text field you can type your own RTSP source url.

If you will change **ws_rtsp.ini** or **wsp.lic** files, be sure that you save in **UTF8** encoding.

#### To watch stream inside local network need to change the ws url in html file

1. Need to turn off your firewall.  
2. Find the string "127.0.0.1" in the "index.html" file and replace on an actual IP of PC, where the Proxy server was installed and launched.

```
Streamedian.player('test_video', {socket:"ws://<your's local PC ip address>:8088/ws/"});
```

The file is here:

```
C:\Users\Public\Documents\Streamedian\WS RTSP Player\nginx\html\index.html
```

**Note**: In the example uses webserver Nginx which forwards all requests from port 8088 to websocket proxy server port 8080. To connect the player to websocket server directly change port number in socket address from 8088 to 8080. Also webscoket proxy port maybe changed in "ws_rtsp.ini" file.  

#### Use in global and local networks

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

[Steps to offline activation](https://streamedian.com/docs/#collapse-win-offline-activation)

![](https://streamedian.com/static/img/offline-activation/step2-inv.png)[](https://streamedian.com/cabinet/)  
![](https://streamedian.com/static/img/offline-activation/step4.png)![](https://streamedian.com/static/img/offline-activation/step5.png)![](https://streamedian.com/static/img/offline-activation/step6.png)  
![](https://streamedian.com/static/img/offline-activation/step7.png)  
![](https://streamedian.com/static/img/offline-activation/step8.png)![](https://streamedian.com/static/img/offline-activation/step9.png)

![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-win-online-activation)

![](https://streamedian.com/static/img/online-activation/step2-inv.png)![](https://streamedian.com/static/img/online-activation/step3-inv.png)  
![](https://streamedian.com/static/img/online-activation/step4-inv.png)![](https://streamedian.com/static/img/online-activation/step5-inv.png)![](https://streamedian.com/static/img/online-activation/step6-inv.png)  
![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)

#### How to watch the logs of proxy

1. Uninstall the previous version of the Streamedian WS RTSP Proxy Server.

2. [Download DebugView.zip.](https://streamedian.com/cabinet/downloads/proxy/debugview/) Unpack it and launch DbgView.exe. You will need to accept the License Agreement. The DebugView is an application of a wholly owned subsidiary of Microsoft Corporation.

3. [Install the new Streamedian WS RTSP Proxy Server.](https://streamedian.com/#downloads)

4. Reproduce an issue.

5. Watch logs on DebugView

### Mac Installer

You install on your PC the restricted proxy server for streaming RTSP over websockets and the free RTSP Player.

We recommend to use the option "NGINX web server" in the installer for testing of our software.  
It allows to launch the RTSP Player in your default browser by double-click on the "LauchPlayer" from "/Applications/Streamedian WS RTSP Proxy Server/". Or type "<u>http://127.0.0.1:8088/</u>" in your browser.

Then you can set a RTSP link, for example: <u>rtsp://&lt;your's local PC ip address&gt;:554/h264</u>, and watch RTSP stream in your browser.  
In text field you can type your own RTSP source url.

The configuration file is placed here:

/Users/Shared/Streamedian/WS RTSP Proxy Server/ws_rtsp.ini

If you will change **ws_rtsp.ini** or **wsp.lic** files, be sure that you save in **UTF8** encoding.

#### To watch stream inside local network need to change the ws url in html file

1. Need to turn off your firewall.  
2. Find the string "127.0.0.1" in the "index.html" file and replace on an actual IP of PC, where the Proxy server was installed and launched.

Streamedian.player('test_video', {socket:"ws://<your's local PC ip address>:8088/ws/"});

The file is here:

/Library/Application Support/Streamedian/WS RTSP Proxy Server/index.html

**Note**: In the example uses webserver Nginx which forwards all requests from port 8088 to websocket proxy server port 8080. To connect the player to websocket server directly change port number in socket address from 8088 to 8080. Also webscoket proxy port maybe changed in "ws_rtsp.ini" file.  

#### Use in global and local networks

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

[Steps to offline activation](https://streamedian.com/docs/#collapse-mac-offline-activation)

![](https://streamedian.com/static/img/offline-activation/step2-inv.png)[](https://streamedian.com/cabinet/)  
![](https://streamedian.com/static/img/offline-activation/step4.png)![](https://streamedian.com/static/img/offline-activation/step5.png)![](https://streamedian.com/static/img/offline-activation/step6.png)  
![](https://streamedian.com/static/img/offline-activation/step7.png)  
![](https://streamedian.com/static/img/offline-activation/step8.png)![](https://streamedian.com/static/img/offline-activation/step9.png)

![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-mac-online-activation)

![](https://streamedian.com/static/img/online-activation/step2-inv.png)![](https://streamedian.com/static/img/online-activation/step3-inv.png)  
![](https://streamedian.com/static/img/online-activation/step4-inv.png)![](https://streamedian.com/static/img/online-activation/step5-inv.png)![](https://streamedian.com/static/img/online-activation/step6-inv.png)  
![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)

### Ubuntu/Debian/Raspberry Installer

You install on your PC the restricted proxy server for streaming RTSP over websockets and the free RTSP Player. The current package installs configuration files for the NGINX and the Apache web servers.

We recommend to install the NGINX web server for most easy testing of our software. To install the NGINX web server, please type in the Terminal:

sudo apt install nginx

It allows to launch and test the RTSP Player in your default browser by typing "<u>localhost:8088</u>" (without quotes).

Then you can set a RTSP link, for example: <u>rtsp://&lt;your's local PC ip address&gt;:554/h264</u>, and watch RTSP stream in your browser. In text field you can type your own RTSP source url.

The configuration file is placed here:

/etc/ws_rtsp.ini

If you will change **ws_rtsp.ini** or **wsp.lic** files, be sure that you save in **UTF8** encoding.

If you would like to use the Apache web server for testing, just type in your browser "localhost:8088" (without quotes).  
If you have installed the Apache web server after this package, please type in the Terminal:

sudo a2enconf ws_rtsp_proxy_stream.conf
sudo service apache2 reload

#### To watch stream inside local network need to change the ws url in html file

1. Need to turn off your firewall.  
2. Find the string "127.0.0.1" in the "index.html" file and replace on an actual IP of PC, where the Proxy server was installed and launched.

Streamedian.player('test_video', {socket:"ws://<your's local PC ip address>:8088/ws/"});

The file is here:

/var/www/ws_rtsp_proxy/index.html

**Note**: In the example uses webserver Nginx which forwards all requests from port 8088 to websocket proxy server port 8080. To connect the player to websocket server directly change port number in socket address from 8088 to 8080. Also webscoket proxy port maybe changed in "ws_rtsp.ini" file.  

#### Use in global and local networks

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

[Steps to offline activation](https://streamedian.com/docs/#collapse-deb-offline-activation)

![](https://streamedian.com/static/img/offline-activation/step2-inv.png)[](https://streamedian.com/cabinet/)  
![](https://streamedian.com/static/img/offline-activation/step4.png)![](https://streamedian.com/static/img/offline-activation/step5.png)![](https://streamedian.com/static/img/offline-activation/step6.png)  
![](https://streamedian.com/static/img/offline-activation/step7.png)  
![](https://streamedian.com/static/img/offline-activation/step8.png)![](https://streamedian.com/static/img/offline-activation/step9.png)

![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-deb-online-activation)

![](https://streamedian.com/static/img/online-activation/step2-inv.png)![](https://streamedian.com/static/img/online-activation/step3-inv.png)  
![](https://streamedian.com/static/img/online-activation/step4-inv.png)![](https://streamedian.com/static/img/online-activation/step5-inv.png)![](https://streamedian.com/static/img/online-activation/step6-inv.png)  
![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)

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

/etc/ws_rtsp.ini

If you will change **ws_rtsp.ini** or **wsp.lic** files, be sure that you save in **UTF8** encoding.

If you would like to use the Apache web server for testing, just type in your browser "localhost:8088" (without quotes).  
If you have installed the Apache web server after this package, please type in the Terminal:

sudo a2enconf ws_rtsp_proxy_stream.conf
sudo service apache2 reload

#### To watch stream inside local network need to change the ws url in html file

1. Need to turn off your firewall.  
2. Find the string "127.0.0.1" in the "index.html" file and replace on an actual IP of PC, where the Proxy server was installed and launched.

Streamedian.player('test_video', {socket:"ws://<your's local PC ip address>:8088/ws/"});

The file is here:

/var/www/ws_rtsp_proxy/index.html

**Note**: In the example uses webserver Nginx which forwards all requests from port 8088 to websocket proxy server port 8080. To connect the player to websocket server directly change port number in socket address from 8088 to 8080. Also webscoket proxy port maybe changed in "ws_rtsp.ini" file.  

#### Use in global and local networks

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

![](https://streamedian.com/static/img/offline-activation/step2-inv.png)[](https://streamedian.com/cabinet/)  
![](https://streamedian.com/static/img/offline-activation/step4.png)![](https://streamedian.com/static/img/offline-activation/step5.png)![](https://streamedian.com/static/img/offline-activation/step6.png)  
![](https://streamedian.com/static/img/offline-activation/step7.png)  
![](https://streamedian.com/static/img/offline-activation/step8.png)![](https://streamedian.com/static/img/offline-activation/step9.png)

![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-rpm-online-activation)

![](https://streamedian.com/static/img/online-activation/step2-inv.png)![](https://streamedian.com/static/img/online-activation/step3-inv.png)  
![](https://streamedian.com/static/img/online-activation/step4-inv.png)![](https://streamedian.com/static/img/online-activation/step5-inv.png)![](https://streamedian.com/static/img/online-activation/step6-inv.png)  
![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)

### Docker Ubuntu Installer

To deploy docker container with websocket proxy to your server. First download an archive with docker image from streamedian.com and extract it with follow command:

tar -xvf ./ws-rtsp-proxy_1.8.5.tar.gz

Move "wsp" folder to "/usr/share":

sudo mv wsp /usr/share/

Install the Docker:

sudo apt-get install docker.io

Load websocket rtsp proxy image to docker in your server:

sudo docker load -i ./ws-rtsp-proxy_1.8-5

Run docker container based on websocket rtsp proxy image:

sudo docker run -d --name ws-rtsp -p 8080:8080 --mount src="/usr/share/wsp/",target=/usr/share/wsp/,type=bind ws-rtsp-proxy:1.8-5

Command parameters explanation:

"-d" parameter run docker container in daemon mode
"--name ws-rtsp" parameter specifies name "ws-rtsp" for container
"-p 8080:8080" parameter is proxing an in/out connection between host server port 8080 and container port 8080
"--mount" parameter gives the container access to the folder "/usr/share/wsp". 
So when we placing a license file in "/usr/share/wso" folder, it's will be available for the websocket proxy in the container.

For container manipulation is necessary to know container name. To get information about running containers and container name use follows command:

sudo docker ps -a

We can see the websocket rtsp proxy logs using docker "logs" command with specifying the container name:

sudo docker logs ws-rtsp

[Steps to check the work of websocket RTSP proxy](https://streamedian.com/docs/#collapse-ubuntu-test-page)

#### Use in global and local networks

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

[Steps to offline activation](https://streamedian.com/docs/#collapse-ubuntu-offline-activation)

[](https://streamedian.com/cabinet/)  
![](https://streamedian.com/static/img/offline-activation/step4.png)![](https://streamedian.com/static/img/offline-activation/step5.png)![](https://streamedian.com/static/img/offline-activation/step6.png)![](https://streamedian.com/static/img/offline-activation/step7.png)  
![](https://streamedian.com/static/img/offline-activation/step8.png)![](https://streamedian.com/static/img/offline-activation/step9.png)

![](https://streamedian.com/static/img/offline-activation/remaining-activations.png)

[Steps to online activation](https://streamedian.com/docs/#collapse-ubuntu-online-activation)

[](https://streamedian.com/#downloads)  

![](https://streamedian.com/static/img/online-activation/step2-inv.png)![](https://streamedian.com/static/img/online-activation/step3-inv.png)![](https://streamedian.com/static/img/online-activation/step4-inv.png)![](https://streamedian.com/static/img/online-activation/step5-inv.png)![](https://streamedian.com/static/img/online-activation/step6-inv.png)![](https://streamedian.com/static/img/online-activation/remaining-activations-inv.png)  

### How RTSP proxy works?

RTSP player establish connection with proxy with following protocol:

- Connect to RTSP channel by connecting websocket with "rtsp" protocol specified and get connection id
  
  c>s:
  WSP/1.1 INIT\r\n
  seq: <sequence_id for response tracking>
  host: <RTSP stream host>\r\n
  port: <RTSP stream port>\r\n\r\n
  s>c:
  WSP/1.1 200 OK\r\n
  seq: <sequence_id for response tracking>
  channel: <channel_id>\r\n\r\n
  Error codes >= 400 means error

- Connect to RTP channel by connecting websocket with "rtp" protocol
  
  c>s:
  WSP/1.1 JOIN\r\n
  seq: <sequence_id for response tracking>\r\n
  channel: <channel_id achieved from RTSP socket initialization>\r\n\r\n
  s>c:
  WSP/1.1 200 OK\r\n
  seq: <sequence_id for response tracking>\r\n\r\n
  Error codes >= 400 means error

- Send RTSP commands wrapped into WSP protocol:
  
  c>s:
  WSP/1.1 WRAP\r\n
  seq: <sequence_id for response tracking>\r\n
  \r\n
  
  <RTSP_PROTOCOL_DATA>
  s>c:
  WSP/1.1 200 OK\r\n
  channel: <channel_id>\r\n
  \r\n
  <RTSP_PROTOCOL_RESPONSE>
  Error codes >= 400 means error

- RTP channel should send interleaved data with 4 byte header ($<channel> <size>). Separate RTP is not supported at this moment

![](https://streamedian.com/static/img/ws_rtsp_proxy.png)

### RTSP WS Tunnel Client (supported since version 1.8.4)

For whom this solution will be convenient.  

- Who has video cameras in the local network, but there is no global IP address to access the cameras from the global network.  
- Who does not have the opportunity to open the necessary ports on routers and firewalls hidden behind routers.  
- If the company has a remote warehouse or several offices and production premises located in different places of the city. The ability to encrypt the channel (wss tunnel) will allow scramble your cameras.

WebSocket RTSP Tunnel Client can be installed:  

- to any computer on the local network,  
- to one of the most popular boards, for example, RasperiPi or OrangePi,  
- flash directly into your router (using an alternative firmware).

![](https://streamedian.com/static/img/html5_client_tunel.jpg)

### Distribution scheme for data

![](https://streamedian.com/static/img/distribution_scheme_for_data.png)

#### Configuration for Nginx

server {
    listen 80;
    server_name <domain name>;
    location / {
    root /srv/proxy/;
    index index.html;
    }
    location = /ws/ {
    proxy_pass http://localhost:8080/ws/;
    }
    location = /tunnel/ {
    proxy_pass http://localhost:4000/tunnel/;
    }
}

#### libssl

For running in raspberry may need library "libssl1.0.0" or 1.0.1 To install it insert this line in "/etc/apt/sources.list":

deb http://archive.raspbian.org/raspbian stretch main contrib non-free

Then run following command in respberry terminal:

sudo apt update
sudo apt install libssl1.0.0

#### Controll

Commands to control the tunnel client service

systemctl start rtsp_ws_tunnel_client
systemctl stop rtsp_ws_tunnel_client

#### Config file /etc/rtsp_ws_tunnel_client.ini

before work need setup config parameters /etc/rtsp_ws_tunnel_client.ini

	systemctl stop rtsp_ws_tunnel_client

[General]
//RTSP WS tunnel client client id
client_id=RTSP WS tunnel client
//websocket proxy access token - should be the same as on your proxy side
proxy_token=OWJlN2FiMDMtZGEyMC00NGM1LTg5ZDItOGVlMjM
// websocket proxy address - should look to your ws://
//if wss:// - set up "ssl=on" below
proxy_url=ws://192.168.1.180:8088/tunnel/
// RTSP WS tunnel client plugin dir
plugin_path=/usr/lib/rwtc/
// wss connection off - for ws:// | on - for wss://
ssl=off
[CAMERAS] - list your rtsp sources - should be TCP type
url=rtsp://192.168.1.185:554/h264 example rtsp url
url=rtsp://192.168.1.186:554/h264 example rtsp url
url=rtsp://192.168.1.187:554/h264 example rtsp url
url=rtsp://192.168.1.188:554/h264 example rtsp url
url=rtsp://192.168.1.189:554/h264 example rtsp url

you will see this list on the test page when the page makes the first connection to the proxy after changing the ini file need restart tunnel client service

	systemctl start rtsp_ws_tunnel_client

### Multiple licenses using

Since version 1.8.5 the ws rtsp proxy supports using of multiple licenses simultaneously. To use multiple licenses, write each license file path to the ws_rtsp.ini file and then restart the ws rtsp proxy. Licenses path records in ws_rtsp.ini looks like:

        # path to license file
        license_path=C:\Users\Public\Documents\Streamedian\WS RTSP Proxy Server\wsp.lic
        license_path=C:\Users\Public\Documents\Streamedian\WS RTSP Proxy Server\wsp_two.lic
        license_path=C:\Users\Public\Documents\Streamedian\WS RTSP Proxy Server\wsp_three.lic

### Video playback delay where web page is inactive in the chrome browser

Automatic jump to buffer end for view live video when returning to the web page was added to the test page. When tab switched or window is minimized chrome browser stopping the player and when returning to the web page starting playback from where player was stopped. This may cause video lagging behind the live stream, because the player buffering part of stream. The code below has handle this case.

        // Tab switching and window minimization processing 
        // for browsers that use the chrome rendering engine.
        if (!!window.chrome) {
            document.addEventListener('visibilitychange', function() {
                if(document.visibilityState === 'hidden') {
                    nativePlayer.pause()
                } else {
                    nativePlayer.play();
                    // Automatic jump to buffer end for view live video when returning to the web page. 
                    setTimeout(function() {
                        nativePlayer.currentTime = nativePlayer.buffered.end(0)
                    }, 3000); // Delay for a few seconds is required for the player has time to update the timeline.
                }
            });
        }

Remove this javascript code from the test page to disable automatic jump to buffer end for view live video.

### Machine Learning object recognition (ml5.js library integration)

Together implementation object recognition on video using ml5.js and HTML5 RTSP player. ml5.js is a library that makes machine learning more accessible and performs all image procesing in a browser side. We integrated it with player in the demo [**PLAYER FREE & ml5.js ML**](https://streamedian.com/demo/ml5/) with the Yolo model to detect objects in the video.

#### ml5.js integration based on HTML5 RTSP player test page

p5 and ml5 libraries loading

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.9.0/p5.min.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.9.0/addons/p5.dom.min.js"></script>

<script src="https://unpkg.com/ml5@0.4.3/dist/ml5.min.js"></script>
```

Canvas adding to test page for bounding boxes displaying

```
<div style="position: relative;">
    <video id="test_video" width="720" height="360" muted autoplay style="position: absolute;"></video>
    <canvas id="test_canvas" style="position: absolute;"></canvas>
</div>
```

Javascript code for object detection and bounding bosxes drawing

```
let yolo;
let ctx;
let width;
let height;
function initObjectsDetection(playerId, canvasId, rtspLink) {
    const updateTime = 3000; // Interval in millis between image capture for objects detection
    const video = document.getElementById(playerId);
    const canvas = document.getElementById(canvasId);
    ctx = canvas.getContext('2d');
    width = video.offsetWidth;
    height = video.offsetHeight;
    // Resize canvas
    canvas.width = width;
    canvas.height = height;
    // Load Yolo model
    const ml = new ml5.YOLO(video);
    ml.loadModel().then(function(model) {
        yolo = model;
        // Start RTSP link playback
        setPlayerSource(rtspLink);
        // Set interval for objects detection
        setInterval(objectDetect, updateTime);
    });
}
function objectDetect() {
    yolo.detect(function(err, results) {
        if (results !== undefined) {
            // Draw results on canvas
            draw(results);
        }
    });
}
function draw(results) {
    ctx.clearRect(0, 0, width, height);
    ctx.font = "24px helvetica";
    ctx.textBaseline = "top";
    for (let i = 0; i < results.length; i++) { //Iterating through all results
        // Bounding box drawing
        ctx.strokeStyle = "#2fff00";
        ctx.lineWidth = 1;
        ctx.strokeRect(results[i].x * width, results[i].y * height, results[i].w * width, results[i].h * height);
        // Text drawing last to ensure it's on top
        const textWidth = ctx.measureText(results[i].label).width;
        const textHeight = parseInt("24px helvetica", 10);
        ctx.fillStyle = "#000000";
        ctx.fillText(results[i].label, results[i].x * width, results[i].y * height - 5);
    }
}
```

Object detection initialization calling after streamedian player initialized

```
var player = Streamedian.player('test_video', playerOptions);
var nativePlayer = document.getElementById('test_video');
var statusText = document.getElementById('statusText');
initObjectsDetection("test_video", "test_canvas", 'rtsp://wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mov');
```

[**Demo: PLAYER FREE & ml5.js ML**](https://streamedian.com/demo/ml5/)

[**More about ml5.js**](https://ml5js.org/)

### License activation web API

If you want to license activate from your software, then here is an API for working with our server

[User verification](https://streamedian.com/docs/#collapse-user-verification-api)

[Key assigning to user account](https://streamedian.com/docs/#collapse-key-assign-api)

[Available license list getting](https://streamedian.com/docs/#collapse-get-licenses-api)

[License activation](https://streamedian.com/docs/#collapse-license-activation-api)

[License deactivation](https://streamedian.com/docs/#collapse-license-deactivation-api)

### Statistic

Websocket statistic API provides an opportunity to receive information about license status and open connections between HTML5 RTSP player and the websocket proxy server.

#### Real time statistics

Follow this instruction to start getting real-time statistic about the HTML5 RTSP player connection to the websocket RTSP proxy server.

First step is to connect to the proxy webocket with specifying **"statistic"** subprotocol

ws://localhost:8088/ws/

Note: The webocket rtsp proxy installer installs configuration files for the NGINX and the Apache also. These configuration files tell webserver to listen **8088** port and forwards requests with the path "/ws/" to the **8080** port that the websocket proxy listens by default. So if you don't use webservers or use your own configuration then specify port **8080** for connecting to the webscoket proxy directly.

Then send the next command to websocket to subscribe to update

```
WSP/1.1 SUBSCRIBE
Authorization: c3RyZWFtZWRpYW4=
seq: 1
```

The authorization variable is password in Base64 encoding. The default password is "streamedian". To change password entry new password in the "statistic_password" variable from the ws_rtsp.ini file.

If the password is incorrect you receive message:

```
WSP/1.1 401 Unauthorized
seq: 1
```

Now when the HTML5 rtsp player connecting or disconnecting from the websocket rtsp proxy you will receive an information message from the statistic websocket. This message contains:

- **connectionTime** - Conection time is in epoch timestamp format without millisecond.
- **disconnectionTime** - Disconection time is in epoch timestamp format without millisecond. If the message reason is the "Connection open" this variable absent.
- **reason** - Reason for sending the message.
- **rtsp** - Contains host and port of remote RTSP source.
- **session_id** - Unique session id for determinate users.
- **user** - Contains the user address and requested domain.
- **videoFormat** - Video codec format. h264 or h265.

**User address descriprion:**  
User address is IP of user machine from which the connection request comes.

**Requested domain descriprion:**  
The requested domain is an address that entered into a browser for opening a page with the HTML5 RTSP player. Also the requested domain is an address that is specified during license activating.

**Reason message descriprion:**

- **Connection open** - Successful open connection between the HTML5 rtsp player and the websocekt rtsp proxy.
- **Connection closed** - Connection is closed without error.
- **Too many connections** - Connection is refused because limit of simultaneous watchers is reached.
- **Invalid Domain (credentials)** - The requested domain does not match the address specified when activating the license.
- **License expired** - The license corresponding to this requested domain has expired.
- **Error closing connection** - An error occurred while the stream initializing.
- **Bad handshake** - An error occurred while the stream initializing.

**Example of real-time statistic message:**  
Please check out the example

```
{
    "connectionTime": "1611850234",
    "disconnectionTime": "1611850242",
    "reason": "Connection closed",
    "rtsp": {"host": "demo.<yourdomain>.net", "port": "554"},
    "session_id": "127.0.0.1-6 41",
    "user": {"address": "127.0.0.1", "requestedDomain": "http://127.0.0.1:8088"},
    "videoFormat": "h264"
}
```

A sample code of real-time statistic can be found on the test page.

#### Detailed statistic information

Follow this instruction to getting detailed statistic about licenses and the HTML5 RTSP player connection to the websocket RTSP proxy server.

First step is to connect to the proxy webocket with specifying **"statistic"** subprotocol

	ws://localhost:8088/ws/

Note: The webocket rtsp proxy installer installs configuration files for the NGINX and the Apache also. These configuration files tell webserver to listen **8088** port and forwards requests with the path "/ws/" to the **8080** port that the websocket proxy listens by default. So if you don't use webservers or use your own configuration then specify port **8080** for connecting to the webscoket proxy directly.

Then send the next command to websocket to get detailed statistic info

```
WSP/1.1 GET_INFO
Authorization: c3RyZWFtZWRpYW4=
seq: 1
```

The authorization variable is password in Base64 encoding. The default password is "streamedian". To change password entry new password in the "statistic_password" variable from the ws_rtsp.ini file.

If the password is incorrect you got message:

```
WSP/1.1 401 Unauthorized
seq: 1
```

If request is successful you receive array with licenses information. Each element of array contain information about license, open sessions and number of open sessions.

License information contains:

- **key** - Unique license key. May be empty if proxy satrtup without license.
- **expiresAt** - License expiration date. After this date, only one session may be opened for this license. May contain "Invalid expiration time" when expiration time reading error from the license file.
- **maxWatchers** - Maximum number of simultaneously open sessions.

Sessions information contains array. Each element of array contains:

- **rtsp** - Contains remote rtsp host and port.
- **user** - Contains the user address and requested domain.
- **connectionTime** - Conection time is in epoch timestamp format without millisecond.
- **session_id** - Unique session id for determinate users.
- **videoFormat** - Video codec format. h264 or h265.

**Example response on detailed information request:**  
Please check out the example

```
[
    {
        "license": {
            "key": "277f7886-1ca5-4429-9463-e14a063044cb",
            "expiresAt": "Mon Jul 26 07:00:00 2021\n",
            "maxWatchers": "3"
        },
        "sessions": [
            {
            "rtsp":
                "host": "demo.<yourdomain>.net",
                "port": "554"
            },
            "user": {
                "address": "127.0.0.1",
                "requestedDomain": "http://127.0.0.1:8088"
            },
            "connectionTime": "1611942677",
            "session_id": "127.0.0.1-2 18467",
            "videoFormat": "h264"
            }
        ],
        "sessionNumber": "1"
    }
]
```

A sample code of detailed statistic can be found on the test page.

#### How to save statistics to file

Simple logging examples using python 3 and nodejs

**Python 3**

First step is the webscokets library install

	pip install websockets

Sample python code to write statistic to file

```
#!/usr/bin/env python
import asyncio
import websockets
import base64
def write_to_file(path, response):
    with open(path, '+a', encoding='utf-8') as file:
        file.write(response)
async def statistic():
    uri = 'ws://localhost:8088/ws/'
    password = base64.b64encode(b'streamedian').decode('utf-8')
    path = 'ws_proxy_statistic.txt'
    async with websockets.connect(uri, subprotocols=['statistic']) as websocket:
        cmd = 'WSP/1.1 SUBSCRIBE\nAuthorization: {}\nseq: 1\n\n'.format(password)
        await websocket.send(cmd)
        while True:
            response = await websocket.recv()
            write_to_file(path, response)
asyncio.get_event_loop().run_until_complete(statistic())
```

**Node.js**

Sample nodejs code to write statistic to file

```
const WebSocket = require('ws');
const fs = require('fs');
const stream = fs.createWriteStream("ws_proxy_statistic.txt", {flags:'a'});
const ws = new WebSocket('ws://localhost:8088/ws/', ['statistic']);
const password = Buffer.from('streamedian').toString('base64');
ws.on('open', function open() {
    ws.send(`WSP/1.1 SUBSCRIBE\nAuthorization: ${password}\nseq: 1\n\n`);
});
ws.on('message', function incoming(data) {
    stream.write(data);
     console.log(data);
});
```

### Multi docker license

This license is suitable for docker users that would like to run many docker images at the same time. Because every time when docker container recreated the machine id of this container changes. And it leads to reactivate the license, but the number of license activation is limited. Multi docker license doesn't binding to machine id. So this license remains valid after container recreation. Also you could create any number of containers with one multi docker license file. This license is supported since websocket rtsp proxy **version 1.8.6**

### Enable H265 support

The H265 feature is available immediately after the websocket rtsp proxy installation. Free license supports 3 simultaneously viewed streams available and the test page will work in the local network only. For using global domain name or your web page from global network it's necessaru to activate free or regular license to enable supporting H265 streaming. Please use the free license first to make sure that our product works successfully with your video stream source before purchasing a license. Note that when counting the number of open connections, it does not take into the type of stream.

### Video recording in the HTML5 RTPS player

The HTML5 RTSP player provides API to receive video and audio fragments from the playback stream. API presented by two classes with the same functionality and parallel recording. "continuousRecording" is used for long recording. "eventRecording" is used for video recording when the event occurs.

#### Recorded video processing and downloading

Before start recording is necessary to setup the callback to receive a recorded video. The callback receives two arguments "data" and "prefix". The "data" is a buffer that contains recorded video and audio in the mp4 container. The "prefix" depending on who made the recording, there may be "continuous" or "event". The callback will be called when the recording is stopped or if the recording time is longer than the file length.

Follow the example to setup callback and download recorded video:

```
        // Create the html link element. Further we will use it to download the file
        var link = document.createElement('a');
        // Callback to receive and handle recorded video file
        var dataHandler = function(data, prefix) {
            // Create the Blob so we can download the video as a file
            let blob = new Blob([data], {type: "application/mp4"});
            // Create object link and set it to the HTML link element
            link.href = window.URL.createObjectURL(blob);
            // Set file name
            link.download = `${prefix}_${new Date()}.mp4`;
            // Call click method. Like a user clicked on a download link
            link.click();
        }
        // Options for HTML5 RTSP Player
        var playerOptions = {
            socket: "ws://localhost:8088/ws/",
            // Set callback to receove recorded video
            **dataHandler**: dataHandler,
        };
        // Set the player options to the HTML5 RTSP player
        player = Streamedian.player("VideoElementId", playerOptions);
```

#### Start recording

To start recording call the "record" method with the parameter true. Looks like the example:

        player.continuousRecording.record(true);
        player.eventRecording.record(true);

To stop recording call the "record" method with the parameter false. Also recording will be automatically stopped when the player page close or the player is paused.

#### File length settings

The file length value is the time in milliseconds of one file recording. If the recording time is longer than the file length value, then "datahandler" callback will be called with the recorded video fragment. And the recording will continue for the next video fragment recording. Default file length is 3 minutes.

The file length can be specified in the HTML5 RTSP player config. Looks like the example:

```
        var playerOptions = {
            socket: "ws://localhost:8088/ws/",
            bufferDuration: 30,
            errorHandler: errHandler,
            infoHandler: infHandler,
            dataHandler: dataHandler,
            **continuousFileLength:** 180000, // 3 minutes
            **eventFileLength:** 10000, // 10 seconds
        };
```

Or using the "setFileLength" method. Looks like the example:

        player.continuousRecording.setFileLength(180000); // 3 minutes
        player.eventRecording.setFileLength(10000); // 10 seconds

Note: The file length must be set before the recording starts. Otherwise file length value will not be applied to the current recording.  
Current file length can get from the "fileLength" property. Looks like the example:

        continuousFileLengthInput.value = player.continuousRecording.fileLength;
        eventFileLengthInput.value = player.eventRecording.fileLength;

A sample code of recording and downloading video can be found on the test page.
