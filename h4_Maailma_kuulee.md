# h3 Maailma kuulee

> ## Tiivistelmä
>
> Raportin kuvaus

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

## Lähdeluettelo

Karvinen, T. 19.9.2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Luettu: 13.9.2024.

Susanna 14.2.2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/. Luettu: 13.9.2024.
