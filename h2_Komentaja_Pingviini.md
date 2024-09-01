# h2 Komentaja Pingviini

> ## Tiivistelmä
>
> Kuvaus

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 800/951 GB vapaana

## x) Tiivistelmä

Karvinen (3.2.2020) esittelee artikkelissaan komentorivin, joka on ollut olemassa jo vuosia ennen edes internetin yleistymistä, perusteita. Komentorivin käytön voi sanoa perustuvan pariin komentokategoriaan, jotka pitkälti toimivat kaiken komentorivillä tehtävän pohjana: liikkuminen hakemistoissa, sekä hakemistojen ja tiedostojen muokkaaminen. Hakemistoissa liikkuminen perustuu seuraaviin komentoihin:
- `pwd` ilmoittaa tällä hetkellä aktiivisena olevan hakemiston
- `ls` näyttää hakemiston sisällön
- `cd [hakemisto]` siirrytään määriteltyyn hakemistoon
- `less [tekstitiedosto]` näyttää kohdennetun tekstitiedoston sisällön ruutu kerrallaan.

Hakemistoja taas voidaan muokata seuraavilla komennoilla:
- `mkdir [hakemisto]` luo uuden hakemiston
- `mv [vanhanimi] [uusinimi]` siirtää [vanhanimi] hakemiston tai tiedoston [uusinimi] sijaintiin ja nimeää sen täksi, jos sitä ei ole ennestään olemassa
- `cp -r [alkuperäinen] [kopio]` kopioi [alkuperäisen] [kopio] nimellä, hakemiston tapauksessa kaiken sisältöineen
- `rmdir [tyhjähakemisto]` poistaa tyhjän hakemiston
- `rm [roska]` poistaa tiedoston

Komentorivi ei erikseen varoittele, kun asioita ollaan siirtämässä tai poistamassa, joten tämän suhteen tulee olla aina huolellinen. Edellä olevien komentojen lisäksi hyödyllinen komento on myös `man [komento]`, joka näyttää komennon manuaalin, ja jota voi siis käyttää apuna selvittämään, miten komoento toimii. Linuxilla tulee tutuksi myös komento `sudo`, joka antaa käyttäjälle korkeimmat käyttöoikeudet, kunhan tietää pääkäyttäjän salasanan. (Karvinen 3.2.2020.)

## a) 

## Lähdeluettelo

Karvinen, T. 3.2.2020. Command Line Basics Revisited. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited. Luettu: 1.9.2024.
