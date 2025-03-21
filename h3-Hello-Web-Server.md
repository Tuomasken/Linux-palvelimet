# H3 Hello Web Server


## Harjoituksessa käytetyn koneen parametrejä

- Kannettavan tietokoneen malli: HP Elitebook 840 G4
- Käyttöjärjestelmä: Windows 10 Pro, versio 22H2
- Prosessori: Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz
- Näytönohjain: Inter(R) HD Graphics 620
- RAM: 8 gb


## x)

- https://httpd.apache.org/docs/2.4/vhosts/name-based.html : Nimipohjainen verkkoisännöinti mahdollistaa useamman sivun ylläpitämisen yhdestä IP-osoitteesta, toisin kuin IP-osoitteeseen perustuva isännöinti, joka sallii vain yhden per osoite.
- https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ : Karvinen käy artikkelissaan läpi nimipohjaisen verkkoisännöinnin peruskomennot ja sivustojen määrittämisen.

## a)

Testaan curl-komennolla, että saan yhteyden localhost-osoitteeseen. Tuloksena näkyy itse asettamani yksinkertainen testisivu, jonka tein harjoituksena tunnilla. Eli yhteys toimii.

![Curl_local](H3/Curl_local.png)

## b)

Siirryin cd-komennolla /var/log hakemistoon ja sieltä ajoin komennon "sudo tail -f apache2/other_vhosts_access.log". Tällä näin viimeisen lokin joka syntyi aiemmasta curl-komennostani:

![Curl_log](H3/Curl_log.png)

Tällä tulosteella osiot tarkoittavat seuraavaa:
 -  tutu.example.com on kohdepalvelimen hostname
 -  80 viittaa porttiin mitä kautta pyyntö kulkee. 80 on oletus HTTP-liikenteelle.
 -  127.0.0.1 on pyynnön lähtöosoite, tässä tapauksessa palvelimeni osoite.
 -  [03/Feb/2025:15:04:23 +0200] on aika milloin pyyntö tehtiin.
 -  "GET / HTTP/1.1" tämä on ajettu pyyntö.
 -  200 on HTTP statuskoodi ja tarkoittaa, että pyyntö onnistui.
 -  240 on vastauksen koko tavuissa.

## c)

Lähdin tekemään uutta aloitussivua seuraavalla komennolla. Käytetyt asetukset sain osoitteesta https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/

    $ sudoedit /etc/apache2/sites-available/hattu.example.com.conf

ja loin sivun sisällön komennolla:

    $ mkdir -p /home/tuomaske/publicsites/hattu.example.com
    $ echo tama on hattu.example > /home/tuomaske/publicsites/hattu.example.com/index.html

Tämän jälkeen lisäsin tämän uuden sivun saatavilla olevien sivujen listaan komennolla: 

    $ sudo a2ensite hattu.example.com

Ja poistin aiemman etusivun käytöstä komennolla:

    $ sudo a2dissite tutu.example.com

Boottasin demonin, koska tein siihen muutoksia: 

    $ sudo systemctl restart apache2

Kokeilin curl localhost -komennolla latautuuko etusivu, ei onnistunut (Statuskoodi 403). Kävin katsomassa apache2:n error.log, josta löysin relevantin virheilmoituksen: 

![Error1](H3/Error1.png)

Virheilmoituksesta tunnistin, että siellä on väärä polku listattuna, joten menin tarkastamaan conf-tiedoston. Ja siellä oli kuin olikin jäänyt kirjoitusvirhe. Korjasin sen ja kokeilin uudelleen curl localhost, toimi. Lisäksi kokeilin selaimella: 

![Etusivun_testaus](H3/Testi_etusivu.png)

## e) 

Seuraavaksi kirjoitin yksinkertaisen html-koodin sivulle ja lisäsin sen index.html -tiedostoon, josta etusivu ladataan. Pystyin suoraan testaamaan tehtyjä muutoksia, koska muokkausoikeudet sallittiin aiemmin:

![Etusivun](H3/Etusivu.png)

Tämän jälkeen kävin validoimassa kirjoittamani HTML5:n osoitteessa https://validator.w3.org/#validate_by_input. Ei ongelmia:

![Validointi](H3/Validi.png)

## f)

    $ curl localhost

![Curl](H3/Curl.png)


    $ curl -I localhost 

![CurlI](H3/Curl_I.png)

Toisin kuin GET-pyyntö, HEAD-pyyntö (curl -I) pyytää palvelimelta vain kyseisen sivun otsikkeet. Saadussa tulosteessa näkyy mm. vastauksen statuskoodi (eli esim. onnistuiko pyyntö eli koodi 200), millaista sisältöä kohde on (esim. text/html) ja milloin viimeksi kohteen sisältöä on muokattu.



## Lähteet

1. https://terokarvinen.com/linux-palvelimet/
2. https://httpd.apache.org/docs/2.4/vhosts/name-based.html lainattu 03.02.2025.
3. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address lainattu 03.02.2025.







