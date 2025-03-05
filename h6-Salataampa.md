# H6 Salataampa


## Harjoituksessa käytetyn koneen parametrejä

- Kannettavan tietokoneen malli: HP Elitebook 840 G4
- Käyttöjärjestelmä: Windows 10 Pro, versio 22H2
- Prosessori: Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz
- Näytönohjain: Inter(R) HD Graphics 620
- RAM: 8 gb



## x)

Let's Encrypt 2024 https://letsencrypt.org/how-it-works/ :

- Let's Encrypt tarjoaa automatisoidun HTTPS-sertifioinnin verkkosivuille.
- Tämä tapahtuu asentamalla sertifikaatin hallintatyökalu verkkopalvelimelle, joka 1) todistaa CA:lle, että verkkopalvelin omistaa käsiteltävän verkkodomainin, 2) tämän jälkeen hallintatyökalu voi pyytää, uusia ja hylätä sertifikaatin.

Lange 2024: Lego: Obtain a Certificate https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server

-

The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample

-


## a) 

Tässä osiossa lähden hankkimaan sertifikaattia domainilleni Let's Encrypt sertifikaattipalvelulta.
Aluksi tarkistin, että toimiihan sivustoni vielä. Tämän tein käynnistämällä uudelleen apache2:n, eli ts. "potkaisin demonia", komennolla

    $ Sudo systemctl restart apache2

Tämän jälkeen kävin isäntäkoneella katsomassa toimiiko sivut vielä.

![image](https://github.com/user-attachments/assets/a80a7ec9-e4cb-46cd-abf9-3ee2226e85ee)

Sivut toimivat kuten pitääkin, eli nyt meillä on varmuus, että lähdemme tulevaan tehtävänosioon toimivalta pohjalta. Tämä auttaa mahdollisten ongelmien diagnostiikassa rajaamalla mahdolliset syyt ensisijaisesti muutoksiin, mitä tullaan tekemään tehtävän yhteydessä.

Lähdin asentamaan LEGO:a, mikä on "Let’s Encrypt client and ACME library written in Go" (LEGO 2025). Aluksi päivitin saatavilla olevat paketit varmistaakseni, että asennan uusimman LEGO:n version, sitten asensin sen:

    $ sudo apt-get update
    $ sudo apt-get install lego

Seuraavaksi loin LEGOlle kansion tuomaske-käyttäjän alle ja tarkistin, että se onnistui:

![image](https://github.com/user-attachments/assets/ec3af4fc-7e14-467a-bd02-544b2e2fb0ee)

Loin aluksi sertifikaatin Let's Encrypting tarjoamaan staging-ympäristöön testaamista varten. Tähän käytin komentoa, jonka pohjan sain osoitteesta https://terokarvinen.com/2024/linux-palvelimet-2024p1-alkusyksy-ici003as2a-3010/ (Karvinen 2025).

![image](https://github.com/user-attachments/assets/d57b07c8-3288-4e87-9bac-5b13f2187943)



    




