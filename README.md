### Meow.htb

----


    sudo openvpn starting_point... (file)


###### :fire: this is the cmd you use to have the vpn up and running in addition you should be in the current dir for it work.

----

ifconfig

###### :fire: this cmd is used in a new terminal to check if the connection was successful. If it is up and running then the below will be shown.

        tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.10.14.55  netmask 255.255.254.0  destination 10.10.14.55
        inet6 dead:beef:2::1035  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::56f5:4d86:a907:23e5  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 500  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 6  bytes 288 (288.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

        tun1: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.10.14.55  netmask 255.255.254.0  destination 10.10.14.55
        inet6 dead:beef:2::1035  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::7e99:7b:f37f:cf64  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 500  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 240 (240.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

----

ping [IP ADDRESS]

###### :fire: ping the IP address given to you by HTB to test if ICMP packets are being sent and received by the server.

###### :fire: use ctrl + c to end the ping.

----

export IP=10.129.143.150  

###### :fire: the export cmd is used to assisgn the variable (IP) the int IP address hence we will use the var inplace of the IP address.
###### :fire: the cmd is entered directly into the terminal and will be only active in that terminal.
###### :fire: to test use the cmd below:

----

echo $IP

###### :fire: the int IP address will be shown.

-----

---------------------------------------------------	ENUMARATION PHASE ----------------------------------------------------

-----

          man nmap

###### -F : this is for a fast scan (scans fewer ports than the default scan.
###### -sV : this probes open ports to determine the service/version info.
###### -p- : this scans the entire 2^16 ports.
###### -p{<port ranges>} : this scans only specified ports.
###### 	e.g. -p22-24 or -p443 or -p U:53,111,137, T:21-25,80,139,8080,S:9
###### 			where U reps UDP and T reps TCP
###### --min-rate [<number>] : sends packets no slower than <number> per second.
###### -A : enables the detection, version detection, script scanning, and traceroute.
###### -oN : used to create a file of the results from the scan. It is applied after the IP address.
###### -sC : Performs a script scan using the default set of scripts. It requires sudo permission, this is because it is viewed as intrusive.

          nmap -p- --min-rate 5000 -sV $IP -oN initial_scan 

          sudo nmap -p21-24 -sC -sV -A $IP -oN initial_scan_2

----

Target:

23/tcp open   telnet    Linux telnetd

###### :fire: port 23 is open
###### :fire: service is telnet which is a application protocol used interating with remote computers using a virtual terminal connection. 

-----

            telnet $IP

            -login: root

###### :fire: root usually defines the super user (su), other names include:
###### 		                         admininstrator.
###### 		                            admin.

            root@Meow:~# ls

###### :fire: ls : list things in the current directory.
###### :fire: after the cmd we found the flag.txt, snap(dir)
###### :fire: in other scenarios you might be looking for 
######			            user.txt
######			            root.txt


           root@Meow:~# help

###### :fire: self explanatory.

           root@Meow:~# cat flag.txt

###### :fire: looked into the contents of the file : :flag: b40abdfe23665f766f9c61ecba8a4c19. :flag:

----
