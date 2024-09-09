# h3 Hello Web Server

> ## Tiivistelmä
>
> Raportissa ensin esitellään tiivistelminä The Apache Software Foundationin (2024) ja Karvisen (10.4.2018) artikkelit nimipohjaisten virtuaali-isäntien toiminnasta. Tämän jälkeen luodaan ja muokataan verkkosivuja hyödyntäen Apache-ohjelmistoa.

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 797/951 GB vapaana

## x) Tiivistelmät

### Name-based Virtual Host Support (ASF 2024a)

ASF:n (2024a) artikkelissa esitellään nimipohjaisten virtuaalisten isäntäkoneiden toimintaa. Ideana tässä on, että samaa IP-osoitetta voidaan käyttää viittaamaan useampaan eri verkkosivuun. Virtuaaliselle isäntäkoneelle määritetään oma IP-osoite, mutta kaikkiin muihin sivuihin, joita palvelin sisältää, viitataan nimien mukaan. Järjestelmän toimimisen ehtona onkin, että päätelaitteet ilmoittavat hakemansa verkkosivun nimen osana HTTP-otsaketietoja, kun ne lähettävät pyyntöjä palvelimelle. Tämän tiedon avulla palvelin pystyy hakemaan oikean sivun ja lähettämään sen vastauksena. (ASF 2004a.)

Nimipohjaisen järjestelmän käyttö perustuu rajalliseen IPv4-osoitteiden määrään. Vapaina olevien osoitteiden määrän tyrehtyessä, mutta uusien verkkosivujen määrän jatkaessa kasvua, on nimipohjainen järjestelmän käyttö käytännössä pakollista jollei laitteisto itsessään vaadi IP-pohjaista virtualisointia. Kuitenkin on hyvä huomata, että lähtökohtaisesti IP-pohjainen nimiresoluutio toimii myös nimipohjaisen järjestelmän perustana. Jos virtuaali-isännän IP-osoitteet on määritelty huonosti DNS-palvelimelle, systeemi ei tule toimimaan, vaikka järjestelmä olisi nimetty muuten täydellisesti. Tämä johtuu siitä, että virtuaali-isännän hallinnoimista sivuista valitaan HTTP-otsakkeessa olevaa nimitietoa sopivin vasta sitten, kun sopivin IP-osoite ja porttinumero on tavoitettu. Tämän jälkeen, erityisesti Apachen tapauksessa, jos useampi verkkosivu vastaa samaa IP-osoitetta, virtuaali-isäntä lähtee tarkastelemaan pyynnön palvelinnimeä sekä mahdollisia aliaksia. (ASF 2024a.)

### Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address (Karvinen 10.4.2018)

Karvinen (10.4.2018) esittelee artikkelissaan lyhyesti, miten Apache otetaan käyttöön ja kuinka sitä voi hyödyntää ohjaamaan verkkoliikennettä yhden IP-osoitteen kautta useisiin eri kohteisiin. Prosessi käynnistyy asentamalla Apache Linuxiin komennolla `sudo apt-get -y install apache2`. Tämän jälkeen Karvinen muokkaa localhostissa olevaa oletussivua komennolla `echo "Default"|sudo tee /var/www/html/index.html`. (10.4.2018.) Seuraavaksi Karvinen (10.4.2018) luo uuden nimipohjaisen virtuaali-isännän komennolla `sudoedit /etc/apache2/sites-available/pyora.example.com.conf`, minkä jälkeen hän laittaa kyseisen sivun päälle (Fritsch 8.6.2007) komennolla `sudo a2ensite pyora.example.com` ja käynnistämällä Apachen uudelleen komennolla `sudo systemctl restart apache2` tuo tehdyt muutokset luettaviksi (Karvinen 10.4.2018). Tämän jälkeen normaalikäyttäjä pystyy muokkaamaan ja luomaan uusia verkkosivuja esimerkiksi komennoilla `mkdir -p /home/[käyttäjä]/publicsites/pyora.example.com/` ja `echo pyora > /home/[käyttäjä]/publicsites/pyora.example.com/index.html`. Lopuksi on aina hyvä testata, että tehdyt muutokset toimivat, mikä tapahtuu esimerkiksi komennoilla `curl -H 'Host: pyora.example.com' localhost` ja `curl localhost`. (Karvinen 10.4.2018.)

## a) Apache-weppipalvelimen asennus

0:00 Asensin Apachen jo keskiviikon luennolla Terminal Emulatorissa komennolla `sudo apt-get -y install apache2`. En tällöin kuitenkaan vielä muokannut oletussivua millään tapaa, joten päätin tehdä tämän myös. Testasin kuitenkin ensin `curl localhost` -komennolla, että oletussivuna ollut sivu näkyi komentorivillä oikein. Tämän jälkeen muokkasin sivun sisältöä Karvisen (10.4.2018) artikkelissa esitellyllä komennolla `echo "Oletussivu"|sudo tee /var/www/html/index.html`. Komennolla `curl localhost` näin muokkauksen toimivan oikein (ks. ensimmäinen kuva alla), ja nettiselaimessakin sivu näkyi oikein (ks. jälkimmäinen kuva alla).

![Oletussivu terminal](https://github.com/user-attachments/assets/ac3062ee-04c8-4284-9bcc-0daa34452e3b)

![Oletussivu selain](https://github.com/user-attachments/assets/7f7fdf9a-a4f2-4b2d-a813-c5a40a793e03)

## b) Lokin analysointi

0:01 Karvisen (20.8.2024) tehtävänannon vihjeistä käytin luennollakin esiteltyä komentoa `sudo tail /var/log/apache2/access.log`, jolla sain lokitiedoston lopun näkyviin (ks. kuva alla).

![Alkuloki](https://github.com/user-attachments/assets/2ae1ca17-368b-4dc9-8950-124782eb86c3)

Lokitiedostossa näkyy hyvin jo luennolla tekemäni kyselypyynnöt, sekä edellisessä tehtävässä tekemäni kyselyt. Lokitiedoston analysointiin etsin tietoa Googlen kautta päätymällä ensin Fitzpatrickin (14.1.2020) artikkeliin, jossa oli linkki ASF:n (2024b) dokumentaatioon. Jo ennen dokumentaation selaamista ymmärsin, että kyselyt oli tehty tältä koneelta, minkä ilmaisee IP-osoite 127.0.0.1. Kuitenkin dokumentaation myötä varmistuin, että ensimmäinen rivin tieto vastaa tosiaan sen koneen IP-osoitetta, josta kysely on tehty. Seuraavilla kahdella "-"-merkillä viitataan tietoihin, jotka eivät ole saatavilla. Tässä tapauksessa ensimmäistä ei ilmoiteta tiedon epävarmuuden takia, kun taas jälkimmäinen puuttui, koska tiedosto ei ole salasanasuojattu. Seuraavana on päivämäärän, kellonajan ja aikavyöhykkeen yhdistelmä. Tämän perässä olevien heittomerkkien sisällä on tieto siitä, mitä kyselyä ollaan tekemässä. Kaikissa tapauksissa ollaan pyytämässä (GET) jotain sivua tietystä paikasta (esim. /), ja asiakas tekee pyynnön hyödyntämällä jotain protokollaa (HTTP/1.1). Palvelin vastaa tähän kyselyyn koodilla, joka alinta tapausta lukuun ottamatta on onnistunut (200). Tätä tietoa seuraa asiakkaalle toimitettavan kohteen koosta, ja lokista voidaankin nähdä, että oletussivun tekstin muuttaminen selvästi pienensi sivun kokoa (10956 muuttui 237). Verkkoselaimella tehty kysely tuotti mielenkiintoisesti suuremman kohteen kuin komentorivillä tehty, mahdollisesti graafisen käyttöliittymän takia. Toiseksi viimeisenä on tieto, mistä osoitteesta kohde on haettu. Jostain syystä localhostin sijainti ilmoitetaan "-". Viimeisenä on tiedot asiakkaan käyttämästä selaimesta. (ASF 2024b.)

Lokitiedoston viimeisenä kyselynä on erikoinen jatko verkkoselaimessa tehdylle kyselylle, minkä kohteena oli "/favicon.ico", jonka haku ei kuitenkaan onnistu (virhekoodi 404). Tämä ilmeisesti liittyy jonkinlaiseen automatisoituun kyselyhakuun, joka tehdään verkkoselaimella normaalin kyselyn yhteydessä, ja joka liittyy verkkosivun visuaaliseen ilmeeseen (Khanna 9.8.2024).

## c) Uuden etusivun luominen

0:05 Lähdin luomaan uutta nimipohjaista virtuaali-isäntä verkkosivua Karvisen (10.4.2018) artikkelia mukaillen. Aloitin komennolla `sudoedit /etc/apache2/sites-available/hattu.example.com.conf`, joka avasi eteeni tyhjän tiedoston Nanossa. Suljin tämän hämmentyneenä ja ajoin seuraavaksi komennon `cat /etc/apache2/sites-available/hattu.example.com.conf`, jolla odotin saavani näkyviin Karvisen (10.4.2018) esimerkin mukaista tekstiä. Jälkikäteen mietittynä ei niin yllättäen luettu tiedosto oli tyhjä (ks. ensimmäinen kuva alla). Tästä viisastuneena ajoin edellä olleen sudoedit-komennon uudelleen ja tällä kertaa kirjoitin tiedostoon pitkälti samat tiedot kuin Karvisen (10.4.2018) esimerkissä (ks. toinen kuva alla).

![Luonti](https://github.com/user-attachments/assets/486ae01b-b529-4a40-bf24-f8a942b3502c)

![Eka edit](https://github.com/user-attachments/assets/f3a77a6c-1153-4062-b234-ff13d2c2048b)

Ihmettelin edelleen, että mikä tämä kotihakemistossa oleva xubuntu-hakemisto oikein oli ja kävin tarkistamassa, oliko tällainen mahdollisesti ilmestynyt sinne Apachen asennuksen yhteydessä. Komennot `cd ..` ja `ls` ja huomasin, ettei tällaista hakemistoa ollut olemassa. Hieman skeptisenä testasin uuden hakemiston luontia Karvisen (10.4.2018) ohjeiden mukaisesti komennolla `mkdir -p /home/xubuntu/publicsites/hattu.example.com/`, mutta sain ilmoituksen, ettei minulla ole oikeuksia tähän. Päättelin tässä vaiheessa kyseessä olevan ainoastaan esimerkki ja palasin taas muokkaamaan tehtävän alussa luomaani hattu.example.com.conf-tiedostoa korjaten samalla kirjoitusvirheet, joita olin tehnyt aiemmin (ks. ensimmäinen kuva alla). Laitoin sivun päälle komennolla `sudo a2ensite hattu.example.com` ja minulle ilmoitettiin, että uuden määrityksen aktivoiminen vaatisi komennon `systemctl reload apache2`. Päätin toimia Karvisen (10.4.2018) ohjeiden mukaisesti ja ajoin komennon `sudo systemctl restart apache2`. Tämä tuotti kuitenkin virheen, joten muutin komennoksi `sudo systemctl reload apache2`, joka ei myöskään toiminut (ks. jälkimmäinen kuva alla). Kokeilin vielä pelkän `systemctl reload apache2` komennon ajamista, mutta tämäkään ei auttanut annettuani erilliseen ikkunaan pääkäyttäjän salasanan.

![Toinen edit](https://github.com/user-attachments/assets/a09b81fd-8663-4cc3-a5a6-d54b70c7e84c)

![Virheitä](https://github.com/user-attachments/assets/43ed950d-83a0-49de-89c8-a50884c6c9d4)

0:12 Lähdin metsästämään, missä ongelma voisi olla. Ajoin ensin komennon `systemctl status apache2.service`, jonka antamista tiedoista en saanut kauheasti irti (ks. kuva alla). Lähdin kuitenkin tämän tiedon pohjalta tutkimaan tarjottua Apachen dokumentaatiota (ASF 2024c). Käytin hakusanoja kuten "apache2.service" ja "status" yrittäessäni löytää lisätietoa siitä, mitä saamani virheet tarkoittaisivat.

![systemctl status](https://github.com/user-attachments/assets/c8501b8c-bc07-4743-b7a2-369e2192bc16)

En kuitenkaan tuntunut saavan käyttämilläni hakusanoilla tulosta, joten palasin takaisin komentoriville ja ajoin edellä suositellun toisen komennon `journalctl -xeu apache2.service`. Avautunut tiedosto oli käytännössä tyhjä, mutta ylhäällä olleesta vihjeestä selvisi, että tavallisella käyttäjällä ei ole oikeuksia tarkastella kyseisen tiedoston tarkkaa sisältöä, joten ajoin saman komennon uudelleen `sudo` alulla. Nyt eteeni avautui huomattavasti enemmän informaatiota, josta bongasin selvästi ruudun ulkopuolelle jatkuvan rivin. Seurasin tätä riviä ja sain selville, etten ollut onnistunut eliminoimaan kaikkia kirjoitusvirheitäni aiemmin, vaan olin unohtanut yhden "/"-merkin (ks. ensimmäinen kuva alla). Sudoedit käyttöön ja virheen korjaus, jonka jälkeen ajoin nyt ilman virheitä komennot `sudo a2ensite hattu.example.com` ja `sudo systemctl restart apache2` (ks. jälkimmäinen kuva alla).

![Virhe](https://github.com/user-attachments/assets/77fa0857-d14e-41aa-96f0-31c9a93b7a6e)

![Korjattu](https://github.com/user-attachments/assets/70542967-0e0c-4f32-ba2d-9ac48eaff3c8)

0:23 Palasin nyt Karvisen (10.4.2018) ohjeisiin ja luomaan sivustolleni sijainnin ja aloitussivun. Sijainnin luominen tapahtui jo aiemmin testaamallani komennolla `mkdir -p /home/leevi/publicsites/hattu.example.com/`, joskin muutin käyttäjän oikeaksi tällä kertaa. Perään loin vielä aloitussivun tekstillä "hattu" komennolla `echo hattu > /home/leevi/publicsites/hattu.example.com/index.html`. Komento `curl -H 'Host: hattu.example.com' localhost` näytti, että sivu on toiminnassa, mutta komento `curl localhost` osoitti, että se ei ollut vielä oletuskohde (ks. kuva alla).

![Sivustonluonti](https://github.com/user-attachments/assets/199f11eb-ee92-4f4a-b86a-d1526c55095a)

Ennen kuin lähdin deaktivoimaan oletussivua, päätin muokata sivun tekstejä tehtävänantoon sopiviksi. Tein tämän komennolla `nano /home/leevi/publicsites/hattu.example.com/index.html` poistaen edellä tiedostoon kirjoittamani "hattu" tekstin korvaten sen Karvisen (12.2.2012) mallia mukaillen hattu.example.comiin sopivaksi. Varmistin tallennuksen jälkeen tekstin olemassaolon komennolla `cat /home/leevi/publicsites/hattu.example.com/index.html`. Todettuani asioiden olevan kunnossa lähdin selvittämään, miten saisin Apachen oletussivun pois päältä. Komento `man a2ensite` kertoi, että minun tulisi käyttää `a2ensite` sijasta `a2dissite`. Seuraavaksi tarkastin sijainnin, jonne olin hattu.example.comin konfiguraatiotiedoston luonut ja siirryin kyseiseen hakemistoon komennolla `cd /etc/apache2/sites-available`, koska oletin oletussivun konfiguraatiotiedoston olevan myös kyseisessä hakemistossa. Löysinkin komennolla `ls` tiedoston 000-default.conf, joten päätin kokeilla komentoa `sudo a2dissite 000-default`. Komento laittoi sivun pois päältä ja kehotti ajamaan komennon `systemctl reload apache2` uusien konfiguraatioiden aktivoimiseksi, minkä teinkin sudo-oikeuksin. Nyt kun testasin uudelleen edellä käyttämiäni kahta `curl`-komentoa sain saman lopputuloksen molemmista, eli hattu.example.comin (ks. kuva alla).

![Oletuksen deaktivoiminen](https://github.com/user-attachments/assets/af0c79c6-6b38-478a-84f6-3b8e6d5e85bb)

## e) HTML5-sivu

Tehtävä oli käytännössä jo tehtynä tehtävän c) jäljiltä, koska muokkasin jo kyseissä tehtävässä hattu.example.comin index.html:stä HTML5 sopivaksi. Luonnollisesti testasin tämän vielä selaimella, joka tuotti hyvää jälkeä (ks. ensimmäinen kuva alla). Ajoin vielä tarkistuksen validator.w3.org:ssa, joka huomautti sivun kielen puuttumisesta tageissa ja muutamista turhista merkeistä. Googlella hain tiedon, miten kieli tulisi ilmoittaa tageissa (Ishida & W3C 23.6.2021) sekä mikä on suomen koodi (W3 Schools 2024). Näiden tietojen ja saamieni huomautusten mukaan muokkasin Nanossa aloitussivusta niin sopivan, ettei validoiminenkaan tuottanut minkäänlaisia huomautuksia (ks. jälkimmäinen kuva alla).

![hattu example com](https://github.com/user-attachments/assets/2d9f9ca5-0c28-4602-9adf-064b47eecc47)

![Priima](https://github.com/user-attachments/assets/f7bdc0d8-28d0-4ed2-8173-c31678f1f8b2)

## f) Komennot `curl` ja `curl -l`

0:32 Saadakseni tietoa curlista käytin komentoa `man curl`, josta selvisi, että kyseinen komento siirtää dataa palvelimelta tai palvelimelle, ja se tukee useita eri protokollia. Aiemmissa tehtävissä olen käyttänyt komentoa näyttämään komentorivillä yksinkertaisia verkkosivuja, jotka hain samalta tietokoneelta. Curlia voi kuitenkin käyttää myös oikeidenkin verkkosivujen "lukemiseen" komentorivillä, joskin tämä ei ole täysin ongelmatonta (tästä lisää kohta).

Curliin voi liittää optiona -I ehdon, jolloin saadaan tietoa sivuston tiedoista (ks. alla oleva kuva). Kuvasta voidaan nähdä esimerkiksi tietoja kuten mitä HTTP-versiota sivusto käyttää, koska sitä on muokattu viimeksi ja minkälaisesta kohteesta on kyse.

![Curl helppo](https://github.com/user-attachments/assets/daeea05c-275b-4620-8197-86a00f639658)

Vaikka curlia voi käyttääkin verkkosivujen lukemiseen, ei esimerkiksi www.google.com :n lukeminen komentoriviltä ole mitenkään helppoa (ks. alla olevan kuvan ylempi osa). Sivusta voidaan kuitenkin saada tietoa irti `curl -I` muodossa, jolloin siitä saadaan järkevääkin infoa irti (ks. alla olevan kuvan alempi osa). Kuvasta voidaan myös huomata, että kaikki sivustot eivät sisällä samoja otsakkeita.

![Curl vaikea](https://github.com/user-attachments/assets/1c187b70-588e-4b6b-bc73-e19ea85f004d)

## Lähdeluettelo

Fitzpatrick, S. 14.1.2020. Understanding the Apache Access Log: View, Locate and Analyze. Luettavissa: https://www.sumologic.com/blog/apache-access-log/. Luettu: 7.9.2024.

Fritsch, S. 8.6.2007. Ubuntu Manpage: a2ensite, a2dissite - enable or disable an apache2 site / virtual host. Luettavissa: https://manpages.ubuntu.com/manpages/focal/en/man8/a2ensite.8.html. Luettu: 5.9.2024.

Ishida, R. & W3C 23.6.2021. Declaring language in HTML. Luettavissa: https://www.w3.org/International/questions/qa-html-language-declarations. Luettu: 7.9.2024.

Karvinen, T. 12.2.2012. Short HTML5 page. Luettavissa: https://terokarvinen.com/2012/short-html5-page/. Luettu: 7.9.2024.

Karvinen, T. 10.4.2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Luettu: 7.9.2024.

Karvinen, T. 20.8.2024. Linux Palvelimet 2024 alkusyksy. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 7.9.2024.

Khanna, G. 9.8.2024. How to Fix Favicon.ico 404 Errors Like a Pro: Tips and Tricks. Luettavissa: https://appwrk.com/resolving-favicon-ico-404-errors. Luettu: 7.9.2024.

The Apache Software Foundation 2024a. Name-based Virtual Host Support. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html. Luettu: 5.9.2024.

The Apache Software Foundation 2024b. Log Files. Luettavissa: https://httpd.apache.org/docs/2.4/logs.html#accesslog. Luettu: 7.9.2024.

The Apache Software Foundation 2024c. Apache HTTP Server Version 2.4 Documentation. Luettavissa: https://httpd.apache.org/docs/2.4/. Luettu: 7.9.2024.

W3 Schools 2024. HTML Language Code Reference. Luettavissa: https://www.w3schools.com/tags/ref_language_codes.asp. Luettu: 7.9.2024.
