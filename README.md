1. Set up your lab account
  * [0.1 Set up an account on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-1-setup-account.md)
  * [0.2 Reserve a simple network on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-2-reserve-and-login.md)
  * [0.3 Inspect network interfaces](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-3-network-interfaces.md)
  * [0.4 Working on remote hosts](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-4-working-on-remote-hosts.md)
  * [0.5 Save data and delete resources on GENI](https://github.com/ffund/tcp-ip-essentials/blob/master/lab0/1-5-delete-resources.md)
2. Network reconnaissance
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
