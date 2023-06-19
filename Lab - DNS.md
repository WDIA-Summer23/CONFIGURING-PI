## DNS

### Objectives

- An online nslookup tutorial can be found and should be read before doing the lab at **`https://www.thegeekstuff.com/2012/07/nslookup-examples/`**
- In this lab, you perform some packet sniffing on DNS packets and you use the command line utility **`nslookup`** to simulate recursive queries. This lab borrows ideas of labs from **`http://en.wikiversity.org`**
- Note that your computer must be connected to the Internet to do this lab.

### Task 1 - Using nslookup

Start a terminal window on the Pi.

``
nslookup google.ca
```

**1. What are the IP address listed for `google.ca`?**

````the ip address are  172.217.13.99

``` 2607:f8b0:4020:805::2003

```
nslookup -type=ns google.com
```

**2. What are the name servers listed for this domain name?**

ns1.google.com
ns2.google.com
ns3.google.com
ns4.google.com

nslookup -type=soa google.com
```

**3. What is the start of authority information listed for this zone?**

origin = ns1.google.com
mail addr = dns-admin.google.com
serial = 541358519
refresh = 900
retry = 900
expire = 1800
minimum = 60```

```

```
nslookup -type=mx google.com
```

**4. What are the mail exchangers listed for this domain name?**

```
mail exchanger = 10 smtp.google.com.
```



### Task 2 - Domain algonquincollege.com

Redo Task 1 on domain **`algonquincollege.com`**

**5. What are the IP address listed for `algonquincollege.com`?**

```
Address: 54.86.119.60
```

**6. What are the name servers listed for this domain name?**

```
origin = ns5.algonquincollege.com
```

**7. What is the start of authority information listed for this zone?**

```
origin = ns5.algonquincollege.com
mail addr = fwadm.algonquincollege.com
serial = 2023053001
refresh = 3600
retry = 3600
expire = 1209600
minimum = 3600
```

**8. What are the mail exchangers listed for this domain name?**

```
mail exchanger = 10 algonquincollege-com.mail.protection.outlook.com.
```



### Task 3 - Recursive query

Open a terminal window

```
nslookup algonquincollege.com
```

**9. What is the IP address listed?**

```
a.gtld-servers.net internet address = 192.5.6.30
b.gtld-servers.net internet address = 192.33.14.30
c.gtld-servers.net internet address = 192.26.92.30
d.gtld-servers.net internet address = 192.31.80.30
e.gtld-servers.net internet address = 192.12.94.30
f.gtld-servers.net internet address = 192.35.51.30
g.gtld-servers.net internet address = 192.42.93.30
h.gtld-servers.net internet address = 192.54.112.30
i.gtld-servers.net internet address = 192.43.172.30
j.gtld-servers.net internet address = 192.48.79.30
k.gtld-servers.net internet address = 192.52.178.30
l.gtld-servers.net internet address = 192.41.162.30
m.gtld-servers.net internet address = 192.55.83.30
```

To simulate a recursive query:

```
nslookup -norecurse -type=ns com. a.root-servers.net
```

The **`-norecurse`** option forces **`nslookup`** to issue a non-recursive or iterative query. This is the type of query that DNS servers typically issue to other DNS servers.

Observe the results. Notice the name servers listed for the **`com`** domain.

**10. What is the first `com` name server IP address returned?**

```
192.5.6.30
```



```
nslookup -norecurse -type=ns algonquincollege.com <com. name server>
```

where **`<com. name server>`** is the **`com`** name server IP address listed .

Observe the results.

**11. What are the DNS servers listed for the `algonquincollege.com` domain.**

```
algonquincollege.com nameserver = ns5.algonquincollege.com.
algonquincollege.com nameserver = ns3.algonquincollege.com.
```

Select the first **`algonquincollege.com`** name server IP address returned.

```
nslookup -norecurse www.algonquincollege.com <algonquincollege.com. name server>
```

where **`<algonquincollege.com. name server>`** is the first **`algonquincollege.com`** name server IP address listed.

Observe the results.

**12. What is the IP returned?**

```
nslookup -norecurse www.algonquincollege.com 54.86.119.60
```

**13. Is it the same IP as the IP returned question 9?**

```no
```



### Task 4- Packet sniffing

This step is to be done on your laptop.

1. Start **`Wireshark`**.
2. Start a new capture on your live interface card.
3. Start a wireshark capture by clicking on the shark fin icon.
4. Open a Terminal window.
5. Use **`nslookup`** to issue some dns queries.
6. Stop the capture by clicking the shark fin icon.
7. In filter box, type DNS to filter traffic to DNS query
8. Take some time to explore DNS traffic in the different panels.
9. **Make a screen shot of the packet capture DNS.jpg .**

Upload the screenshot and this file with your answers to GitHub.

