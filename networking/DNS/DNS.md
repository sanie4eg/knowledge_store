### DNS

**DNS** stands for Domain Name System. DNS resolve name to the IP address and IP address to name.  
**DDNS** stands for Dynamic - DNS or Dynamic Domain Name System. It is a method of updating, in real time, a Domain Name 
System to point to a changing IP address on the Internet. This is used to provide a persistent domain name 
for a resource that may change location on the network.

**A (Address)** Maps a host name to an IP address. When a computer has multiple adapter cards and IP addresses,
 it should have multiple address records.  
**AAAA** same as **A** just for IPv6.  
**Text Record:** The text record can hold arbitrary non-formatted text string. Typically, the record is used
by Sender Policy Framework (SPF) to prevent fake emails to appear to be sent by you.
**CNAME (Canonical Name)** Sets an alias for a host name. For example, using this record, zeta.tvpress.com can have
 an alias as www.tvpress.com.  
**MX (Mail Exchange)** Specifies a mail exchange server for the domain, which allows mail to be delivered
 to the correct mail servers in the domain.  
**NS (Name Server)** Specifies a name server for the domain, which allows DNS lookups within various zones.
 Each primary and secondary name server should be declared through this record.  
**PTR (Pointer)** Creates a pointer that maps an IP address to a host name for reverse lookups.  
**SOA (Start of Authority)** Declares the host that is the most authoritative for the zone and, as such,
is the best source of DNS information for the zone. Each zone file must have an SOA record
(which is created automatically when you add a zone).
SOA records contain a TTL value, used by default in all resource records in the zone. 
SOA records contain the e-mail address of the person who is responsible for maintaining the zone. 
SOA records contain the current serial number of the zone, which is used in zone transfers.  
**SRV (Service record)** The SRV record is a resource record in DNS that is used to identify or point
 to a computer that host specific services i.e Active directory.
**Forward Lookup:** When a name query is send to the DNS server against to IP address, it is generally said
 a forward lookup.  
**Reverse Lookup:** DNS also provides a reverse lookup process,
 enabling clients to use a known IP address during a name query and look up a computer name based on its address. 
  
**Primary zone:** This is the read and writable copy of a zone file in the DNS namespace. This is primary source
 for information about the zone and it stores the master copy of zone data in a local file or in AD DS.   
**Secondary zone:** This is the read only copy of a zone file in the DNS namespace. This is secondary source
 for information about the zone and it get the updated information from the master copy of primary zone.
Provides fault tolerance and load balancing by acting as backup server to primary server.
**Stub zone:** contains a copy of name server and SOA records used for reducing the DNS search orders. 
Provides fault tolerance and load balancing.

**Recursive Query:** This name queries are generally made by a DNS client to a DNS server or by a DNS server that
is configured to pass unresolved name queries to another DNS server, in the case of a DNS server configured
to use a forwarder.
**Iterative Query:** An iterative name query is one in which a DNS client allows the DNS server to return
the best answer it can give based on its cache or zone data. If the queried DNS server does not have an exact match
for the queried name, the best possible information it can return is a referral.
The DNS client can then query the DNS server for which it obtained a referral. 
It continues this process until it locates a DNS server that is authoritative for the queried name, 
or until an error or time-out condition is met.  
**Inverse Query:** A Domain Name System (DNS) query in which a resolver contacts a name server to perform a reverse 
name lookup, requesting a host name for a given IP address. An inverse query is the opposite of the usual DNS 
query - that is, given a host's fully qualified domain name (FQDN), it determines the host's IP address

By Default, If The Name Is Not Found In The Cache Or Local Hosts File client performs a recursive search
through the primary DNS server based on the network interface configuration.

**Port:** The port number of DNS is 53.

**Why TCP and UDP**
DNS and some other services work on both the protocols. Two protocols are somewhat different from each other. 
TCP is a connection-oriented protocol and it requires data to be consistent 
at the destination and UDP is connection-less protocol and doesn't require data to be consistent or don't need 
a connection to be established with host for consistency of data.
 
UDP packets are smaller in size. UDP packets can not be greater then 512 bytes. So any application needs data to be 
transferred greater than 512 bytes require TCP in place. For example, DNS uses both TCP and UDP for valid reasons 
described below. Note that UDP messages are not larger than 512 Bytes and are truncated when greater than this size.  
DNS uses TCP for Zone transfer and UDP for name queries either regular (primary) or reverse. UDP can be used to exchange
small information whereas TCP must be used to exchange information larger than 512 bytes. If a client doesn't get 
response from DNS it must re-transmit the data using TCP after 3-5 seconds of interval.
 
There should be consistency in DNS Zone database. To make this, DNS always transfer Zone data using TCP because TCP 
is reliable and make sure zone data is consistent by transferring the full zone to other DNS servers who 
has requested the data.
 
LDAP always uses TCP - this is true and why not UDP because a secure connection is established between client and server
to send the data and this can be done only using TCP not UDP. UDP is only used when finding a domain controller 
(Kerberos) for authentication. For example, a domain client finding a domain controller using DNS.

DNS uses TCP when the size of the request or the response is greater than a single packet such as with responses 
that have many records or many IPv6 responses or most DNSSEC responses.

The maximum size was originally 512 bytes but there is an extension to the DNS protocol that allows clients to indicate 
that they can handle UDP responses of up to 4096 bytes.
DNSSEC responses are usually larger than the maximum UDP size.
Transfer requests are usually larger than the maximum UDP size and hence will also be done over TCP.