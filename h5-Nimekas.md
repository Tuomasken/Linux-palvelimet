# H5 Nimekäs


## Harjoituksessa käytetyn koneen parametrejä

- Kannettavan tietokoneen malli: HP Elitebook 840 G4
- Käyttöjärjestelmä: Windows 10 Pro, versio 22H2
- Prosessori: Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz
- Näytönohjain: Inter(R) HD Graphics 620
- RAM: 8 gb



## a)

Olin jo aiemmin vuokrannut Namecheap.com palvelusta domainin kenttala.com, eli käytän sitä tässä harjoituksessa.

## b)

Lähdin asettamaan nimipalvelinta komennolla:

    $ sudoedit /etc/apache2/sites-available/kenttala.com.conf

Ja käytin seuraavia asetuksia:

![image](https://github.com/user-attachments/assets/cdfb3f66-cc90-4060-82ae-c4cea3e8ebf7)

Tämän jälkeen loin sivulle sisältöä sen testaamista varten:

    $ mkdir -p /home/tuomaske/publicsites/kenttala.com
    $ echo testataanpa > /home/tuomaske/publicsites/kenttala.com/index.html

Lisäksi lisäsin kenttala.com saatavilla olevien sivujen joukkoon a2ensite-komennolla, ja poistin oletussivun a2dissite-komennolla. 
Tämän jälkeen boottasin apache2:n komennolla:

    $ sudo systemctl restart apache2

Tämän jälkeen testasin sivun toimivuutta curl-komennolla, jolloin sain "Permission denied" virheilmoituksen. Siirryin tarkastelemaan virhettä tarkemmin apachen lokeihin komennolla:

    $ sudo tail /var/log/apache2/error.log

Jossa oli seuraavanlainen virheilmoitus:

![image](https://github.com/user-attachments/assets/0fe01c61-5013-4540-9345-c6446f149016)

Oletin tämän tarkoittavan, että apachella ei ole käyttöoikeuksia lokitapahtumassa näkyvän polun päässä olevassa objektissa, eli tässä tapauksessa kansiossa tuomaske.com olevassa index.html-tiedostossa. Siirryin tarkastelemaan sitä:

![image](https://github.com/user-attachments/assets/07217239-54a0-42a4-85f5-f4b63923c965)

Ajattelin execute-oikeuksien puuttumisen others-ryhmän jäseniltä tukevan päätelmääni, joten lisäsin kaikille ryhmille execute-oikeudet. Lisäksi tässä näkyy, kuinka sivua pystyy muokkaamaan user-ryhmän jäsenenä ilman pääkäyttäjien oikeuksia:

![image](https://github.com/user-attachments/assets/42328c82-fbc5-47b6-ae25-653ec4f611d1)

Tämä ei kuitenkaan auttanut, vaan sivua testattaessa tuli sama virhe samalla loki-tapahtumalla. Siirryin konsultoimaan googlea, ja löysin apua sivulta https://stackoverflow.com/questions/43318041/ah00035-access-to-denied-filesystem-path-users-xxx-documents-workspace-b. Kokeilin sivulla ehdotettua komentoa nähdäkseni koko polun käyttöoikeudet:

![image](https://github.com/user-attachments/assets/fc002343-57f0-4cf1-ac4d-e983604688dc)

Tämän avulla vihdoinkin löysin vian, eli tuomaske-hakemiston käyttöoikeuksissa oli puutteita. Korjasin asian:

![image](https://github.com/user-attachments/assets/888dad1e-b1b9-45d5-8f26-0a7d76d75369)

Tämän jälkeen kokeilin jälleen curl-komentoa, ei toiminut, mutta lokitapahtuma oli eri:

![image](https://github.com/user-attachments/assets/7351ce6d-8ac2-4365-8cbb-adb584f697d7)

Tämä korjaantui siirtymällä lokitapahtumassa mainitulle polulle, jossa huomasin kirjoitusvirheen hakemistossa. Korjasin asian ja kokeilin uudelleen sivua, ja se toimi.

![image](https://github.com/user-attachments/assets/eb0c4842-8471-429a-b258-6c9c7eac12cf)


## c)

Tässä harjoituksessa lähdin luomaan kotisivua, joka sisältää kolme erillistä alasivua. Loin aluksi jo olemassa olevan index.html:n lisäksi kaksi muuta alasivua (blog.html ja projects.html):

![image](https://github.com/user-attachments/assets/deab6018-9845-4d04-8550-d0716a24467d)

Tämän jälkeen kirjoitin jokaiseen html-tiedostoon koodia. Apua koodin sivujen väliseen viittaamiseen kysyin tekoälyltä (chatgpt.com). Tässä on esimerkki etusivun html-koodista:

![image](https://github.com/user-attachments/assets/cca3b253-c808-4745-a6f1-bc950b7429ea)

Ja tässä on lopputulos, joka päivittyi automaattisesti muokattuani html-tiedostoa. Kaikki alasivut toimivat tarkoituksenmukaisesti:

![image](https://github.com/user-attachments/assets/5a7c54aa-19ba-4e77-9925-40d18ea2c0ed)

Lisäksi tarkistin sivuni HTML-koodin palvelulla https://validator.w3.org/

![image](https://github.com/user-attachments/assets/74794634-b2aa-48cf-8efe-b0c436c05925)


## d)

Tässä osiossa loin kaksi uutta alidoimainia sivulleni, jotka avaavat saman sivun kuin päädomain-osoite. Luodut alidoimainit ovat blog.kenttala.com ja portfolio.kenttala.com.

![image](https://github.com/user-attachments/assets/355cd4ce-55af-4c00-89bf-b25e19c9b88d)

Testasin molempien alidomainien toimivuutta:

![image](https://github.com/user-attachments/assets/1ef850ee-8795-4ce4-b5ad-f3675a607d9e)

![image](https://github.com/user-attachments/assets/af073012-6519-4673-8871-6a0d0b62de64)



## e)

Aluksi kokeilin komentoja dig ja host, mutta niitä ei löytynyt. Googletin ja löysin sivun https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/, minkä kautta selvisi, että ne pitää asentaa.
Ajoin komennon:

        $ sudo apt-get install dnsutils

Tämän jälkeen ajoin komennon:

        $ host kenttala.com

Mikä antoi seuraavanlaisen tuloksen:

![image](https://github.com/user-attachments/assets/6750a0a1-ebb0-4e23-996d-c2ee91dcf08b)

Tämän tuloksen ja dellä mainitun sivun (geeksforgeeks.org) artikkelin perusteella päättelisin, että host-komento haki DNS-palvelun kautta domainin kenttala.com osoitetiedot.

Tarkastelin myös alidomainia blog.kenttala.com host-komennolla, ja se osasi kertoa, että kyseinen domain on alias kenttala.com domainille.

![image](https://github.com/user-attachments/assets/cd35012d-3e6f-413d-a8f0-f6d49dea4c15)

Lisäksi kokeilin komentoa:

        $ dig kenttala.com ANY

Tämä komento antoi kaikki DNS-tiedot domainiin liittyen:

![image](https://github.com/user-attachments/assets/c11b08a6-2e1d-4a54-a185-d45a82ac57ca)



Seuraavaksi tarkastelin domainin pohjoispohjalaiset.fi osoitetietoja host ja dig komennoilla:

![image](https://github.com/user-attachments/assets/c4b43a06-ff22-4196-8ac1-ff1c54bb9bcd)
![image](https://github.com/user-attachments/assets/fb48fe91-0cae-4ecb-be6f-91fe637fec79)














