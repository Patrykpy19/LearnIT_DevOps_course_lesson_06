# Kurs LearnIT DevOps #

## Zadanie domowe ##

# Zadanie 3: Ściągawka typów rekordów #

1. **A -nazwa na adres IPv4**
Przykład zapisu: example.com. 3600 IN A 203.0.113.10
Zastosowanie: domea z przypisanym IPv4
Pułapka: przez to, że można przypisać wiele rekordów do 1 nazwy, serwer zwraca wszystkie w przypadkowej kolejności<br>
 a klient bierze pierwszy może dochodzić do pomyłek

2. **AAAA - nazwa na adres IPv6**
Przykład zapisu: example.com. 3600 IN A <IPv6>
Zastosowanie: domena ma przypisany adres IPv6
Pułapka: jeśli opublikujesz AAAA wskazujący na adres, na którym aplikacja nie nasłuchuje, część użytkowników dostanie losowe opóźnienia lub błędy

3. **CNAME - alias na inną nazwę**
Przykład zapisu: www.example.com. 3600 IN CNAME example.com
Zastosowanie: jeśli masz "pseudonim" dla swojej strony
Pułapka: nie może mieć własnego MX ani TXT; nie wolno umieszać na wierzchołku strefy

4. **MX - dokąd dostarczać pocztę**
Przykład zapisu: example.com. 360 IN MX 10 aspmx.l.google.com
Zastosowanie: masz server pocztowy i ma mieć inną domenę niż serwer
Pułapka: MX wskazuje nazwę a nie adres IP; nazwa dolecowa nie może być CNAME

5. **TXT - dowolny text, w praktyce polityki poczty**
Przykład zapisu: example.com. 3600 IN TXT "v=spf1 include:_spf.google.com ip4:203.0.113.10 ~all"
Zastosowanie: do ochrony przez cyerzbójami (SPF, DKIM,DMARC)
Pułapka: uwaga z wdrozeniem, przeskok od razu do p=reject potrafi wyciąć newsletter, fakturowanie i powiadomienia z CRM naraz

6. **NS - kto jest autorytatywny dla strefy**
Przykład zapisu: example.com. 172800 IN NS  ns1.dostawca.example <br> example.com. 172800 IN NS  ns2.dostawca.example
Zastosowanie: działa jak wskaźnik, mówi gdzie można znaleźć informacje (inny server DNS)
Pułapka: występuje na raz w 2 miejscach; Gdy komplety się różnią, mamy lame delegation:<br>
część resolwerów pyta serwer, który nie uważa się za autorytatywny, i dostaje odmowę. Objaw: domena działa u połowy użytkowników

7. **SOA - metryka strefy**
Przykład zapisu: example.com. 3600 IN SOA ns1.dostawca.example. admin.example.com. (
2026081901 ; serial
7200 ; refresh
1800 ; retry
1209600 ; expire
3600 ) ; minimum

Zastosowanie: występuje w każdej stresie tylko 1 raz i opisuje jej parametry administracyjne
Pułapka:<br>
Zmieniłeś rekord, ale nie zwiększyłeś numeru seryjnego. Serwer główny widzi nową treść,serwery zapasowe nadal serwują starą<br>
i nie mają powodu jej odświeżać. Objaw: zmiana widoczna z jednego serwera DNS, niewidoczna z drugiego, i nikt nie wie dlaczego.<br>

8. **PTR - strefa odwrotna**
Przykład zapisu: 10.113.8.203.in-addr .srpa. 3600 IN PTR mail.example.com
Zastosowanie:<br>
Po co: serwery pocztowe punktują ujemnie pocztę z adresów bez PTR, a jeszcze surowiej taką, gdzie PTR nie zgadza się z rekordem A<br>
(brak FCrDNS — Forward-Confirmed reverse DNS). Jeśli wysyłasz pocztę z własnego serwera, PTR jest obowiązkowy
Pułapka: 

9. **SRV - gdzie działa konretna usługa**
Przykład zapisu: _sip._tcp.example.com. 3600 IN SRV 10 60 5060 sip1.example.com
Zastosowanie: Rekord SRV podaje nie tylko host, ale też port, priorytet i wagę. Nazwa ma sztywny format _usługa._ protokół.domena
Pułapka: Ruch HTTP go nie używa —przeglądarki celowo go ignorują

10. **CAA - kto może wystawić cetyfikat dla tej domeny**
Przykład zapisu: example.com 3600 IN CAA 0 issue "letsebcrypt.org"
Zastosowanie:<br>
Rekord CAA (Certification Authority Authorization) mówi urzędom certyfikacji, kto może wystawić certyfikat dla tej domeny.<br>
Każdy urząd ma obowiązek sprawdzić CAA przed wydaniem i odmówić, jeśli nie jest na liście — to tania bariera przed cudzym certyfikatem na Twoją domenę.<br>
Wpis iodef podaje adres do zgłaszania prób naruszenia
Pułapka:

