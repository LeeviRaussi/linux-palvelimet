# h5 Nimekäs

> ## Tiivistelmä
>
> Raportissa luodaan uusia sivuja Apache-virtuaalipalvelimelle, jotka linkittyvät toisiinsa. Lisäksi käyttöön otetaan uusia alidomaineja ja SSH-avainpari mahdollistamaan automatisoitu kirjautuminen salasanan korvaamiseksi. Lopuksi tarkastellaan miten `host` ja `dig` komennot toimivat.

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 779/951 GB vapaana

Keskiviikon luennolla hankittiin GitHub Educationin avulla Namecheapistä raussi.me -domain, jota näissä tehtävissä hyödynnetään. Myös koska tämä hankittiin jo ennen tehtävien tekoa, hankkimisprosessiin ei perehdytä sen enempää.

## a) Kotisivu

0:00 Tehtävässä oli tarkoitus tehdä kolmen sivun kotisivukokonaisuus, joten lähdin luomaan sivuja koneellani olevalla virtuaalikoneella, enkä suoraan palvelimelle, jotta pystyisin testaamaan sivujen toimintaa ennen kuin laittaisin ne näkyviin. Päätin myös hyödyntää jo aiemmin luomiani hattu.example.com-sivujen tiedostoja, joten loin ensin kotihakemistoni nettisivuhakemistoon raussi.me-kansion ja kopioin sitten tarvittavat tiedostot uusilla nimillä oikeisiin sijainteihin muokaten tiedostojen sisällöt sopiviksi. Laitoin tämän jälkeen sivut päälle, käynnistin Apachen uudelleen, otin hattu.example.comin sivut alas ja käynnistin taas Apachen uudelleen (ks. alla oleva ensimmäinen kuva käytetyistä komennoista). Uudet sivut tulivat onnistuneesti näkyviin nettiselaimessa localhost-osoitteessa (ks. jälkimmäinen alla oleva kuva).

![raussi me pohja](https://github.com/user-attachments/assets/a2efbfb9-d000-41b6-ad23-a2750d502d65)

![virtuaali raussi me pohja](https://github.com/user-attachments/assets/adb60d46-829d-4a9f-99b3-516f8b490573)

0:07 Seuraavaksi loin kaksi uutta sivua kopioimalla `cp`-komennolla index.html:n linux-palvelimet.html ja yliopisto.html tiedostoiksi (ks. kuva alla).

![Kopiot](https://github.com/user-attachments/assets/d9222857-371f-4690-a74d-196e5ce16c5a)

Kun aloin muokkaamaan näihin tiedostoihin linkkejä takaisin etusivulle, aloin etsimään tietoa, miten tämä tulisi toteuttaa. Hyperlinkki tulisi luoda käyttäen koodia `<a href="[osoite]">teksti</a>` (W3Schools 2024), mutta itse osoite oli vielä epäselvä. Ensiksi ajattelin kokeilla Susannan (2024) artikkelissa mainittua userdir-moduulia, jonka sain käyttöön komennolla `sudo a2enmod userdir`. En kuitenkaan saanut sivuja näkymään heti, joten tutkin lisää, miten userdir-moduuli toimii. ASF:n (2024) dokumentaatiota lukiessani päädyin luopumaan moduulin käytöstä, koska tämä ei mielestäni vastaisi kunnolla sitä, mitä halusin, minkä lisäksi dokumentaatiossa mainitut mahdolliset tietoturvaongelmat vaikuttivat päätökseeni. Kyseinen artikkeli kuitenkin myös avasi sitä, miten osoitteet toimivat hakemistoissa, ja sainkin tätä kautta localhost/linux-palvelimet.html-sivun auki (ks. alla oleva kuva).

![Toimiva localhost toinen sivu](https://github.com/user-attachments/assets/49fcef1b-305e-4033-9cbe-76f0400752c7)

Kun nyt tiesin kahden toisen sivun osoitteet, niin lähdin muokkaamaan etusivun html-tiedoston `href`-koodeja alasivujen osoitteiden muotoon "localhost/linux-palvelimet.html" ja "localhost/yliopisto.html". Tämä ei kuitenkaan toiminut kuten olin ajatellut (ks. alla oleva kuva).

![Buginen href](https://github.com/user-attachments/assets/7efc4fc3-a9c5-4494-9b5f-36f1e230131b)

Osoitekentän perusteella muokka `href`-koodia (ks. ensimmäinen alla oleva kuva), minkä myötä hyperlinkit alkoivat toimia kunhan käynnistin Apachen aina uudelleen (ks. jälkimmäinen kuva alla kaikista komennoista tässä vaiheessa).

![Korjattu href](https://github.com/user-attachments/assets/3f75a30b-ba6d-4973-a846-7acdb94b8e5e)

![userdir saato](https://github.com/user-attachments/assets/6de149e5-1431-4071-aa93-645bb7fcf5ef)

0:28 Sivujen toimiessa virtuaalikoneella lähdin siirtämään niitä virtuaalipalvelimelle. Käytin tässä Karvisen (3.2.2020) artikkelista löytyvää `scp`-komentoa. Hakemisto "raussi.me" siirtyi palvelimelle ongelmitta, mutta siirtäessäni conf-tiedostoa minulla oli pieniä ongelmia, kun syötin useamman kerran palvelimen salasanan, kun minun olisi pitänyt antaa `sudo`-komennon takia virtuaalikoneen salasana. Tästä ehkä opin, ettei välttämättä ole järkevää nimetä näiden kahden käyttäjiä samalla nimellä selkeyden vuoksi. Lopulta siirto onnistui (ks. alla oleva kuva).

![scp siirto](https://github.com/user-attachments/assets/00bb5fd4-e817-4867-8521-5b8a62b69908)

Siirryin tämän jälkeen toisella komentorivillä virtuaalipalvelimen puolelle ja siirsin edellä siirtämäni conf-tiedoston oikeaan hakemistoon `mv`-komennolla (ks. ensimmäinen alla oleva kuva). Tämän jälkeen tein virtuaalipalvelimella samanlaisen avaamis-sulkemis prosessin raussi.me- ja hattu.example.com-tiedostoille kuin tein edellä virtuaalikoneellani. Hetken odoteltuani testasin raussi.me sivun toimimisen niin virtuaalikoneellani kuin toisella koneella ja totesin niin etusivun kuin myös sivujen raussi.me/yliopisto.html ja raussi.me/linux-palvelimet.html toimivan (ks. jälkimmäinen alla oleva kuva).

![conf siirto](https://github.com/user-attachments/assets/17e0dc61-7870-4c36-bedc-a41b53c3a84a)

![Toimiva raussi me](https://github.com/user-attachments/assets/56ad9940-b543-45f6-8508-6fa5663fb18e)

## b) Alidomain

0:35 Alidomaineita pystyy käyttämään osoittamaan verkko-osoitteeseen aliaksina (Elz & Bush 1997). Namecheap (2024) huomauttaa, että käyttäessä CNAME-tietuetta, tulisi olla olemassa jokin muukin A-tietue kuin pelkkä @-domain. Tämän takia päädyinkin tekemään Namecheapin Advanced DNS -asetuksissa A-tietueena www-subdomainin ja CNAME-tietueena poc (proof of concept) alidomainit, jotka toimivat aliaksina verkkosivuilleni (ks. kuvat alla).

![Subdomainit](https://github.com/user-attachments/assets/8db4638b-1556-49c2-9ee0-1bf3e2326a5a)

![www toimii](https://github.com/user-attachments/assets/32e82ef8-5ee1-4236-866b-d61885640f99)

![poc toimii](https://github.com/user-attachments/assets/00bc83e9-3e79-4d43-9149-e9774e0df5ea)

## c) Pubkey

0:36 Tehtävässä oli tarkoitus ottaa yksityinen-julkinen avainpari käyttöön virtuaalipalvelimelle kirjautuessa korvaamaan tähän asti käytössä ollut salasana. Googlaamalla löysin Gitin (2024) artikkelin asiasta ja tarkistin `man ssh-keygen` komennolla, että kyseessä oli tosiaan oikea työkalu. Artikkelin ohjeiden mukaisesti tarkistin ensin .ssh-hakemiston sisältä, ettei julkista avainta ollut vielä luotuna, ja tämän jälkeen loin sen komennolla `ssh-keygen -o` (ks. alla oleva kuva).

![Julkinen luonti](https://github.com/user-attachments/assets/3f9080aa-fa30-4df5-b3ba-0d5ca1aa760f)

Siirryin sitten palvelimentarjoajani DigitalOceanin sivuille, ja kun en huomannut itse palvelimen sivulla mitään mahdollisuutta julkisen SSH-avaimen käyttöön ottoon, tarkastin Settings-välilehden, jonka Security asetuksista pystyin lisäämään julkisen avaimeni tililleni. Yritin tämän jälkeen kirjautua palvelimelleni, mutta minulta kysyttiin salasanaa, joten jotain oli vielä pielessä. Huomasin sitten DigitalOceanin asetuksissa juuri yhdistetyn SSH-avaimen alapuolella linkin artikkeliin, jossa neuvottiin SSH-avaimen käyttöönottoprosessi. Minulta uupui vielä `ssh-copy-id leevi@188.166.34.160` komento, jolla siirsin julkisen avaimeni myös virtuaalipalvelimelleni (DigitalOcean 15.12.2021), ja tämän myötä kirjautuminen onnistui ilman salasanaa (ks. kuva alla).

![Avainpari toimintaan](https://github.com/user-attachments/assets/a93dda12-e680-431a-a125-e5186a01ae02)

## d) Komennot `host` ja `dig`

Komento `man host` kertoi, että komentoa `host` käytetään selvittämään tietoja liittyen DNS:ään. Näitä tietoja ovat esimerkiksi IP-osoite ja sähköpostipalvelimet, joita sivu hyödyntää. Nämä tulivat hyvin esiin testatessani komentoa omaan sivuuni (raussi.me) (ks. kuva alla). Komennon pitäisi myös toimia IP-osoitteella, mutta jostain syystä tämä tuotti virheen itselläni. Samannäköinen virhe oli tullut vastaan keskiviikon luennolla, jolloin asiaan suhtauduttiin "tokenee ajan kanssa", joten en jäänyt murehtimaan tätä sen pidemmäksi aikaa. Testasin myös alidomainini poc.raussi.me, joka tunnistettiin oikein raussi.me aliakseksi. Sähköpostipalvelimet, joita komento tuotti, näyttivät olevan samaa muotoa kuin Namecheapin-sivujen Advanced DNS -välilehden sähköpostiasetukset.

![host raussi me](https://github.com/user-attachments/assets/84d65b0c-582e-4b9b-8db7-207e60d1bd94)

Mikäli `host`-komentoa ei lähdetä tarkemmin määrittelemään erinäisiä argumentteja, saadut tulokset eivät poikkea kovinkaan paljoa vaikka siirryttäisiin isommillekin verkkosivuille. Tästä esimerkkinä toimivat hyvin kruunuradio.fi, hifi-laitteisiin erikoistunut myymälä, sekä maailman suurin hakukone Google. Kun molempia sivuja tarkasteltiin komennolla, eivät saadut tulokset sinällään poikenneet raussi.me-tuloksista, vaan näillekin annettiin kuuliaisesti Ipv4-osoite (ja Googlen tapauksessa myös IPv6-osoite) sekä yksittäinen sähköpostipalvelin. Näiden sivujen kohdalla tosin käänteinen haku IP-osoitteella tuotti myös tuloksen, Googlen kohdalla jopa neljä eri PTR-tietuetta osoittaa sivustoon (ks. kuva alla). Tämä nostaa myös esiin mahdollisuuden, että oman sivuni PTR-tietueessa saattaisi olla ongelma.

![host muut](https://github.com/user-attachments/assets/6adceb7c-ba98-4b2e-a2c3-d3da8fff7c75)

Komennon `dig` kanssa törmäsin heti ongelmiin, sillä ensinnäkään kyseisen komennon manuaalia ei löytynyt komennolla `man dig`, komentoa ei ollut virtuaalikoneella, eikä sellaista ohjelmaa pystynyt asentamaan (ks. kuva alla).

![no dig](https://github.com/user-attachments/assets/e36007e0-2eb7-4a14-b197-6b86fb20e8f7)

Googlaamalla löysin Giten (19.3.2024) artikkelin, joka kertoi, että `dig` löytyisi osana dnsutils-nimistä pakettia. Asensin kyseisen paketin komennolla `sudo apt-get -y install dnsutills`, minkä jälkeen komento `man dig` tuotti tulosta. Myös komento `dig` lähti toimimaan, ja ajoinkin komennon kaikkiin kolmeen edellä mainittuihin sivuihin (ks. kuvat alla). Komennon manuaali osasi avata, että ilman tarkempia argumenttimäärittelyjä komento hakee tietoa kohteen A-tietueesta. Tämä tieto ei kuitenkaan yksissään riittänyt alla olevien kuvien tietojen analysointiin, joskin A-tietueen sijainti tuloksissa valkeni heti. Tarkempaa analyysiä varten löysin Mutkawoan (8.11.2015) artikkelin aiheesta, joka avasi hyvin tulosten eri kohdat. Ensinnäkisin "global options: +cmd" kertoo, ettei mitään ylimääräisiä argumentteja ole käytetty komennon yhteydessä. Tätä tietoa seuraa sitten ID-numero tehdylle kyselylle, mikä poikkeaakin jokaisessa haussa. Flagsit qr, rd ja ra headerit ovat pelkästään käytössä tässä oletusarvoisessa kyselyssä. Kaikkiin sivuihin tehtiin yksi kysely, ja tällä kertaa jokaisen tapauksessa saatiin yksi vastaus, minkä lisäksi Googlen ja raussi.me tapauksessa saatiin myös yksi ylimääräinen tieto, joka ilmeisesti vastaa optionaalista pseudo-osiota. Tätä seuraa kysely-osio, joka kertoo minne kysely on kohdistettu, eli nimi- tai IP-osoite, ja mitä tietuetta ollaan haettu (tässä A). Vastaus-osiossa saadaan tieto siitä, kuinka kauan sivua pidetään DNS-välimuistissa (TTL) ennen kuin siitä pyydetään uutta versiota. Erityisesti raussi.me kohdalla 300 (sekuntia) vastaa juuri sitä arvoa, mikä määriteltiin keskiviikon luennolla Namecheapissä (5 minuuttia). Lisäksi saadaan tieto, mistä tietueesta on kyse ja mikä on haetun sivun IP-osoite. Viimeisessä osiossa on metatietoa siitä, kauanko kyselyn teko kesti, mistä se tehtiin, koska se tehtiin, ja kuinka suuri saadun viestin koko oli tavuina. (Mutkawoa 8.11.2015.)

![dig raussi me](https://github.com/user-attachments/assets/4110b8e0-141b-45f4-8fbd-9aab684831af)

![dig kruunuradio](https://github.com/user-attachments/assets/34fa0f3e-8bde-4d64-b124-95dd1ccd7c3e)

![dig google](https://github.com/user-attachments/assets/4301600b-ece3-4ea6-ab4e-98d2580f2818)

## Lähdeluettelo

DigitalOcean 15.12.2021. How To Set Up SSH Keys on Ubuntu 12.04. Luettavissa: https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2. Luettu: 22.9.2024.

Elz, R. & Bush, R. 1997. Clarifications to the DNS Specification. Luettavissa: https://datatracker.ietf.org/doc/html/rfc2181. Luettu: 22.9.2024.

Git 2024. 4.3 Git on the Server - Generating Your SSH Public Key. Luettavissa: https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key. Luettu: 22.9.2024.

Gite, V. 19.3.2024. How to install dig on Debian Linux 12/11/10. Luettavissa: https://www.cyberciti.biz/faq/debian-9-dig-command-not-found-how-to-install-dig-on-debian/. Luettu: 22.9.2024.

Karvinen, T. 3.2.2020. Command Line Basics Revisited. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited. Luettu: 22.9.2024.

Mutkawoa, N. J. 8.11.2015. Anatomy of a simple dig result. Luettavissa: https://tunnelix.com/anatomy-of-a-simple-dig-result/. Luettu: 22.9.2024.

Namecheap 2024. Which record type option should I choose for the information I’m about to enter? Luettavissa: https://www.namecheap.com/support/knowledgebase/article.aspx/579/2237/which-record-type-option-should-i-choose-for-the-information-im-about-to-enter/. Luettu: 22.9.2024.

Susanna 14.2.2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/. Luettu: 13.9.2024.

The Apache Software Foundation 2024. Mapping URLs to Filesystem Locations. Luettavissa: https://httpd.apache.org/docs/trunk/urlmapping.html. Luettu: 22.9.2024.

W3 Schools 2024. HTML Links. Luettavissa: https://www.w3schools.com/html/html_links.asp. Luettu: 22.4.2024.
