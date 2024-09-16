# h4 Maailma kuulee

> ## Tiivistelmä
>
> Raportissa tiivistetään ensin lyhyesti kaksi virtuaalisten pilvipalvelimien käyttöönottoa käsittelevää artikkelia, minkä jälkeen esitetään oma suoritus tästä samaisesta asiasta.

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 781/951 GB vapaana

## x) Tiivistelmät

### Teoriasta käytäntöön pilvipalvelimen avulla (h4) (Susanna 14.2.2022)

- a) Susanna (14.2.2022) hyödynsi tehtävän suorittamisessa GitHub Educationia ja hankki tämän avulla palvelimen käyttöön DigitalOceanilta. Viiden dollarin kuukausimaksulla hän sai Amsterdamissa sijaitsevassa datakeskuksesta käyttöönsä yhden prosessoriytimen, gigan muistia, 25 gigaa SSD-kovalevytilaa ja 1000 gigan verran datan siirtämistä. Lisäksi hän sai GitHub Educationin avulla .me-päättyisen domainnimen käyttöön vuodeksi Namecheapiltä. Molemmissa tapauksissa täytyi kuitenkin luoda alustalle uusi käyttäjätunnus vaikkakin ne myöhemmin yhdistettiin GitHubissa olevaan käyttäjätunnukseen. Lopuksi hän yhdisti juuri luomansa domainnimen osoittamaan virtuaalipalvelimen IP-osoitteeseen. (Susanna 14.2.2022.)
- d) Susanna (14.2.2022) pääsi hallinnoimaan luomaansa virtuaalipalvelinta ottamalla siihen SSH-etäyhteyden omalta koneeltaan komennolla `ssh root@[IP-osoite]`. Päästyään sisälle virtuaalipalvelimelle hän päivitti asennuslistansa komennolla `sudo apt-get update`, minkä jälkeen hän asensi palomuurin, joka sallii SSH-etäyhteydet komennoilla `sudo get-apt install ufw` (asennus), `sudo ufw allow 22/tpc` (SSH-yhteyksien salliminen) ja `sudo ufw enable` (palomuuri päälle) (Susanna 14.2.2022).
- e) Susanna (14.2.2022) aloitti uuden kotisivun luontiprosessin tekemällä virtuaalipalvelimella olevalle koneelle normaalin käyttäjän, jonka hän liitti osaksi pääkäyttäjäryhmää. Testattuaan uuden käyttäjän toimivan halutulla tavalla, hän sulki root-käyttäjän, jottei sitä pääsisi käyttämään. Tämän jälkeen hän asensi virtuaalipalvelimelle Apache-webbipalvelimen, jonka oletussivun hän sai suoraan toimimaan omalla domainillaan. Sivuston muokkaamista varten virtuaalipalvelimelle asennettiin Micro-editori, jonka avulla luotiin uusi HTML-pohjainen kotisivu. (Susanna 14.2.2022.)
- f) SSH-yhteyden avulla Susanna (14.2.2022) päivitti virtuaalipalvelimensa ohjelmat komennoilla `sudo apt-get update`, `sudo apt-get upgrade` ja `sudo apt-get dist-upgrade`.

### First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS (Karvinen 19.9.2017)

Karvinen (19.9.2017) esittelee artikkelissaan lyhyesti, miten virtuaalipalvelin otetaan käyttöön etänä. Karvinen suosittelee artikkelissaan DigitalOceania virtuaalipalvelimen tarjoajaksi ja Namecheapiä domainnimen tarjoajaksi, koska kyseisissä palveluissa on mahdollista hyödyntää GitHub Educationin opiskelijaetuja. Palvelimen hankkimisen jälkeen siihen otetaan yhteys SSH-yhteydellä kirjautumalla koneelta löytyvälle root-pääkäyttäjälle. Virtuaalipalvelimelle on aiheellista asentaa heti palomuuri, joka sallii SSH-yhteydet. Tämän lisäksi on aiheellista luoda uusi käyttäjä, joka lisätään pääkäyttäjäksi. Tämän jälkeen root-käyttäjä lukitaan tietoturvasyistä komennolla `sudo usermod --lock root` sekä mahdollisuus SSH-yhteyden ottamiseen kyseiseen käyttäjään evätään muokkaamalla komennolla `sudoedit /etc/ssh/sshd_config` tiedostoa siten, että tiedostossa lukee "PermitRootLogin no", minkä jälkeen yhteys käynnistetään uudelleen komennolla `sudo service ssh restart`. Lopuksi tulee päivittää palvelimelta löytyvät ohjelmistot, jotta mahdollisilta tietoturva-aukoilta säästytään. Karvinen myös teroittaa useampaan kertaan, että käyttäjille on annettava hyvät salasanat, jotta vältyttäisiin tietoturvamurroilta. (Karvinen 19.9.2017.)

## a) Oman virtuaalipalvelimen vuokraus

-3 päivää: Aloitin virtuaalipalvelimen hankkimisen liittymällä GitHub Educationiin (2024), jonka kautta oli mahdollisuus saada ilmaiseksi käyttöön tällä kurssilla tarvitsemiani resursseja. Prosessi oli suoraviivaista ehtojen täyttämistä esimerkiksi monivaiheisen tunnistautumisen käyttöön ottamisen muodossa, ja todisteen opinto-oikeudestani sain kuvakaappauksella Haaga-Helian Pepistä hankittavalla todistuksella, josta piilotin pois näkyvistä henkilötunnukseni. Hakemukseni hyväksyttiin vuorokauden sisällä ja kolme päivää myöhemmin sain sähköpostin, että edut olivat käytettävissäni.

0:00 GitHub Educationin kautta sain 200 dollarin edestä krediittejä vuodeksi käyttöön DigitalOceaniin, minkä takia päädyin tähän palvelimentarjoajaan. Klikkasin Student Developer Packin sivuilla DigitalOceanin linkkiä ja pyrin kirjautumaan sisään palveluun GitHub käyttäjälläni. Annoin hyväksyntäni tietojeni antamiseen DigitalOceanille, minkä jälkeen sain virheilmoituksen, ettei kyseisellä sähköpostilla ole olemassa käyttäjätunnusta. Huomasin sitten sivun oikeassa ylälaidassa Sign up -linkin, jota kautta rekisteröidyin GitHub-käyttäjätunnukseni avulla. Prosessissa minun piti antaa maksukorttitietoni ja DigitalOcean teki noin 14 dollarin maksuvarauksen, jonka pitäisi palautua tililleni viikon kuluessa. Annettuani uudelleen luvan GitHubin kautta käyttäjätietojeni yhdistämiseen pääsin viimein sisälle palveluun. Billing-välilehdeltä näin, että 200 dollarin edestä krediittejä oli lisätty onnistuneesti tililleni (ks. kuva alla). Muokkasin lisäksi vielä Billing-välilehden Settingsistä Billing Alertin rajaksi 1 dollarin, jotta varmasti muistaisin sulkea kurssin jälkeen palvelimen, sekä otin Settings-välilehdeltä käyttöön Secure Sign-In:n.

![Krediitit](https://github.com/user-attachments/assets/ab8a650d-4e82-4ebc-b640-3c54b5c8f5c2)

0:05 Lähdin luomaan virtuaalipalvelinta vasemmalla olevan valikon Droplets-välilehdeltä. Palvelimen sijainniksi valitsin Amsterdamin, koska se oli käytännössä lähin EU:n sisällä oleva palvelin (ks. kuva alla).

![Sijainti](https://github.com/user-attachments/assets/478e815f-bd90-47e2-a55e-0da3f611d841)

Käyttöjärjestelmänä jatkoin Debian 12 käyttöä kurssin hengen mukaisesti (ks. kuva alla).

![OS](https://github.com/user-attachments/assets/6765687b-1817-45b1-a866-1b4acbe822d3)

Laitteiston puolesta tarjontaa olisi ollut paljonkin, mutta luennolla annetun ohjeistuksen mukaisesti valitsin tavallisen jaetun prosessorin 25 gigan SSD:llä ja yhdellä gigalla muistia (ks. kuva alla).

![Laitteisto](https://github.com/user-attachments/assets/2038e06a-f4d3-4bee-9dfb-0f95b6cb5568)

Karvisen (19.9.2017) painotusten mukaisesti pyrin luomaan mielestäni vahvan salasanan, jota en ole aiemmin käyttänyt. Viimeistelin luomisprosessin nimeämällä virtuaalipalvelimen suhteellisen geneerisesti ja sijoittamalla sen oletusprojektiini (ks. kuva alla).

![Nimi](https://github.com/user-attachments/assets/9f6e9434-79d7-4478-9ced-e870be90f0ed)

Virtuaalipalvelin ilmestyi heti näkyville, ja nimesin samalla projektin asetuksista projektin uudelleen koskemaan tätä kurssia (ks. kuva alla).

![Valmis](https://github.com/user-attachments/assets/2ccab800-54c4-429d-9b92-47c652b6bf08)

## b) Virtuaalipalvelimen alkutoimet

0:10 Käynnistin Linux virtuaalikoneeni ja pyrin ottamaan yhteyden SSH:lla virtuaalipalvelimeeni komennolla `ssh root@[IP-osoite]` Karvisen (19.9.2017) ohjeiden mukaisesti. Sain kuitenkin virheilmoituksen, että koneellani ei ole ohjelmaa SSH. Päivitin saatavilla olevat ohjelmistot komennolla `sudo apt-get update` ja asensin SSH:n komennolla `sudo apt-get -y install ssh`. Tämän jälkeen sain muodostettua yhteyden virtuaalipalvelimeeni edellä olevalla komennolla. Syötin virtuaalipalvelimelleni antaman salasanan ja pääsin sisälle palvelimelle. Ensiksi päivitin saatavilla olevien ohjelmistojen listan komennolla `sudo apt-get update` ja asensin palomuurin komennolla `sudo apt-get -y install ufw`. Ennen kuin laitoin palomuurin päälle, avasin siihen SSH:ta varten aukon komennolla `sudo ufw allow 22/tcp`, minkä jälkeen laitoin palomuurin päälle komennolla `sudo ufw enable` (ks. kuva alla).

![UFW](https://github.com/user-attachments/assets/0ec7f63e-6a78-42ed-8083-7befa487e5cc)

0:15 Seuraavaksi loin normaalin käyttäjän "leevi" (ks. ensimmäinen kuva alla), jonka lisäsin käyttäjäryhmiin sudo, adm ja admin Karvisen (19.9.2017) ohjeiden mukaisesti. Tämän jälkeen avasin paikallisella virtuaalikoneellani uuden komentorivin ja otin yhteyden virtuaalipalvelimeen komennolla `ssh leevi@[IP-osoite]`. Kirjautuminen onnistui ongelmitta (ks. jälkimmäinen kuva alla).

![adduser](https://github.com/user-attachments/assets/a82ee4e9-0508-4205-85a2-b5848fe1b06f)

![ssh user](https://github.com/user-attachments/assets/558d0e44-5ed2-4211-915e-18a83d836d7b)

0:18 Seuraavaksi lukitsin root-pääkäyttäjän komennolla `sudo usermod --lock root`. Otin myös pois käytöstä mahdollisuuden kirjautua etänä root-käyttäjänä muokkaamalla sshd_config-tiedostoa (ks. ensimmäinen kuva alla). Lopuksi uudelleen käynnistin SSH-palvelun komennolla `sudo service ssh restart`, jotta tekemäni asiat tulisivat voimaan (ks. jälkimmäinen kuva alla).

![permitrootlogin](https://github.com/user-attachments/assets/50219653-be7c-4844-93cd-6ef85a645afa)

![lock root](https://github.com/user-attachments/assets/d7845970-60de-490e-9569-e11186c6ff20)

0:20 Tehtävän lopuksi päivitin palvelimella olevat ohjelmistot komennoilla `sudo apt-get update` ja `sudo apt-get upgrade`.

## c) Weppipalvelin virtuaalipalvelimelle

0:21 Apachen asennusprosessissa turvauduin suoraan edelliseen tehtävääni (ks. LeeviRaussi 9.9.2024) ja kopioin pitkälti sieltä komentoja. Apache asentui komennolla `sudo apt-get -y install apache2`, oletussivulle muokkasin tekstin "Oletussivu" komennolla `echo "Oletussivu"|sudo tee /var/www/html/index.html`, ja tämän toimimisen testasin komennolla `curl localhost`. Kaiken toimiessa halutulla tavalla siirryin suoraan luomaan uuden sivun conf-tiedoston komennolla `sudoedit /etc/apache2/sites-available/hattu.example.com.conf`, jonka muokkasin vastaamaan edellisen viikon tehtävää. Mahdollisesti tulen myöhemmin kurssilla luomaan erinimisen sivun, mutta menin nyt näillä "oletuksilla". Loin uuden kansion omaan kotikansiooni komennolla `mkdir -p /home/leevi/publicsites/hattu.example.com/`, minne julkiset nettisivuni tulevat. Muokkasin lisäksi sivulle tekstin "hattu" komennolla `echo hattu > /home/leevi/publicsites/hattu.example.com/index.html`, minkä jälkeen käytin komentoa `curl -H 'Host: hattu.example.com' localhost` nähdäkseni kaiken toimivan. Sain kuitenkin Apachen oletussivulle muokkaamani tekstin eteeni, ja hetken mietittyäni tajusin, etten ollut laittanut uutta nettisivua koskaan päälle, joten tein sen komennolla `sudo a2ensite hattu.example.com` (ks. kuva alla kaikista näistä vaiheista).

![Alkuoletukset](https://github.com/user-attachments/assets/f7e6ddd8-fd56-48a5-840e-408e08768440)

Käynnistin Apachen uudelleen komennolla `sudo systemctl restart apache2` ja yritin uudelleen edellä ollutta curl-komentoa saaden kuitenkin tällä kertaa 403-virheen (ks. ensimmäinen kuva alla). Miettiessäni mikä oli mennyt vikaan, silmiini osui Karvisen (19.9.2017) ohjeesta kohta, jossa Apachea varten avataan palomuuriin portti, joten tein tämän komennolla `sudo ufw allow 80/tcp`. Virhe kuitenkin säilyi edelleen (ks. jälkimmäinen kuva alla).

![403 curl virhe](https://github.com/user-attachments/assets/7a802c99-3942-4989-816b-e78299817ba5)

![Porttiauki virhe](https://github.com/user-attachments/assets/3cb7ee83-372e-4fc8-9801-c139d83b09d6)

0:30 Testasin nettiselaimella toimiiko Apache ylipäätänsä, ja sain iloiseksi yllätykseni eteeni sivun tekstillä "Oletussivu", kun syötin virtuaalipalvelimeni IP-osoitteen (ks. ensimmäinen kuva alla). Vika siis näyttäisi koskevan vain juuri luomaani sivua. Selasin edellisen viikon tehtävien vinkkejä ja huomasin komennot `chmod ugo+x $HOME $HOME/public_html/` ja `ls -ld $HOME $HOME/public_html/`, jotka oli liitetty 403-virheeseen. Ensimmäisen komennon googlauksen kautta sain selville, että ensimmäillä komennolla annetaan käyttöoikeuksia määäriteltyyn kohteeseen (CETS), ja päätin testata komentoa käytännössä. Sain ensin virheilmoituksen, ettei hakemistoa public_html ole olemassa, mistä ymmärsin, että minun tulisi korvata tämä oman hakemistorakenteeni publicsites-hakemistolla. Komentojen muokkaaminen muotoon `chmod ugo+x $HOME $HOME/publicsites/` ja `ls -ld $HOME $HOME/publicsites/`, ja nyt curl-komento tuotti haluamaani tulosta (ks. jälkimmäinen kuva alla).

![Oletussivu nakyy](https://github.com/user-attachments/assets/674b1af8-d38f-47c6-8202-87d8d6cc6d31)

![403 ratkaisu](https://github.com/user-attachments/assets/bd865007-b3fa-4206-8f7a-e4ef57f614aa)

0:32 Muokkasin edellisen viikon tehtävän mukaisesti Micro-editorissa sivun tiedostoa komennolla `micro /home/leevi/publicsites/hattu.example.com/index.html`, jotta siitä tulisi HTML5 mukainen. Tämän jälkeen otin Apachen oletussivun alas komennolla `sudo a2dissite 000-default` ja käynnistin Apachen uudelleen komennolla `sudo systemctl reload apache2`. Komento `curl localhost` näytti, että uusi luomani sivu oli nyt oletuksena localhostissa (ks. ensimmäinen kuva alla). Testasin sitten nettiselaimella päästä virtuaalipalvelimeni IP-osoitteeseen, mutta sain vastaani vain valkoisen sivun lyhyen tekstin sijasta. Ensimmäinen arvaukseni ongelmaan oli, että olin tehnyt typon jossakin, ja näinhän oli asian laita, kun katsoin edellä tulostamaani `curl localhost` tulostetta tarkemmin (/title muuttunutkin /head:ksi). Tämän nopea korjaus ja nyt sain sivun näkymään nettiselaimellakin (ks. jälkimmäinen kuva alla). Testasin myös sivun toimimisen toisella koneella, eikä ongelmia esiintynyt.

![Oletus alas](https://github.com/user-attachments/assets/74edac43-a1ef-43a4-9f17-70c8d76c923e)

![Typot korjattu](https://github.com/user-attachments/assets/f77a8375-86df-4a8b-8437-9f06b0dbfd6f)


## Lähdeluettelo

Computing and Educational Technology Services. How do I use chmod to change permissions? Luettavissa: https://cets.seas.upenn.edu/answers/chmod.html. Luettu: 15.9.2024.

GitHub 2024: GitHub Education. Luettavissa: https://github.com/education. Luettu: 15.9.2024.

Karvinen, T. 19.9.2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Luettu: 13.9.2024.

Karvinen, T. 20.8.2024. Linux Palvelimet 2024 alkusyksy. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 15.9.2024.

LeeviRaussi 9.9.2024. h3 Hello Web Server. Luettavissa: https://github.com/LeeviRaussi/linux-palvelimet/blob/main/h3_Hello_Web_Server.md. Luettu: 15.9.2024.

Susanna 14.2.2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/. Luettu: 13.9.2024.
