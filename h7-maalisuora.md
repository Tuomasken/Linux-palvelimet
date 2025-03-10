# H7 Maalisuora


## Harjoituksessa käytetyn koneen parametrejä

- Kannettavan tietokoneen malli: HP Elitebook 840 G4
- Käyttöjärjestelmä: Windows 10 Pro, versio 22H2
- Prosessori: Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz
- Näytönohjain: Inter(R) HD Graphics 620
- RAM: 8 gb



## a)

Tässä harjoituksessa testaan eri ohjelmointikielien ajamista linux-ympäristössä.

### Python 3

Aluksi tarkastin onko Python3 jo asennettuna koneella komennolla (lähde https://www.geeksforgeeks.org/how-to-install-python-on-linux/)

    $ python3 --version

Ja olemassa oleva versio löytyi

![image](https://github.com/user-attachments/assets/99f5e1ff-2003-4c29-a18f-6bc4b64e28a1)

Ja vaikka kyseessä on verrattain tuore virtuaalikone, päivitin vielä varmuuden vuoksi paketit seuraavilla komennoilla (tässä kesti noin 5 minuuttia)

    $ sudo apt-get update
    $ sudo apt-get upgrade

Seuraavaksi kokeilin pythonia artikkelin https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/ ohjeiden mukaisesti:

Loin python-tiedoston ja ajoin sen seuraavilla komennoilla:

    $ echo "print(\"Hei maailma\")" > heimaailmapy.py
    $ python3 heimaailmapy.py

![image](https://github.com/user-attachments/assets/702ebc04-1950-4465-b015-96c79b13ee38)


### Bash

Tarkistin onko Bash asennettuna:

    $ bash --version

Löydettyäni Bashin asennettuna loin sh-tiedoston seuraavilla komennoilla:

    $ echo "echo \"Hei maailma\"" > heimaailmabash.sh
    $ bash heimaailmabash.sh


![image](https://github.com/user-attachments/assets/739234b0-48c8-4e06-a6cd-0bd7984212b9)


### Java


Seuraavaksi lähdin kokeilemaan javaa. En löytänyt sitä asennettuna, joten etsin openjdk (java-implementaatiota jota halusin käyttää) komennolla:

    $ sudo apt-cache search openjdk

Ja valitsin listasta vaihtoehdon:

![image](https://github.com/user-attachments/assets/63b00807-2290-4972-ae47-9cc9c1489f71)

Jonka asensin komennolla:

    $ sudo apt-get install openjdk-17-jdk

Sitten loin microlla java-tiedoston heimaailmajava.java, johon kirjoitin seuraavan koodinpätkän ja sen jälkeen ajoin sen:

    public class heimaailmajava {
     public static void main(String[] args)
     {
     System.out.println("Hei maailma");
     }
    }

![image](https://github.com/user-attachments/assets/b6eef5a8-d43e-4cdd-bf75-37bde4b0755b)


## c)

Tässä harjoituksen osiossa lähdin luomaan shell-komentoa, jota kaikki käyttäjät voivat käyttää. 

Aluksi loin sh-tiedoston:

    $ micro testishelli.sh

Ja kirjoitin sinne "date" ja "uptime" komennot. Testishelli.sh sisältö näytti lopulta tältä:

![image](https://github.com/user-attachments/assets/2116291e-77ea-4c0e-8df0-c8cb1fbe8b59)

Alun komento !#/usr/bin/bash kertoo ajettavalle shell-komennolle, mitä tulkkausohjelmaa sen lukemiseen käytetään. Luotuani komennon testasin sitä:

![image](https://github.com/user-attachments/assets/8e3535cd-ec7e-4d18-ab84-17ac55323348)

Tämän jälkeen lähdin muuttamaan sen käyttöoikeuksia, niin että kaikki käyttäjät voivat ajaa sen. Jonka jälkeen kopioin sen /usr/local/bin/ polkuun, jossa se on kaikkien käyttäjien saatavilla. Sen jälkeen poistin alkuperäisen shell-komennon polusta /home/tuomaske:

        $ chmod ugo+x /home/tuomaske/testishelli.sh
        $ sudo cp testishelli.sh /usr/local/bin/
        $ rm testishelli.sh

Ja testasin nyt uudelleen komentoa:

![image](https://github.com/user-attachments/assets/3e1e6fe5-a8f1-4ad7-9c7d-c3fa3abb1d81)


## d)

Tässä osiossa lähden suorittamaan labraharjoitusta https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-3-uusi-ops-alkukevaalla-2017-p1/

Lähdin aluksi luomaan tehtävänannon mukaisesti kotisivuja käyttäjille Jorma Mähkylä, Pekka Hurme, Ronaldo Smith, Håkan Petersson, Einari Mikkonen, Einari Vähäkäähkä, Eija Vähäkäähkä.

Loin https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ ohjeiden mukaisesti uuden conf-tiedoston komennolla:

    $ sudoedit /etc/apache2/sites-available/mahkyla.kurssikuru.com.conf

Näin luotuun  tiedostoon kirjoitin 

![image](https://github.com/user-attachments/assets/346af22d-9611-4307-92cc-e5b921628c72)

Tämän jälkeen kopioin tämän tiedoston kaikille eri käyttäjille seuraavaa komentomallia käyttäen:

    $ sudo cp mahkyla.kurssikuru.com.conf smith.kurssikuru.com.conf

Tässä vaiheessa hyvän muistin aikana poistin aiemman sivun käytössä olevista sivuista komennolla (ja potkaisin demonia):

    $ sudo a2dissite hattu.example.com.conf
    $ sudo systemctl restart apache2

Seuraavaksi siirryin muokkaamaan kaikkia conf-tiedostoja oikeaan muotoon. Komennolla a2ensite lisäsin kaikki uudet sivut saatavilla olevien sivujen joukkoon. Jonka jälkeen potkaisin taas demonia. Seuraavaksi siirryin polkuun /home/tuomaske/publicsites/ luomaan jokaiselle sivulle oman kansion ja muokkaamaan niihin index.html tiedostot tehtävänannon mukaiseksi. 

Tämän jälkeen simuloin nimipalvelua muokkaamalla /etc/hosts ja lisäämällä sinne tekemäni sivut:

![image](https://github.com/user-attachments/assets/e612070b-935d-4a44-b39f-d613196b4296)

Sitten aktivoin palomuurin ja tein siihen porttiin 80 reiän:

    $ sudo ufw enable
    $ sudo ufw allow 80/tcp

Jonka jälkeen kokeilin kaikkia luotuja sivuja niiden osoitteella ja ne toimivat. Esimerkkinä Einari Vähäkäähkän sivu:

![image](https://github.com/user-attachments/assets/1ce3fc83-09cb-43f9-a9af-a3b162867a7e)


## Lähteet

1. https://terokarvinen.com/linux-palvelimet Lainattu 10.03.2025
2. https://www.geeksforgeeks.org/how-to-install-python-on-linux/ Lainattu 10.03.2025
3. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/ Lainattu 10.03.2025
4. https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-3-uusi-ops-alkukevaalla-2017-p1/ Lainattu 10.03.2025
5. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ Lainattu 10.03.2025














