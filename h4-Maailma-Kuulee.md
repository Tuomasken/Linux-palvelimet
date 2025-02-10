# H4 Maailma kuulee


## Harjoituksessa käytetyn koneen parametrejä

- Kannettavan tietokoneen malli: HP Elitebook 840 G4
- Käyttöjärjestelmä: Windows 10 Pro, versio 22H2
- Prosessori: Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz
- Näytönohjain: Inter(R) HD Graphics 620
- RAM: 8 gb



## x)

Susanna Lehdon artikkeli https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/ tiivistetysti:

- Kyseessä on tämän H4-harjoituksen esimerkkiraportti
- Kyseisessä raportissa Lehto käy läpi pilvipalvelun vuokraamisen, domainnimen vuokraamisen, uuden palvelimen alkutoimet ja kotisivun muuttamisen.
- Lisäksi raportissa oli käyty läpi murtautumisyrityksien tarkastelu komennolla:
  
        $ sudo less /var/log/auth.log | grep log


Tero Karvisen (2012) artikkeli https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/

- Artikkelissa Karvinen käy läpi uuden palvelimen alkutoimia, kuten palomuurin käyttöön otto, salittujen porttien asettaminen, uuden käyttäjän luominen, root-käyttäjän lukitseminen.
- Lisäksi hän lyhyesti kertoo miten hankkia oma domainnimi.
## a)

Aluksi kävin luomassa tunnuksen palveluun upcloud.com. Tämän jälkeen vuokrasin palvelimen luennolla annettujen speksien mukaisesti.

![Palvelin](https://github.com/user-attachments/assets/bd180df2-6189-44c1-8616-74a1a8952702)

Samassa yhteydessä loin SSH-avainparin isäntävirtuaalikoneella, jolla tunnistautua uudelle virtuaalikoneelle. Lisäksi kävin kopioimassa sen palvelimen asennusta varten:

        $ ssh-keygen
        $ micro tuomaske/.ssh/id_rsa.pub # Kopioin tekstisisällön Ctrl-C komennolla

## b)


Kirjauduin virtuaalikoneellani palvelimelle ja aloitin alkutoimet. Asensin aluksi tulimuurin ja muita hyödyllisiä ohjelmia komennoilla

    $ sudo apt-get update
    $ sudo apt-get -y install micro bash-completion openssh-client wget curl ufw

Tämän jälkeen konfiguroin sallitut portit tulimuuriin ja laitoin sen päälle komennoilla:

    $ sudo ufw allow 22/tcp; sudo ufw enable; sudo ufw allow 80/tcp

Seuraavaksi loin uuden käyttäjän, jolla on sudo-oikeudet. Lisäksi kopioin sille SSH-asetukset ja vaihdoin tuomaske-käyttäjän kyseisten tiedostojen omistajaksi:

    $ sudo adduser tuomaske
    $ sudo adduser tuomaske sudo
    $ sudo cp -rvn /root/.ssh/ /home/tuomaske/
    $ sudo chown -R tuomaske:tuomaske /home/tuomaske/

Tämän jälkeen palasin exit-komennolla paikalliselle virtuaalikoneelle, ja kirjauduin palvelimelle uudelle käyttäjälle. Kirjauduttuani ongelmitta tuomaske-käyttäjänä, suljin root-tunnuksen ja poistin sen SSH-oikeudet:

    $ sudo usermod --lock root
    $ sudo mv -nv /root/.ssh /root/DISABLED-ssh/

## c)

Asensin apache2 ja korvasin aloitussivun sanalla "Testi":

    $ sudo apt-get -y install apache2
    $ echo "Testi"|sudo tee /var/www/html/index.html

Testasin, että aloitussivu on muuttunut:

![Aloitussivu1](https://github.com/user-attachments/assets/cbaf06c8-34e7-4b4f-a7e7-12afbeaa7995)

![Aloitussivu2](https://github.com/user-attachments/assets/6a7b529c-08bb-49d5-93b0-15b56cd3bf6c)



## Lähteet

1. https://terokarvinen.com/linux-palvelimet/ Lainattu 10.02.2025
2. https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/ Lainattu 10.02.2025
3. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ Lainattu 10.02.2025

