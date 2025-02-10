# H4 Maailma kuulee

## a)

Aluksi kävin luomassa tunnuksen palveluun upcloud.com. Tämän jälkeen vuokrasin palvelimen luennolla annettujen speksien mukaisesti. Samassa yhteydessä loin SSH-avainparin isäntävirtuaalikoneella, jolla tunnistautua uudelle virtuaalikoneelle.

![Palvelin](https://github.com/user-attachments/assets/bd180df2-6189-44c1-8616-74a1a8952702)


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

## b)

Asensin apache2 ja korvasin aloitussivun sanalla "Testi":

    $ sudo apt-get -y install apache2
    $ echo "Testi"|sudo tee /var/www/html/index.html

Testasin, että aloitussivu on muuttunut:

![Aloitussivu](https://github.com/user-attachments/assets/cbaf06c8-34e7-4b4f-a7e7-12afbeaa7995)
