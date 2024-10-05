# h7 Maalisuora

> ## Tiivistelmä
>
> Raportissa esitellään ensin "Hei maailma!"-koodi kolmella kielellä, minkä jälkeen Linuxiin luodaan uusi komento kaikkien koneen käyttäjien käytettäväksi. Tämän jälkeen suoritetaan 2,5 tunnin aikahaaste, jona aikana pyritään suorittamaan kokonaan edellisen kevään kurssin arvioitava laboratorioharjoitus.

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 777/951 GB vapaana

## "Hei maailma" eri kielillä

Tehtävässä oli tarkoituksena kirjoittaa "Hei maailma"-koodi kolmella eri kielellä ja suorittaa jokainen koodi komentorivillä. Käytin koodien kirjoittamisessa apuna Karvisen (27.9.2018) artikkelia, josta valitsin käytettäviksi kieliksi Pythonin, Bashin ja C:n.

0:00 Tein ensiksi kotihakemistooni uuden hakemiston "Koodit" komennolla `mkdir Koodit`, jonne suunnittelin tekeväni tämän viikon tehtävät. Lisäksi päätin kirjoittaa jokaisen koodin itse käsin, jotta paremmin oppisin ymmärtämään koodin tuottamista sen sijaan, että vain kopioisin kaiken suoraan artikkelista. Siirryin juuri luomaani hakemistoon komennolla `cd Koodit` ja loin sinne komennolla `micro hei_maailma.py` Micro-editorilla uuden python-tiedoston, johon "koodasin" tehtävänannon (ks. ensimmäinen alla oleva kuva koodista). Tallennettuani tiedoston palasin komentoriville ja ajoin koodin komennolla `python3 hei_maailma.py` (ks. jälkimmäinen kuva alla).

![maailma python koodi](https://github.com/user-attachments/assets/dc04606d-012d-4367-bc00-24451cbef09c)

![maailma python](https://github.com/user-attachments/assets/744b2d4b-9635-4055-99e3-9f24ed87e322)

0:01 Seuraavaksi lähdin luomaan edellä olevan toteutuksen Bashilla. Käytin jälleen Microa luomaan "hei_maailma.sh"-tiedoston, johon kirjoitin "Hei maailma!". Tallensin tiedoston ja yritin ajaa sitä komentorivillä komennolla `bash hei_maailma.sh`, mutta sain ilmoituksen, ettei komentoa "Hei" löytynyt. Ajattelin sitten, että Karvisen (27.9.2018) artikkelissa mainitut heittomerkit tekstin ympärillä olivat aiheelliset, joten muokkasin nämä mukaan tiedostoon. Koodi ei kuitenkaan suostunut vieläkään toimimaan, vaan sain edelleen saman virheilmoituksen kuin edellä. Hetken tuijotettuani Karvisen (27.9.2018) artikkelia muistin keskiviikon luennolta, että Bashissä ajetaan komentorivikomentoja, ja tämän myötä ymmärsin, että "echo" oli osa vaadittua koodia. Muokkasin `echo`-komennon osaksi koodiani (ks. ensimmäinen alla oleva kuva), jonka jälkeen sain ajettua onnistuneesti komennon `bash hei_maailma.sh` (ks. jälkimmäinen alla oleva kuva).

![maailma bash koodi](https://github.com/user-attachments/assets/bb51edee-2f46-4fbb-aa17-1e53226b6fda)

![maailma bash](https://github.com/user-attachments/assets/c566c3e0-0aec-434b-b67a-9d687bbb7333)

0:03 Lopuksi loin toteutuksen C:llä. Jälleen Microa hyödyntäen loin tiedoston hello_maailma.c, johon kirjoitin tällä kertaa tarkasti Karvisen (27.9.2018) artikkelia mukaillen oikean koodin (ks. ensimmäinen alla oleva kuva). Käänsin komennon ajettavaksi komennolla `gcc hei_maailma.c -o hei_maailmac`, jonka jälkeen koodin ajo onnistui komennolla `./hei_maailmac` (ks. jälkimmäinen alla oleva kuva).

![maailma c koodi](https://github.com/user-attachments/assets/1ff79bac-673f-4f51-98b5-74638669e19d)

![maailma c](https://github.com/user-attachments/assets/4ac542c4-f43e-4b59-a9b0-967119ddd599)

## b) Uuden komennon luonti kaikkien käyttöön

0:05 Tehtävässä oli tarkoituksena luoda uusi komento Linuxiin, jota kaikki koneen käyttäjät voisivat käyttää. Käytin apunani Karvisen (4.12.2007) artikkelia aiheesta. Aloitin luomalla Microlla tiedoston "poyta", jonne kirjoitin Karvisen (4.12.2007) artikkelin mukaisesti ensimmäiselle riville tekstin "#!/bin/bash", jonka tarkoituksena on kertoa käyttöjärjestelmälle kyseessä olevan sarjan komentoja, jotka käännetään Bashilla (Mishra 22.2.2018). Tämän jälkeen kirjoitin ajettavaksi komennoksi `echo` ja tämän perään tekstin "(╯°□°）╯︵ ┻━┻" (ks. kuva alla lopullisesta koodista). Komennon tarkoitus onkin päästellä höyryjä pihalle.

![poyta koodi](https://github.com/user-attachments/assets/62e6ede9-bd86-48d3-bbcc-0d50831251ac)

Tämän jälkeen annoin komennolla `chmod a+x poyta` tiedostolle suoritusoikeudet, jonka jälkeen testasin komennolla `./poyta`, että ajaminen onnistuu paikallisesti. Todettuani tämän toimimisen kopioin tiedoston hakemistoon /usr/local/bin/, jotta se olisi kaikkien käyttäjien käytettävissä. Unohdin ensimmäisellä yrityksellä sudon, joten jouduin ajamaan komennon uudelleen. Siirryin sitten pois Koodit-hakemistosta ja testasin onnistuneesti, että `poyta`-komento oli käytettävissä (ks. alla oleva kuva).

![poyta ajo](https://github.com/user-attachments/assets/2b6a15bd-6d8d-436e-9518-2a06c0b9d7ab)

## c) Vanha laboratorioharjoitus

Tehtävässä oli tarkoituksena valita jonkin aiemman kurssitoteutuksen viimeinen laboratorioharjoitus, joten valitsin kevään 2024 harjoituksen (ks. Karvinen 12.3.2024), koska ajattelin tämän antavan ajankohtaisen vastineen tälle toteutukselle. Huomasin tehtäviä silmäillessä, että joitain tehtäviä en pystyisi tekemään (esim. tietokannan rakentaminen), mutta ajoittain soveltaisin näihin kohtiin tällä kurssilla olleita asioita siten, miten mahdollista. Päätin myös, että tekisin harjoituksen kuin itse koetilanteessa, joten annoin käyttööni 2,5 tuntia reaaliaikaa tekemiseen ja raportin kirjoittamiseen, jotta saisin paremman kuvan, miten saan tehtyä asioita kiivaammalla temmolla. Tästä johtuen raportointityylini tässä tehtävässä muistuttaa myös enemmän harjoitusta kuin aiempia tämän kurssin raporttejani, joskin puhtaasti harjoituksen tyyliä en ota käyttöön. Lisäksi vaikka luon raportin virtuaalikoneelle, kirjoitan sen todellisuudessa tänne. Myös lähdeviitteet on lisätty vasta ajan loppumisen jälkeen.

### a) Taustatiedot

0:00 Loin kotihakemistooni uuden hakemiston "report" ja sen sisälle tiedoston "index.md", jonne kirjoitin tarvittavat tiedot (ks. kuva alla).

![a) taustatiedot](https://github.com/user-attachments/assets/edff21eb-3e9c-4ace-a37c-03c3d5b65c29)

### b) Tiivistelmä

Tehtävät a)-h1) tehty ja osoitettu toimivaksi. Tehtävä h2) jäänyt vajaaksi.

### c) Ei kolmea sekoseiskaa

0:04 Suojasin raporttini `chmod 700 index.md`-komennolla, mikä näkyy `ls -l index.md`-komennolla (ks. kuva alla).

![c) sekoseiska](https://github.com/user-attachments/assets/f2093d86-ccad-4bc7-bf5b-96286b2d1d42)

### d) 'howdy'

0:10 Etsin tiedon, millä komennolla saadaan tulostettua päivämäärä (Gite 5.4.2024). Loin Microlla howdy-tiedoston, johon kirjoitin oikean koodialun (vrt. tämän viikon b-tehtävää) ja `date`-komennon. Annoin tiedostolle tarvittavat oikeudet, jonka jälkeen se toimi paikallisesti. Siirsin sitten sudon avulla tiedoston oikeaan hakemistoon, jolloin se alkoi toimimaan kaikilla käyttäjillä (ks. kuva alla).

![d) howdy](https://github.com/user-attachments/assets/258acd9c-9001-484a-911a-7120584c0f53)

### e) Etusivu uusiksi

0:19 Apache oli jo valmiina asennettuna virtuaalikoneelle, joten en lähtenyt sitä poistamaan varta vasten. Päätin vain suoraan tehdä uuden nettisivun, jonka asettaisin näkyville. [Lähteenä Karvinen 10.4.2018] Tein conf-tiedoston sivulle ai.kakone ja tällä kertaa huomasin typon jo suhteellisen nopeasti (ks. alla oleva kuva).

![e) ai kakone conf](https://github.com/user-attachments/assets/49c9e74d-690f-4430-8ed6-efaf4a0ced1f)

0:31 [Pohjana LeeviRaussi 9.9.2024] Otin edellisellä viikolla luodun raussi.me.static-sivun conf-tiedoston alas ja laitoin AI Kakoneen conf-tiedoston päälle bootaten tämän jälkeen Apachen. Loin sitten aikakone-hakemistoon index.html-tiedoston, johon kirjoitin HTML-koodilla pienen etusivun "AI Kakone"-yritykselle. Sivu lähti suoraan toimimaan koneen omassa IP-osoitteessa 127.0.0.1 (ks. ensimmäinen kuva alla) sekä `curl`-komennolla (ks. toinen kuva alla). Lopuksi säädin vielä hakemistoihin ja tiedostoihin liittyvien oikeuksien kanssa päätyen lopulta antamaan sekä report-hakemistolle että index.html-tiedostolle execute-oikeudet niin `chmod ugo+x` komentoa käyttäen (ks. viimeinen alla oleva kuva).

![e) ai kakone selain](https://github.com/user-attachments/assets/8b9a3250-806f-4f8b-8c85-db43dd6b7f82)

![e) curl](https://github.com/user-attachments/assets/064b20ed-4aff-493a-975e-c7513d518669)

![e) oikeudet](https://github.com/user-attachments/assets/7f3a953c-c405-4ada-99c6-fd1bcecd24be)

### g) Salattua hallintaa

0:54 SSH-palvelin on jo asennettuna virtuaalikoneelle, joten ohitan tämän vaiheen. Loin uuden käyttäjän "Leevi Raussi test" komennolla `sudo adduser lerate01` (Karvinen 19.9.2017) syöttäen vaaditut tiedot (ks. ensimmäinen alla oleva kuva). Ensimmäinen ssh-kirjautumisyritys kariutui siihen, että unohdin käyttäjätunnuksen perässä olevan "01" kirjoittamisen, mutta korjattuani tämän virheen pääsin onnistuneesti kirjautumaan sisälle (ks. jälkimmäinen alla oleva kuva).

![g) adduser](https://github.com/user-attachments/assets/5a694b9f-044b-48f8-a2a0-a217c7172252)

![g) ssh salasana](https://github.com/user-attachments/assets/86fc0f34-1624-46be-b775-e1664bc405c0)

1:04 Olen aiemmin kurssilla luonut jo julkisen avaimen, joten hyödynnän tässä sitä. Kaivoin muutaman viikon takaisesta raportistani komennon `ssh-copy-id` (LeeviRaussi 23.9.2024), jolla sain siirrettyä julkisen avaimen lerate01-käyttäjälle. Tämän jälkeen kirjautuminen onnistui salasanattomasti (ks. alla oleva kuva).

![g) julkinen](https://github.com/user-attachments/assets/7c595136-53f3-41a3-83ee-0fbf9ce23409)

### h) Djangon lahjat, h) Tuotantopropelli

1:12 Näissä tehtävissä pitäisi asentaa Django ja tehdä tietokanta, sekä asettaa tämä näkyviin localhostin etusivulle. Koska kurssilla ei ole tehty tätä, muokkaan tehtävää sen verran, että hyödynnän jo asentamaani Virtualenv-asennusta, mutta luon uuden virtuaaliympäristön aikakone-hakemistoon, jonne luon uuden projektin, jossa toteutan samanlaisen Python-ohjelman luonnin kuin edellisellä viikolla. [Pohjana tässä tehtävässä käytetty LeeviRaussi 30.9.2024] Aloitin luomalla uuden virtuaaliympäristön, ja siirryin sen sisälle tarkistaen myös, että olin varmasti oikeassa hakemistossa. Tämän jälkeen tein Djangon asennusta varten tekstitiedoston, minkä jälkeen asensin tuoreimman version Djangosta (ks. alla oleva kuva).

![h) virtualenv](https://github.com/user-attachments/assets/409f21e5-630a-478b-a1a0-ebd9fcacf57c)

1:25 Aloitin Djangossa uuden projektin "aikakone" ja käynnistin sitten Djangon palvelimen. Edellisen viikon tapaan sain herjat puutteellisista siirroista, joten tein nämä ensin (ks. ensimmäinen alla oleva kuva), jonka jälkeen palvelin käynnistyi kiltisti (ks. jälkimmäinen alla oleva kuva).

![h) projekti luonti](https://github.com/user-attachments/assets/48e3849c-f278-4d6f-9996-31370f2cc7ac)

![h) Django eka](https://github.com/user-attachments/assets/4603e83d-4de7-48ca-a9a1-aa91b3311405)

1:35 Loin Djangoon pääkäyttäjän "ultimaattinen", jolle generoin `pwgen`-komennolla salasanan toisella komentorivillä (ks. ensimmäinen kuva alla). Tämän jälkeen pääsin kirjautumaan onnistuneesti sisään Djangon pääkäyttäjähallintaan osoitteessa 127.0.0.1:8000/admin (ks. jälkimmäinen kuva alla).

![h) ultimaattinen admin](https://github.com/user-attachments/assets/3941fc82-6ee7-4058-96b0-97e48960ea6d)

![h) django admin](https://github.com/user-attachments/assets/4edf7eee-1a5e-4c31-b8bf-b696df8e313d)

1:14 En tällä kertaa luonut ylimääräistä käyttäjää, vaan lähdin suoraan luomaan crm-lisäohjelmistoa. Komento `./manage.py startapp crm` loi ohjelman. Lisäsin projektin asetuksiin merkinnän tästä ohjelmasta, minkä jälkeen muokkasin crm-ohjelmiston models- (ks. ensimmäinen alla oleva kuva) ja admin-tiedostojen (ks. jälkimmäinen alla oleva kuva) koodit sopiviksi. Testasin ja huomasin sivujen bugaavan, minkä jälkeen huomasin unohtaneeni suorittaa `migrate`-komennot (ks. kolmas alla oleva kuva). Tämän jälkeen crm-ohjelmisto alkoi toimia Admin-käyttöliittymässä (ks. viimeinen alla oleva kuva).

![h) models koodi](https://github.com/user-attachments/assets/0dcf31c0-e24a-4441-b14c-1795457d6b68)

![h) admin koodi](https://github.com/user-attachments/assets/caae43f7-87b7-4c03-9665-ee444a50cb3e)

![h) crm komennot](https://github.com/user-attachments/assets/65d638d3-bec7-43c7-ac18-717c821e2842)

![h) crm toimii](https://github.com/user-attachments/assets/0787bf04-6994-40a7-83e4-28dffee2fdf1)

1:31 Lähdin sitten yrittämään saada Djangon näkymään localhostissa Apachen kautta. [Tästä eteenpäin kirjoitus tapahtuu yliajalla] Koska minulla oli jo käytännössä kaikki tarvittava koneella, aloin suoraan muokkaamaan aikakone.conf-tiedostoa. Tämä myös osoittautui suureksi haasteeksti, sillä ensinnäkään itselläni ei ollut "staattista" /static/-hakemistoa, jonka kanssa aiemmin on työskennelty ja joka sisältää itsessään käytettävän sivun. Yritin muokata tiedoston määritelmiä Karvisen (13.2.2022) artikkelin ohjeiden mukaisesti pyrkien hyppäämään /static/-hakemiston yli ja osoittamaan suoraan index.html:ään. Tämä ei tuottanut kuitenkaan tulosta, joten päätin kuitenkin luoda static-hakemiston, jonne kopioin käyttämäni index.html:n. Bootattuani Apachen sain yllätyksekseni 403-virheviestin `curl`-komennosta (ks. ensimmäinen kuva alla). Tässä kohtaa lähdin metsästämään typoja conf-tiedostossa, mutta en huomannut mitään ongelmia verratessani Karvisen (13.2.2022) artikkeliin. Lopulta ajaessani uudelleen komennon `/sbin/apache2ctl configtest` nähdäkseni toimiiko se edelleen, huomasin tämän valittavan, ettei TWSGI-muuttujaa oltu määritelty (ks. toinen kuva alla). Tarkastaessani jälleen kerran conf-tiedostoa huomasin viimein, että olin heti alussa unohtanut kirjoittaa toiselle riville TWSGI:n Definen perään (ks. kolmas kuva alla korjatusta conf-tiedostosta). Nyt kun käynnistin Apachen uudelleen sain Djangon näkymään localhostissa (ks. viimeinen kuva alla).

![h) apache saato](https://github.com/user-attachments/assets/b8ac0690-5ee9-467b-b75d-eacb3b31f63b)

![h) configtest](https://github.com/user-attachments/assets/b7a30e0e-d806-42ec-97f7-86f4fbac8402)

![h) lopullinen conf](https://github.com/user-attachments/assets/10173b8f-16b2-4f7d-a78b-44278de98cb8)

![h) localhost django](https://github.com/user-attachments/assets/5ec94783-cc4e-4cf3-bfe7-08f4cf57fc02)

Tässä kohtaa minulta kuitenkin loppui aika. Aivan maaliin saakka en siis päässyt (DEBUG-tilan poisto ja CSS-tyylien muokkaus jäivät uupumaan), mutta joitain huomionarvoisia nostoja sain kuitenkin näistä viimeisistä virheistäni tehtyä. Tärkeimpänä näistä minun ei olisi kannattanut muuttaa tekemääni aikakone.conf-tiedostoa static-hakemistoon sopivaksi, vaan tämän kopioiminen olisi ollut järkevämpi vaihtoehto. Tällöin olisin todennäköisesti saanut ainakin ensiksi localhostissa näkymään alkuperäisen sivun ja localhost/static/index.html-osoitteessa "staattisen"-sivun. Tämän jälkeen mikäli Django ei pelaisi yhteen alkuperäisen aikakoneen index.html kanssa, voi sen sulkea pois käytöstä.

## Lähdeluettelo

Gite, V. 5.4.2024. Display Date And Time In Linux. Luettavissa: https://www.cyberciti.biz/faq/linux-display-date-and-time/. Luettu: 5.10.2024.

Karvinen, T. 4.12.2007. Shell Scripting. Luettavissa: https://terokarvinen.com/2007/12/04/shell-scripting-4/. Luettu: 5.10.2024.

Karvinen, T. 19.9.2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Luettu: 5.10.2024.

Karvinen, T. 10.4.2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Luettu: 5.10.2024.

Karvinen, T. 27.9.2018. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/. Luettu: 5.10.2024.

Karvinen, T. 13.2.2022. Deploy Django 4 - Production Install. Luettavissa: https://terokarvinen.com/2022/deploy-django/. Luettu: 5.10.2024.

Karvinen, T. 12.3.2024. Final Lab for Linux Palvelimet 2024 Spring. Luettavissa: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/. Luettu: 5.10.2024.

LeeviRaussi 9.9.2024. h3 Hello Web Server. Luettavissa: https://github.com/LeeviRaussi/linux-palvelimet/blob/main/h3_Hello_Web_Server.md. Luettu: 5.10.2024.

LeeviRaussi 23.9.2024. h5 Nimekäs. Luettavissa: https://github.com/LeeviRaussi/linux-palvelimet/blob/main/h5_Nimekas.md. Luettu: 5.10.2024.

LeeviRaussi 30.9.2024. h6 Hello Django. Luettavissa: https://github.com/LeeviRaussi/linux-palvelimet/blob/main/h6_Hello_Django.md. Luettu: 5.10.2024.

Mishra, S. 22.2.2018. (#!/bin/bash ) What exactly is this ?. Luettavissa: https://medium.com/@codingmaths/bin-bash-what-exactly-is-this-95fc8db817bf. Luettu: 5.10.2024.
