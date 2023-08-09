![image](https://github.com/AntIT-1/dns/assets/141161539/4f8deb0c-d7a4-4254-a217-d552e062beac)


</p>

<h1>Building Intuition for DNS </h1>
In this tutorial I will inspect A-records on a DNS server and create an A-record. I wil also touch on CNAME records. 



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>A-Record Exercise</h2>
We can begin by trying to ping “mainframe” from Client-1. Notice that it fails.
If you Nslookup “mainframe” you will notice that it fails as well (no DNS record).There is nothing in the DNS records that will associate "mainframe" to an IP address in the Domain. Thats what a DNS is used for. The A-records are instructions that live in authoritative DNS servers and provide information about a domain.

![image](https://github.com/AntIT-1/dns/assets/141161539/3f04996e-c1d8-4204-b24c-ede8e11eea70)

After entering NSLOOKUP "mainframe", you can see that there is no DNS record for this. We are about to change this.  

![image](https://github.com/AntIT-1/dns/assets/141161539/86548bfa-6155-43a1-aa84-fe9bdf842091)

Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address. This can be done in the Foware lookup zone in the DNS server. 

![image](https://github.com/AntIT-1/dns/assets/141161539/7fbbf9c2-0e24-47d0-a2fe-96258d45106e)

![image](https://github.com/AntIT-1/dns/assets/141161539/99a14386-ed04-4458-b1fb-00447c555a25)

Go back to Client-1 and try to ping it. Observe that it works

![image](https://github.com/AntIT-1/dns/assets/141161539/4c5ceb08-9248-4826-805e-c4b76199d482)

Local DNS Cache Exercise:

Go back to DC-1 and change mainframe’s record address to 8.8.8.8

![image](https://github.com/AntIT-1/dns/assets/141161539/dd118a6a-f286-49df-868e-023fdd3a0abe)


Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address

![image](https://github.com/AntIT-1/dns/assets/141161539/0b9a86f7-40c2-412d-9769-c269024438b0)


Observe the local dns cache (ipconfig /displaydns)

![image](https://github.com/AntIT-1/dns/assets/141161539/2b73a41b-fcd3-435f-8417-f185daec0d7b)




Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty

![image](https://github.com/AntIT-1/dns/assets/141161539/521c3745-0c1c-4655-9f02-29bee543677e)




Attempt to ping “mainframe” again. Observe the address of the new record is showing up since it was changed in the DNS records. 

![image](https://github.com/AntIT-1/dns/assets/141161539/82152922-360b-48b1-8fbc-05b5ab87decc)

<h2>CNAME (Canonical name) Exercise</h2>
A canonical name (CNAME) is a type of Domain Name System (DNS) record that indicates that a domain name is the nickname or alias for another domain name.





Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”


![image](https://github.com/AntIT-1/dns/assets/141161539/ec07008f-e8ea-40c8-948e-d228f57c8c26)

Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record. 

![image](https://github.com/AntIT-1/dns/assets/141161539/ac59ddf3-7987-4204-8250-21d3d1c13180)

The word "search" was resolved to www.google.com because of the CNAME settings we changed. 






















