# H2 Komentaja Pingviini

## Tehtävä

Työskentely aloitettu 6:47 30/01/2024. Käytetyn koneen ominaisuuksia: 
*Prosessori* Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz 2.71 GHz. 
*RAM* 8GB. 
*Käyttöjärjestelmä* Windows 10 Pro 64-bit (versio 22H2). 
*GPU* Intel(R) HD Graphics 620.

### Micro-editorin asennus

Aloitetaan asennus päivittämällä ohjelmapakettien indeksit:
![apt-get_update](H2Kuvat/Update)

Tämän jälkeen asennetaan Micro-editori [https://terokarvinen.com/2022/micro-editor-plugin-hello-world/](https://terokarvinen.com/2022/micro-editor-plugin-hello-world/) ohjeiden mukaisesti.
![micro_asennus](H2Kuvat/Micron_asennus)

### Rauta

Asennetaan lshw-ohjelma (list hardware) micro-editorin asennuksessa opitun kaavan mukaisesti.
![lshw_asennus](H2Kuvat/lshw_Asennus)

Ajetaan lshw.
![lshw1](H2Kuvat/lshw1)
![lshw2](H2Kuvat/lshw2)

Luonnollisesti lshw näyttää luodun virtuaalikoneen laitteistoa eli "rautaa". Levyn ja työmuistin koko ovat vastaavat mitä asetettiin konetta luodessa. Prosessori on käytetyn isäntäkoneen. Eli komennon saatiin selville ensisijaisesti se, että 1) työskennellään virtuaalisella koneella 2) osa virtuaalisen koneen asetuksista.

### Valinnaisten komentoriviohjelmien asennus

Aluksi tutustuin ohjelmistopaketti-valikoimaan "apt-cache search" komennolla. Hakusanoina käytin "text user interface" ja "command line interface".
![Search_komento](H2Kuvat/Search)

Kun löysin kiinnostavan paketin, tutustuin siihen tarkemmin "apt-cache show" komennolla.
![Show_komento](H2Kuvat/apt-cache_Searchmonkey)

Valitsin testattaviksi ohjelmiksi Searchmonkey ja Gitit nimiset paketit. Lisäksi olin entuudestaan hieman tutustunut Nethack nimiseen peliin, jonka valitsin myös yhdeksi testattavista ohjelmista. Asensin kyseiset ohjelmat 7:59. Asennus kesti noin minuutin.

![Pakettien_asennus](H2Kuvat/3asennus)

Seuraavaksi testasin asennetut ohjelmat:

*Searchmonkey*
Kyseessä hieman graafisempi versio komentorivin hakutoiminnosta. Testattu hakemalla yksinkertaisella hakusanalla. Löysi kaikki tiedostot joissa oli nimessä kyseinen sana.
![Searchmonkey](H2Kuvat/Searchmonkey)

*Gitit*
Wikiohjelma, eli yksinkertaisesti tietopankki.
![Gitit](H2Kuvat/Gitit)

*Nethack*
Merkkigrafiikalla toteutettu roolipeli.
![Nethack](H2Kuvat/Nethack)




  


## Lähteet
https://terokarvinen.com/2022/micro-editor-plugin-hello-world/
