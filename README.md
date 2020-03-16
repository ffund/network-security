1. Set up your lab account
  * [0.1 Set up an account on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-1-setup-account.md)
  * [0.2 Reserve a simple network on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-2-reserve-and-login.md)
  * [0.3 Inspect network interfaces](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-3-network-interfaces.md)
  * [0.4 Working on remote hosts](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-4-working-on-remote-hosts.md)
  * [0.5 Save data and delete resources on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-5-delete-resources.md)
2. [Network reconnaissance](https://witestlab.poly.edu/blog/network-reconnaissance-and-vulnerability-assessment/)
  * Answer the questions in the "Exercise" section. 
3. [Redirect traffic to a wrong or fake site with DNS spoofing on a LAN
](https://witestlab.poly.edu/blog/redirect-traffic-to-a-wrong-or-fake-site-with-dns-spoofing-on-a-lan/). 
  * Answer the questions in the "Exercise" section. 
  * Also answer the following questions: 
      * (1) If we hadn't put that big "FAKE" notice over the logo, would you be able to detect the DNS spoofing attack on loading the bank's web page in your browser? Explain. 
      * (2) The Diamond Banking website lets users input their username and password on a form on a web page that is loaded over HTTP. But when the user presses "Login", the form sends the username and password to a page that is loaded over HTTPS, i.e. the username and password are sent over an encrypted connection. Explain why this is not sufficient to protect the users' login information. What kind of attack are users left vulnerable to? How would using HTTPS for the entire site protect users against this kind of attack? 
      * (3) Would DNSSEC protect against this kind of attack? Explain your answer.
4. Attacks on WiFi confidentiality: [Passive sniffing](https://witestlab.poly.edu/blog/passive-sniffing-in-802-11-networks/) and [MITM attack](https://witestlab.poly.edu/blog/conduct-a-simple-man-in-the-middle-attack-on-a-wifi-hotspot/). 
  * Answer the questions in the "Exercise" sections.
  * Also answer the following question: In the passive sniffing attack, Mallory needs to capture the 4-way handshake in order to read user data on a WPA network. But in the MITM attack on WPA, Mallory did not capture the 4-way handshake, but was still able to read sensitive user data. How did Mallory bypass WPA confidentiality in this attack?
5. [Layer 7 DoS attack with slowloris](https://witestlab.poly.edu/blog/slowloris/). Answer the following questions:
  * Show the plot of connections vs. time in your experiment for three scenarios: no mitigation, mitigation using firewall, and using the Apache web server.
  * In the plot of connections vs. time in the firewall scenario: how do we see the effect of the firewall? 
  * With the firewall in place, the `slowhttptest` plot still shows that service is not available - does this mean that the attack was effective and legitimate users cannot connect to the web server?
  * Firewalls can be problematic when they interfere with legitimate application use. Sometimes, many hosts might share the same IP address (such as with NAT). How would the firewall strategy used in the lab to prevent the slowloris attack affect legitimate users in this scenario?
6. [Anonymous Routing of Network Traffic Using Tor](https://witestlab.poly.edu/blog/anonymous-routing-of-network-traffic-using-tor/)
  * List the sequence of Tor relays used as a circuit in your experiment, with their IP addresses. Explain how you used `nload`, `ifconfig` and Tor Arm to identify the circuit, and show evidence from the output of these applications.
  * You captured an HTTP GET request for `file.txt` from the client to the web server, at multiple points in the network: (1) on the client before it was passed to the SOCKS proxy, (2) on the router between the client and the entry relay, (3) between the entry relay and middle relay, (4) between the middle relay and exit relay, and (5) between the exit relay and the web server. At each of these points, was the HTTP GET request encrypted? What was the source and destination IP addresss on the packet? Show the specific packet from each packet capture that supports your answer.
  * Which of these statements are true and which of them are false? Show evidence from your experiment to support your answer. (1) When the client routes traffic through the Tor network, the server cannot tell the true IP address of the client. (2) When the client routes traffic through the Tor network, the packet payload is encrypted until it reaches the server. (3) None of the Tor relays knows the true IP address of the client. (4) None of the Tor relays knows the IP address of all three relays in the Tor circuit. (5) None of the Tor relays knows both the true IP address of the client, AND the true IP address of the server. (6) When using the Tor network in this experiment, the client does not need to know the true IP address of the server.


