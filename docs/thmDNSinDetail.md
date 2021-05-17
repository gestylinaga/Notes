# DNS in Detail

* DNS -- Domain Name System

    * turns IP addresses into URLs:

        * 104.26.10.229 -- tryhackme.com

## Domain Hierarchy

* **TLD** -- **Top-Level Domain**

    - gTLD -- Generic Top Level

        + .com -- commercial purposes

        + .org -- organisations

        + .edu -- education

        + .gov -- government

    - ccTLD -- Country Code Top Level Domain

        + .ca -- based in Canada

        + .co.uk -- based in the United Kingdom

    - [full list of TLDs](https://data.iana.org/TLD/tlds-alpha-by-domain.txt)

* **Second-Level Domain**

    - in 'tryhackme.com' -- the *tryhackme* part

    - limited to 63 characters

    - can only use A-Z, 0-9

    - can use hyphens "-", but cannot start or end with one, or have consecutive hyphens

* **Subdomain**

    - in 'admin.tryhackme.com' -- the *admin* part

    - same restrictions as a Second-Level Domain

    - no limit on number of subdomains -- 'jupiter.servers.tryhackme.com'

        + maximum length still 253 overall characters


## Record Types

* DNS not just for websites

* Common DNS Record Types

    - **A Record**

        + resolve to IPv4 addresses -- 104.46.10.229

    - **AAAA Record**

        + resolve to IPv6 addresses -- 2606:4700:20::681a:be5

    - **CNAME Record**

        + resolve to another domain name

        + store.tryhackme.com -- shops.shopify.com

        + another DNS request would be made to work out new address

    - **MX Record**
    
        + resolve to the address of the servers that handle the email for the domain you're querying

        + alt1.l.google.com -- MX record response for tryhackme.com

        + come with a priority flag

            * this tells the client which order to try the servers

            * useful for if a main server goes down, and an email needs to be sent to a backup server

    - **TXT Record**

        + free text fields where any text-based data can be stored

        + Common Uses:

            * list servers with email authority on behalf of the domain

            * to verify ownership of domain name when signing up for 3rd-party services


## Making Requests

1. your computer checks its local cache 

    - process stops here if you've looked up the address recently

    - if not, a request is sent to your Recursive DNS Server

2. A **Recursive DNS Server**, usually provided by your ISP, checks its own local cache

    - *usually* set by your Internet Server Provider, but you can choose your own

    - if a result is found, the process ends here

    - common for popular/heavily requested sites: Google, Facebook, Twitter, etc...

    - if still not found, a request is made to a root DNS server

3. The **Root DNS Servers** redirects your request to the correct Top-Level Domain Server -- TLD

    - can be seen as the *backbone* of the internet

    - ie tryhackme.com -- the root server would recognise .com and refer you to the correct TLD

4. The **TLD Server** holds the records for where to find the authoritative server

    - Authoritative Server aka *nameserver* for a domain

    - ie: tryhackme.com -- kip.ns.cloudflare.com, and uma.ns.cloudflare.com

    - often multiple nameservers for a domain name to act as backups

5. An **Authoritative DNS Server** stores the records for a particular domain name 

    - also where any updates to a domain's name DNS record would be made

    - the DNS record is sent back to the Recursive DNS Server, to be cached for future requests

    - DNS record is relayed to original client that made the request

    - DNS records all come wih a **TTL** -- Time To Live

        + TTL are represented in seconds 

        + saved locally until you have to look it up again or it *dies*


## Practical

1. CNAME of shop.website.thm
```
nslookup --type=CNAME shop.website.thm

shop.website.thm canonical name = shops.myshopify.com
```

2. TXT record of website.thm
```
nslookup --type=TXT website.thm

website.thm text = "THM{7012BBA60997F35A9516C2E16D2944FF}"
```

3. Numerical Value for the MX record
```
nslookup --type=MX website.thm

website.thm mail exchanger = 30 alt4.aspmx.l.google.com
```

4. IP address for the A record of www.website.thm
```
nslookup --type=A www.website.thm

Name: www.website.thm
Address: 10.10.10.10
```

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
