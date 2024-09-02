# h2 Komentaja Pingviini

> ## Tiivistelmä
>
> Raportti koostuu Tero Karvisen komentorivikomentoja käsittelevän artikkelin tiivistelmästä sekä Linuxin komentoriviin keskittyvistä tehtävistä. Nämä tehtävät on raportoitu aikaleimoin, jotta lukija saisi kuvaa siitä, kuinka paljon aikaa vastaavaan saattaisi kulua.

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

## a) Micro

0:00 Tehtävässä asennetaan virtuaalikoneeseen micro-editori. Aloitin prosessin avaamalla Applicationsista Terminal Emulatorin ja antamalla Karvisen (3.2.2020) artikkelista löytyvän komennon `sudo apt-get update`, jotta saatavilla olevat ohjelmat olisivat ajantasalla. Syötin pääkäyttäjäni salasanan, minkä jälkeen saatavilla olevat ohjelmat päivittyivät nopeasti. Seurasin tätä toisella Karvisen (3.2.2020) artikkelista löytyvällä komennolla `apt-cache search micro`, jonka tarkoituksena oli selvittää, millä nimellä saisin asennettua micro-editorin. Hakuehtojen ollessa kuitenkin hyvin väljät osuvia ohjelmia oli huomattavasti enemmän kuin odotin. Päätin jakaa ohjelmat pienempiin osiin putkittamalla edellä olevan komennon perään komennon `less`. Ohjelmistolistaa selatessani otin käyttöön hakukomennon `/micro`, joka korosti kaikki micro-sanat ohjelmien nimistä ja kuvauksista. Tämän avulla löysin lopulta etsimäni ohjelman (ks. kuva alla).

![micro search](https://github.com/user-attachments/assets/cf8c0657-3158-43f3-a295-a5a902a55f90)

0:08 Asensin ohjelman Karvisen (3.2.2020) artikkelista löytyvällä komennolla `sudo apt-get -y install micro`. Nopean asennusprosessin jälkeen halusin varmistaa, että asennus oli todella tapahtunut, joten lähdin etsimään, missä asennettu ohjelma sijaitsisi. Kahdella `cd ..`-komennolla siirryin juurihakemistoon, jossa tarkastin hakemiston sisällön `ls`-komennolla. Siirryin seuraavaksi käyttäjähakemistoon `cd usr`-komennolla. Selvitin jälleen `ls`-komennolla hakemiston sisällön. Lähdin tämän jälkeen hakuampumaan komennoilla `ls src` ja `ls lib` alla olevien hakemistojen sisältöä ilman tulosta. Googlasin sitten tarkempaa tietoa, minne Linux asentaa ohjelmansa ja päädyin Afriportal Networkin (17.10.2023) sivulle, joka vihjasi sijainniksi bin-hakemistoa. `ls bin`-komento näytti liian monta hakemistoa, joten putkitin perään `less`-komennon ja tein haun `/micro` löytäen viimein asentamani tiedoston (ks. kuva alla).

![micro bin](https://github.com/user-attachments/assets/e0193e44-7f35-459a-8365-c297e95e8fc1)

0:12 Navigoin sitten takaisin käyttäjäni hakemistoon (/home/leevi) komennoilla `cd ..`, `cd home` ja `cd leevi`, jossa testasin Micron avaamista komennolla `micro`. Editori aukeni hyvin ja oli toimiva (ks. kuva alla). Pyrkiessäni sulkemaan ohjelman suljin vahingossa koko Terminal Emulatorin, sillä sekoitin ruudun ylälaidassa olevan valikkorivin Micron omaksi. Avasin Terminal Emulatorin ja micron uudelleen ja pienen silmäilyn jälkeen huomasin saavani apua CTRL+g-komennolla. Sillä selvisi, että CTRL+q-komennolla saa Micron suljettua, joka toimi kuten luvattu.

![microssa](https://github.com/user-attachments/assets/8ff8c99b-048e-436b-9250-99551163e334)

## b) Apt

0:15 Tehtävässä oli tarkoituksena asentaa kolme komentoriviohjelmaa, joten lähdin suoraan tutkimaan tarjontaa komennolla `apt-cache search terminal interface|less`. Tämä ei välttämättä ollut paras ratkaisu, sillä haun tuottaessa suuren määrän tuloksia itselläni ei ollut minkäänlaista vertailupohjaa, mitä minun pitäisi oikeastaan asentaa ja onko kyseinen ohjelma edes sellainen, mitä olen hakemassa kuvauksesta huolimatta. Päädyinkin googlaamaan hyviä linuxin terminaalikäyttöliittymiä ja päädyin Redditin keskusteluun (Gitarre94 24.12.2022). Poimin kyseisestä keskusteluketjusta ohjelmat gnome-terminal, kitty ja foot, ja palasin takaisin Terminal Emulatoriin tekemään edellä olevan haun uudelleen, tosin tällä kertaa ilman "interface" loppua. Hakukomennon (`/[ohjelma]`) avulla varmistin, että edellä olevat kolme ohjelmaa löytyivät listalta juuri näillä nimillä.

0:24 Palasin hausta takaisin Terminal Emulatoriin q-näppäimellä ja annoin Karvisen (3.2.2020) artikkelin vinkin mukaan normaalin asennuskomennon, mutta liittäen kaikki kolme ohjelmaa toistensa perään, jotta ne asentuisivat kerralla (ks. kuva alla). Ohjelmat asentuivatkin ongelmitta pääkäyttäjän salasanan antamisen jälkeen.

![moniasennus](https://github.com/user-attachments/assets/39e8e209-dafc-48bb-aa86-da851257908c)

0:25 Aloitin asentamieni ohjelmien testauksen foot:sta antamalla komennon `foot` Terminal Emulatorissa, ja vastaani tuli heti ongelmia (ks. kuva alla). Koska en ymmärtänyt, mikä oli mennyt pieleen, lähdin selaamaan ohjelman manuaali komennolla `man foot`. En kuitenkaan saanut ohjeistuksesta juuri mitään irti, mahdollisesti kokemattomuudestani johtuen, ja kärsivällisyyteni loppuessa päädyin testaamaan Karvisen (3.2.2020) esittelemää ohjelmien poistokomentoa `sudo apt-get purge foot`. Asennus poistui kiltisti koneelta (ks. keskimmäinen kuva alla). Nyt kuitenkin minulla oli vain kaksi komentoriviohjelmaa, joten palasin jälleen Redditiin ja poimin tällä kertaa asennettavaksi Konsolen. `apt-cache search terminal|less` ja `/konsole` komennoilla nimen varmistus ja asennus komennolla `sudo apt-get -y install konsole`. Tämäkin ohjelma asentui ongelmitta ja footista poiketen lähti ongelmitta käyntiin Terminal Emulatorissa annetun ohjelmanimen `konsole` myötä. Konsolessa näytti toimivan myös muutamat peruskomennot, joita testasin (ks. viimeinen kuva alla).

![foot start](https://github.com/user-attachments/assets/56749827-773f-41cf-86e8-27ce8fded0e2)

![foot purge](https://github.com/user-attachments/assets/6cdc53e2-a70e-4eb2-94db-bf85950a4e99)

![konsole](https://github.com/user-attachments/assets/886dd623-47c1-42d4-b39a-b7d5e8f218e5)

0:34 Seuraavaksi testasin Kittyn toimimista. Tämäkin ohjelma lähti ongelmitta käyntiin Terminal Emulatorissa `kitty`-komennolla. Myös tässä ohjelmassa normaalit komentorivikomennot kuten `ls` ja `cd` toimivat ongelmitta. `man kitty`-komennolla avasin manuaalin (ks. kuva alla), josta en kuitenkaan saanut liiemmin irti, mikä tekee kyseisestä ohjelmasta erikoisen.

![man kitty](https://github.com/user-attachments/assets/ef2961ea-54a4-44ee-8340-0ff348be693d)

0:38 Viimeisenä testasin gnome-terminalin toimintaa avaamalla sen edellisten ohjelmien tapaan komentorivikomennolla `gnome-terminal`. Tyylillisesti suurin ero edellisiin ohjelmiin oli täysin valkoinen tausta, joka ei ollut ollenkaan makuuni. Nopeiden komentorivikomentojen (`ls`, `cd`, `man gnome-terminal`, ks. kuva alla) testauksen jälkeen suljin ohjelman suosiolla `exit` komennolla.

![gnome](https://github.com/user-attachments/assets/96ebdc93-ec5f-4057-9730-e8dfccac7bc8)

Kolme toimivaa asennusta erosivat visuaalisesti Debianin mukana tulleesta Terminal Emulatorista, mutta itselleni jäi vielä melko avonaiseksi kysymykseksi, mitä muita eroja eri komentoriviohjelmilla on keskenään. Redditin keskustelun (Gitarre94 24.12.2022) mukaan eroja löytyisi ohjelmien pyörittämiskeveydestä sekä muokattavuudesta, minkä lisäksi ilmeisesti esimerkiksi Kitty pyörittäisi paremmin CJK-fontteja (kiinalaiset, japanilaiset, korealaiset merkit). Eroja siis vaikuttaisi olevan ja kokeneempi käyttäjä varmaan pystyisikin muokkaamaan juuri itselleen sopivan visuaalisen tyylinkin haluamaansa ohjelmaan. Itse tosin taidan tyytyä Terminal Emulatorin värimaailmaan ja tyyliin.

## c) FHS

0:39 Käynnistettäessä Terminal Emulator työpöydältä aktiivisena hakemistona on alkuun käyttäjän oma hakemisto, josta juurihakemistoon päästään helposti komennolla `cd ../..` (ks. kuva alla). Juurihakemisto toimii koko Linux-järjestelmän pohjana, ja tänne asennetaan kaikki muut hakemistot joiden alahakemistoihin asennellaan esimerkiksi käyttäjien tiedostoja tai ohjelmia (Karvinen 3.2.2020).

![root](https://github.com/user-attachments/assets/fe47c600-1b61-4e90-9b97-b3aa3f6edea6)

0:40 Juurihakemistosta päästää siirtymään komennolla `cd home` tietokoneen kotihakemistoon, joka sisältää kaikkien tietokoneen käyttäjien henkilökohtaiset hakemistot (Karvinen 3.2.2020). Tämän virtuaalikoneelle asennetun Debianin tapauksessa nyt käytössä olevan käyttäjän kotihakemisto on ainoa hakemisto, joka täältä löytyy (ks. alla oleva kuva).

![home](https://github.com/user-attachments/assets/d08ee231-6fa2-4a93-b19f-f089f569ec9e)

0:40 Käyttäjän omaan kotihakemistoon päästään tietokoneen kotihakemistosta komennolla `cd [käyttäjä]` (tässä käyttäjä on "leevi"). Tämä hakemisto sisältää kyseisen käyttäjän henkilökohtaisia hakemistoja ja tiedostoja, joihin vain hänellä on muokkauskäyttöoikeudet. Lisäksi tämä on ainoa paikka, jonne käyttäjä itse voi tallentaa dataa (Karvinen 3.2.2020). Tällä hetkellä kyseinen hakemisto sisältää pelkästään muita hakemistoja, jotka on nimetty oletuksena teemoittain (ks. kuva alla).

![leevi](https://github.com/user-attachments/assets/7287d282-0357-416c-9183-fe9ffef3632a)

0:41 Järjestelmäasetuksiin keskittyvä hakemisto "etc" sijaitsee suoraan juurihakemiston alapuolella, joten sinne päästään juurihakemistosta komennolla `cd etc` (Karvinen 3.2.2020). Hakemisto sisältää niin alihakemistoja kuin myös tekstidokumentteja (ks. ylin kuva alla). Ilman tarkempaa perehtymistä, mitä kukin tiedosto tai hakemisto sisältää, selaaminen oli hakuammuntaa (ks. keskimmäinen kuva alla). Hakemistoihin pääsi siirtymään normaalisti `cd`-komennolla, kun taas `less`-komentoa pystyi käyttämään tekstitiedostojen lukemiseen. Sisältä löytyvien tietojen moninaisuudesta esimerkkinä toimii tietokoneen nimi, joka määritettiin aiemmin tehtävässä h1, tiedostossa "hostname" (ks. alin kuva alla).

![ls etc](https://github.com/user-attachments/assets/250d69bd-9531-4a7a-ac61-7c8247233a58)

![hakua](https://github.com/user-attachments/assets/21980f47-19a0-4ab2-b561-80759c008302)

![hostname](https://github.com/user-attachments/assets/d61383b3-10a3-4945-a7b6-595edcb53acf)

0:49 Karvisen (3.2.2020) mukaan /media/ kansio sisältää sisältöä, joka ilmeisesti liitetään hetkellisesti koneeseen kuten CD-levyt tai USB-muistitikut. Juurihakemistosta hakemistoon pääsee `cd media` komennolla. Kuitenkin omassa tapauksessani kyseinen hakemisto ei sisältänyt käyttäjän hakemistoa lukuun ottamatta mitään, ja tämäkin alihakemisto oli tyhjä. Tämä siitäkin huolimatta, että tehtävässä h1 hyödynnetty VirtualBoxin Guest Additions CD Image oli edelleen mountattuna koneeseen (ks. kuva alla). Ilmeisesti kyseinen mount ei kuitenkaan kuulu tämän hakemiston sisältöön.

![media](https://github.com/user-attachments/assets/7e6ccfd0-e487-4e25-9b80-1dd1f759bdd4)

0:50 Viimeisenä tarkasteltavana hakemistona on juurihakemistossa sijaitseva /var/log/. Karvisen (3.2.2020) mukaan kyseisessä hakemistossa säilytetään tietokoneen lokitiedostoja ja lokeja sisältäviä hakemistoja. Todennäköisesti tietokoneen nuoresta iästä johtuen hakemiston sisältö oli vielä melko pieni (ks. ensimmäinen kuva alla). Myöskään lokitiedostoissa ei ollut vielä kauheasti sisältöä. Kuitenkin apt-hakemistosta löytyvästä history.log-tiedostosta löytyi tietoa tietokoneelle tehdyistä asennuksista. Komennolla `/purge` löysin myös, että lokitiedostosta löytyvät ohjelmistojen poistot myös, joten aiemmin poistettu foot-ohjelma löytyi myös lokista (ks. jälkimmäinen kuva alla).

![varlog](https://github.com/user-attachments/assets/1758c6c7-2760-4c11-b06b-62a1c3900352)

![history](https://github.com/user-attachments/assets/3465be13-8f6f-4c2b-bd47-03afb2afa6c3)

## d) The Friendly M

0:55 Koska en tarkkaan muistanut, mistä `grep`-komennossa oli kyse, käytin komentoa `man grep` päästäkseni lukemaan tästä (ks. kuva alla). Grepillä voi hakea kirjainjonolla tietoa siitä, sisältääkö jokin tekstitiedosto (tai hakemisto) kyseistä tekstijonoa, ja grep palauttaa oletuksena riveittäin kaikki sopivat tulokset.

![man grep](https://github.com/user-attachments/assets/f49303ed-7d42-4349-8fb6-c3ee857bca0a)

Käytin tätä edellä tarkastelemaani history.log-tiedostoon ja tekstijonona "purge", jolloin /var/log/apt-hakemistossa tehty komento oli `grep purge history.log` (ks. kuva alla).

![grep purge](https://github.com/user-attachments/assets/cbf8ba20-7f03-44c0-b9d2-3d409d8fe1ed)

Tämän jälkeen tulkitsin grepin manuaalia väärin, kun luulin, että jättämällä kohdetiedoston pois haku tehtäisiin rekursiivisesti kaikkiin hakemiston tiedostoihin. Komento `grep insta` aiheutti käytännössä Terminal Emulatorin jumiutumisen, josta pääsin pois CTRL+c yhdistelmällä (ks. kuva alla).

![vajaa](https://github.com/user-attachments/assets/8b69f51a-4745-4665-8860-5e6fde24717b)

Tarkastelin lisää grepin manuaalia ja otin testiin laskemis-filterin. Ominaisuus on hyödyllinen suurissa tekstitiedostoissa, joista halutaan tietää, monellako rivillä jokin tekstijono esiintyy. Tämän sain toimimaan onnistuneesti komennoilla `grep -c install history.log` ja `grep -c purge history.log` (ks. kuva alla).

![grep count](https://github.com/user-attachments/assets/939ebaab-24f5-4e8a-8360-23111366ece4)

Minua kuitenkin häiritsi edelleen miten rekursiivinen haku voitaisiin toteuttaa, koska alihakemistoista etsiminen tuntuisi luonnolliselta ominaisuudelta. Pienen googlailun jälkeen löysin Prakashin (30.8.2024) artikkelin, josta bongasin komennon `grep -r [hakutermi] .`, jolla rekursiivinen haku lähti toimimaan. Testatessani tätä hakemistossa /var/log komennolla `grep -r install .` sain huomattavan määrän tuloksia, joten kiinnostuin miten saisin yhdistettyä laskemis-filterin rekursiivisuuden kanssa. Googlailun jälkeen löysin Rain (10.1.2017) kysymyksen aiheesta ja tämän vastauksista bongasin putkituksen käyttämisen ratkaisuna. Nyt käyttäessäni komentoa `grep -r install . | grep -c install` sain laskettua monellako rivillä /var/log hakemiston ja sen alihakemistoissa olevissa tiedostoissa on käytetty tekstipätkää "install" (ks. kuva alla).

![grep multi](https://github.com/user-attachments/assets/14bfe7e5-df85-4de6-8fce-02f045138c0c)

## e) Pipe

Putkien tarkoitus on yhdistää eri komentoja toimimaan yhdessä. Aiemmin tässä raportissa esimerkiksi kohdassa a) putkitin `less`-komennon näyttämään "sivuttain" ohjelmistoja, joita hain komennolla `apt-cache search micro | less` ja taas juuri äsken kohdassa d) putkitin kaksi grepiä, jotta pystyin rekursiivisesti laskemaan hakemieni merkkijonojen määrän eri hakemistoissa sijaitsevista tiedostoista.

## f) Rauta

1:06 Lopuksi analysoin rautaa, jolle Linux on asennettu. Annoin komennon `sudo lshw -short -sanitize` ja syötin pääkäyttäjän salasanan saadakseni ilmoituksen, ettei koneella ole lshw-ohjelmaa (ks. ensimmäinen kuva alla). Ohjelman asennus komennolla `sudo apt-get -y install lshw` sujui nopeasti ja uudelleen ajettu `sudo lshw -short -sanitize`-komento toimi nyt (ks. jälkimmäinen kuva alla).

![eiollu](https://github.com/user-attachments/assets/9de948b9-d58a-4105-b6ba-28c89aaab596)

![rauta](https://github.com/user-attachments/assets/d99f9204-44f1-403b-8580-cfe708c3198e)

Kyseinen komento näyttäisi kertovan lyhennetyssä muodossa, minkälaiselle koneelle Linux on asennettu. Tässä tapauksessa mielenkiintoista on se, että listaus tunnistaa virtuaalikoneen (VirtualBox) käyttämisen osana rautaa, esimerkiksi 8 gigaa muistia, sekä oikean raudan tietoja, kuten prosessorin AMD Ryzen 7 7840HS. Tiedoissa on myös joitain erikoisuuksia kuten 64 gigan VBOX-kovalevy, kun tehtävässä h1 kovalevyn suuruudeksi annoin 60 gigaa. Myös verkkoliittimenä on näennäisesti gigabitin ethernet-liitin, joka on selvästi virtualisoitu, sillä tässä kannettavassa ei ole fyysistä verkkoliitintä.

## Lähdeluettelo

Afriportal Network 17.10.2023. Where Linux install programs. Luettavissa: https://afriportalnetworkltd.com/blog/where-linux-install-programs/. Luettu: 2.9.2024.

Gitarre94 24.12.2022. What is the best terminal for linux for you? Luettavissa: https://www.reddit.com/r/linux/comments/zty01e/what_is_the_best_terminal_for_linux_for_you/. Luettu: 2.9.2024.

Rai, G. 10.1.2017. grep -rc does not work; count number of matches in a directory. Luettavissa: https://unix.stackexchange.com/questions/336398/grep-rc-does-not-work-count-number-of-matches-in-a-directory. Luettu: 2.9.2024.

Karvinen, T. 3.2.2020. Command Line Basics Revisited. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited. Luettu: 2.9.2024.

Prakash, A. 30.8.2024. How to Perform Grep Search on All Files and in All Directories. Luettavissa: https://linuxhandbook.com/grep-search-all-files-directories/. Luettu: 2.9.2024.
