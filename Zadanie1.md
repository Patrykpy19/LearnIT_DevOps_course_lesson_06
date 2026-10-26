# Kurs LearnIT DevOps #

## Zadanie domowe ##

# Zadanie 1: Raport diagnostyczny domeny #

**Lets check local resolver:**

``patryk@patryk-GL62M-7RDX:~$ dig example.com``

; <<>> DiG 9.18.39-0ubuntu0.24.04.8-Ubuntu <<>> example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7846
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;example.com.			IN	A

;; ANSWER SECTION:
example.com.		224	IN	A	104.20.23.154
example.com.		224	IN	A	172.66.147.243

;; Query time: 17 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sun Oct 25 23:38:14 CET 2026
;; MSG SIZE  rcvd: 72

**And public resolver:**

``patryk@patryk-GL62M-7RDX:~$ dig @8.8.8.8 example.com``

; <<>> DiG 9.18.39-0ubuntu0.24.04.8-Ubuntu <<>> @8.8.8.8 example.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23601
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;example.com.			IN	A

;; ANSWER SECTION:
example.com.		300	IN	A	172.66.147.243
example.com.		300	IN	A	104.20.23.154

;; Query time: 43 msec
;; SERVER: 8.8.8.8#53(8.8.8.8) (UDP)
;; WHEN: Sun Oct 25 23:40:23 CET 2026
;; MSG SIZE  rcvd: 72

//got same thing, looks good//

____________________________________________________________________________________________
**Checking trace:**

``patryk@patryk-GL62M-7RDX:~$ dig example.com +trace``

; <<>> DiG 9.18.39-0ubuntu0.24.04.8-Ubuntu <<>> example.com +trace
;; global options: +cmd
.			81522	IN	NS	e.root-servers.net.
.			81522	IN	NS	f.root-servers.net.
.			81522	IN	NS	g.root-servers.net.
.			81522	IN	NS	h.root-servers.net.
.			81522	IN	NS	i.root-servers.net.
.			81522	IN	NS	j.root-servers.net.
.			81522	IN	NS	k.root-servers.net.
.			81522	IN	NS	l.root-servers.net.
.			81522	IN	NS	m.root-servers.net.
.			81522	IN	NS	a.root-servers.net.
.			81522	IN	NS	b.root-servers.net.
.			81522	IN	NS	c.root-servers.net.
.			81522	IN	NS	d.root-servers.net.
;; Received 239 bytes from 127.0.0.53#53(127.0.0.53) in 16 ms

com.			172800	IN	NS	a.gtld-servers.net.
com.			172800	IN	NS	b.gtld-servers.net.
com.			172800	IN	NS	c.gtld-servers.net.
com.			172800	IN	NS	d.gtld-servers.net.
com.			172800	IN	NS	e.gtld-servers.net.
com.			172800	IN	NS	f.gtld-servers.net.
com.			172800	IN	NS	g.gtld-servers.net.
com.			172800	IN	NS	h.gtld-servers.net.
com.			172800	IN	NS	i.gtld-servers.net.
com.			172800	IN	NS	j.gtld-servers.net.
com.			172800	IN	NS	k.gtld-servers.net.
com.			172800	IN	NS	l.gtld-servers.net.
com.			172800	IN	NS	m.gtld-servers.net.
com.			86400	IN	DS	19718 13 2 8ACBB0CD28F41250A80A491389424D341522D946B0DA0C0291F2D3D7 71D7805A
com.			86400	IN	RRSIG	DS 8 1 86400 20261107170000 20261025160000 8763 . rlMETFQkOqIQo6NXPgKcYe8NuIpWBIdI3iEsF+OcGB88f025PUDs0uXk UZUsq/NS8c3cR/TdqBC3nQCkkAI5p797q1cSRxPw4eq1O009334u2dCO US8I3K2PFJyi8SFs23xe5Mwu8PyVsNg2zI/QYmdHEzICRwpUwi1g0lAR cxXpjBX7K1OdpSMnTclzcMkH6luzAtG3LQNf3bvF+qRX1iFZjttmdN/g +OU3j/tFbHZ+iQt0JCuNlNHPOS26QDim2iHoNxHQMGykM9KyfjRFX71X AiIOq0WmC3Mbmyc/whjJX6oaynVEqQAd3UkmHG59FwVcwPCysPfVxgKX 2gHJvA==
;; Received 1171 bytes from 170.247.170.2#53(b.root-servers.net) in 33 ms

example.com.		172800	IN	NS	hera.ns.cloudflare.com.
example.com.		172800	IN	NS	elliott.ns.cloudflare.com.
example.com.		86400	IN	DS	2371 13 2 C988EC423E3880EB8DD8A46FE06CA230EE23F35B578D64E78B29C3E1 C83D245A
example.com.		86400	IN	RRSIG	DS 13 2 86400 20261101013317 20261025002317 65344 com. 74li2aMojC1BxjCRiVarr1Lafmcb5oM3ITHEvoINP7fWqmR12KSqFVSg TbYVulxc8QOP/W7AsgljkS7t8s1F7g==
;; Received 506 bytes from 192.35.51.30#53(f.gtld-servers.net) in 33 ms

example.com.		300	IN	A	172.66.147.243
example.com.		300	IN	A	104.20.23.154
example.com.		300	IN	RRSIG	A 13 2 300 20261026234130 20261024214130 34505 example.com. QC4KH8wEEwwucc0+rGVi6e5Ism6fkVgiK3h8VtkG40QNWZJ38hN7VPf+ rsfmBqi5Y46RTvJ+z2VQPsDPNoHckw==
;; Received 179 bytes from 2a06:98c1:50::ac40:20a2#53(hera.ns.cloudflare.com) in 28 ms


**b-root answered**
```DS      19718 13 2 8ACBB0CD28F41250A80A491389424D341522D946B0DA0C0291F2D3D7 71D7805A
com.                    86400   IN      RRSIG   DS 8 1 86400 20261107170000 20261025160000 8763 . rlMETFQkOqIQo6NXPgKcYe8NuIpWBIdI3iEsF+OcGB88f025PUDs0uXk UZ>
;; Received 1171 bytes from 170.247.170.2#53(b.root-servers.net) in 33 ms
```

**that f.gtld-server.net**
```
DS      2371 13 2 C988EC423E3880EB8DD8A46FE06CA230EE23F35B578D64E78B29C3E1 C83D245A
example.com.            86400   IN      RRSIG   DS 13 2 86400 20261101013317 20261025002317 65344 com. 74li2aMojC1BxjCRiVarr1Lafmcb5oM3ITHEvoINP7fWqmR12KSqFV>
;; Received 506 bytes from 192.35.51.30#53(f.gtld-servers.net) in 33 ms
```

**knows this domain**
```
example.com.            300     IN      A       172.66.147.243
example.com.            300     IN      A       104.20.23.154
example.com.            300     IN      RRSIG   A 13 2 300 20261026234130 20261024214130 34505 example.com. QC4KH8wEEwwucc0+rGVi6e5Ism6fkVgiK3h8VtkG40QNWZJ38>
;; Received 179 bytes from 2a06:98c1:50::ac40:20a2#53(hera.ns.cloudflare.com) in 28 m
s

```
______________________________________________________________________________________________________________

**Checing MX record**

```
patryk@patryk-GL62M-7RDX:~$ dig example.com MX +noall +answer
example.com.		300	IN	MX	0 .
```
//Clearly shows that is has no mailing server//

______________________________________________________________________________________________________________

**Checkign website's https port**

```
patryk@patryk-GL62M-7RDX:~$ nc -zv example.com 443
Connection to example.com (2606:4700:10::6814:179a) 443 port [tcp/https] succeeded!
patryk@patryk-GL62M-7RDX:~$
```

**Checking website's http port**

```
patryk@patryk-GL62M-7RDX:~$ nc -zv example.com 80
Connection to example.com (2606:4700:10::6814:179a) 80 port [tcp/http] succeeded!
patryk@patryk-GL62M-7RDX:~$ 

```
//Looks good to me and someone is lying//

____________________________________________________________________________________________________________

**Lets check HTTP respond with curl**

```
patryk@patryk-GL62M-7RDX:~$ curl -I https://example.com
HTTP/2 200 
date: Sun, 25 Oct 2026 23:18:55 GMT
content-type: text/html; charset=utf-8
server: cloudflare
last-modified: Sat, 24 Oct 2026 11:34:40 GMT
allow: GET, HEAD
accept-ranges: bytes
age: 1
cf-cache-status: HIT
cf-ray: a504f1770c242954-FRA
alt-svc: h3=":443"; ma=86400

patryk@patryk-GL62M-7RDX:~$
```
//Got 200, it shows it is good//

What to do - check computer of a person who told what is not working
