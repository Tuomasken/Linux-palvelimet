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

Seuraavaksi loin microlla java-tiedoston heimaailmajava.java, johon kirjoitin seuraavan koodinpätkän:

    public class heimaailmajava {
     public static void main(String[] args)
     {
     System.out.println("Hei maailma");
     }
    }

![image](https://github.com/user-attachments/assets/b6eef5a8-d43e-4cdd-bf75-37bde4b0755b)








