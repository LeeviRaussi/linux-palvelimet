# h1 Oma Linux

> ## Tiivistelmä
>
> Raportissa tiivistetään ensin Karvisen (4.6.2006) artikkeli raportin kirjoittamisesta sekä Free Software Foundationin määritelmä vapaasta ohjelmistosta (free software)

## x) Artikkelitiivistelmät

### Raportin kirjoittaminen tiivistelmä

Karvinen (4.6.2006) keskittyy artikkelissaan esittelemään tietokoneen testaamiseen tarkoitettua raportointityyliä. Lähtökohtaisesti raportointityyli muistuttaa esimerkiksi Haaga-Helian raportointityyliä (kts. esim. pitkän raportin ohje Haaga-Helia 2024), mutta siinä missä Haaga-Helian (2024) ohjeissa annetaan suhteellisen paljonkin painoarvoa ulkoasulle, Karvisen ohjeet keskittyvät käytännön kirjoittamiseen. Keskeiseksi asiaksi näistä ohjeista nousee vaatimus siitä, että lukijan täytyy pystyä toistamaan raportin tekijän toimet. Tämä tapahtuu raportoimalla tarkasti, millä laitteistolla kirjoittaja on testinsä tehnyt, mitä kaikkia välivaiheita kirjoittaja on tehnyt, ja milloin jokainen välivaihe on tehty. Raportointiin kuuluu kertoa myös mahdollisista ongelmista ja miten ne ratkaistiin, sillä lukijan tulisi kohdata samat ongelmat raportin ollessa täsmällisesti kirjoitettu. Lopuksi Karvinen muistuttaa vielä hyvän akateemisen kirjoittamisen tapojen noudattamista, eli kirjoitusasu on selvä ja teksti on asianmukaisesti lähdeviitoitettu. (Karvinen 4.6.2006.)

### Vapaan ohjelmiston määritelmä

Free Software Foundation (FSF) määrittelee vapaaksi ohjelmistoksi (free software) ohjelmiston, joka kunnioittaa käyttäjän oikeuksia esimerkiksi muokata ja julkaista sitä vapaasti (FSF 1.1.2024). Aatteen ideologia pohjautuu eritoten rakennuspilareina oleviin neljään vapauteen:

> 1. Käyttäjällä on vapaus käyttää ohjelmaa millä tahansa haluamallaan tavalla (vapaus 0)
> 2. Käyttäjällä on vapaus tutkia ohjelmiston lähdekoodia ja muokata sitä vapaasti sopimaan hänen omiin tarkoituksiinsa (vapaus 1)
> 3. Käyttäjä saa vapaasti jakaa alkuperäistä ohjelmaa muille käyttäjille (vapaus 2)
> 4. Käyttäjä saa vapaasti jakaa muokkaamaansa ohjelmistoa muille käyttäjille (vapaus 3)
> 
> (FSF 1.1.2024)

Vapaan ohjelmiston idea on siis siinä, että kuka tahansa voi käyttää ohjelmistoa oman mielensä mukaisesti ja tarvittaessa muokata sitä sopimaan omiin tarpeisiinsa. FSF (1.1.2024) myös huomauttaa, että vapaa ohjelmisto ei tarkoita sitä, etteikö ohjelmistoa voisi käyttää kaupallisesti tai myydä eteenpäin, joskin ohjelmiston tulisi edelleen noudattaa neljää vapautta, jotta se pysyisi vapaana ohjelmistona. Mikäli ohjelmisto ei nooudata jotain neljästä vapaudesta, sitä pidetään ei-vapaana riippumatta missä määrin tai muodossa vapauksien rikkominen tapahtuu (FSF 1.1.2024).

## Linuxin asentaminen virtuaalikoneeseen

> ### Käytetty laitteisto
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)

### Tarvittavat tiedostot

Aloitin asennusprosessin Karvisen (8.11.2023) ohjeiden mukaisesti lataamalla koneelleni ISO-tiedoston Debian 12.6.0 Live Xfce -versiosta (kts. Debian 6.8.2024). Noin 3 gigan tiedosto latautui suoraan sivuston linkistä, eikä minun tarvinnut käyttää mirroreita. Tämän jälkeen latasin Windows-version VirtualBox 7.0.20:sta (kts. Oracle 2023). Noin 100 megan tiedosto latautui alle 15 sekunnissa.

### VirtualBox asennus

Yllä ladattu VirtualBoxin exe-tiedosto käynnisti kaksoisklikkauksella Wizard-asennusprosessin, jolle annoin valtuudet muokata tietokoneeni sisältöä. Asennuspaikaksi jätin oletusasetukset voimaan (kts. alla oleva kuva). Sain tämän jälkeen varoituksen, että VirtualBox katkaisee asennuksessa hetkeksi koneen internet-yhteyden. Lisäksi asennus vaati, että koneella tulisi ennestään olla asennettuna "Python Core Package" ja "win32api bindings", joiden asennukseen myönnyin. Poistin oletuksena olleet asetukset työpöydän ja Quick Launch Barin pikakuvakkeiden luonnista, sillä itselleni riittää Start menusta löytyvä ohjelmiston käynnistäjä. Tämän jälkeen ohjelmisto asentui noin parissa kymmenessä sekunnissa koneelleni.

![VirtualBox asennus](https://github.com/user-attachments/assets/094a7708-9d7a-43d5-85a1-0ba2108398ba)

### Virtuaalikoneen luominen

Palasin sitten Karvisen (8.11.2023) ohjeiden pariin ja käynnistin VirtualBoxissa uuden virtuaalikoneen asentamisprosessin. Ohjeiden mukaisesti otin käyttööni "Expert Moden" sekä ohitin "Unattended Installin". Ohjeista poiketen myös annoin virtuaalikoneelle käyttöön 8 gigaa muistia, koska en odota tämän vaikuttavan negatiivisesti tietokoneen käyttöön. Alta löytyvät vielä kuvat jokaisesta luontiprosessin vaiheesta ja käytetyistä asetuksista. Ensimmäisessä kuvassa näkyy mahdollisuus ISO-tiedoston syöttämiseen, mutta jätin tämän tekemättä, koska tämä on jätetty ohjeissa asennusprosessin seuraavaan vaiheeseen.

![Expert](https://github.com/user-attachments/assets/41087292-f9b4-434e-b9ab-c02e15677905)

![Virtuaali RAM](https://github.com/user-attachments/assets/1ff8ac94-42f2-4050-a3bd-415a6e7be8ea)

![Virtuaali HDD](https://github.com/user-attachments/assets/3d30bbba-9cf2-4cbe-86e2-260321a7a17c)

Virtuaalikoneen luonnin jälkeen siirryin lisäämään asetuksista yllä ladatun Debianin ISO-tiedoston virtuaaliseen CD-asemaan (kts. kuva alla).

![CD-asema](https://github.com/user-attachments/assets/75f590ff-6f5c-4caf-965f-67ab9d6e657d)

### Debian asennus

Käynnistin seuraavaksi luomani virtuaalikoneen kaksoisklikkauksella. Mitättömän pienen kokoinen ikkuna ei kelvannut itselleni, joten muutin ylhäällä olevasta View-valikosta Scaled-tilan päälle, jolloin ikkunan koon muuttaminen muutti myös näkymän kokoa (kts. kuva alla). (Jälkihuomio: tämä näkymä vaihtoehto saattaa tulla ongelmalliseksi asennuksen myöhemmässä vaiheessa. Palaaminen Windowed modeen oletus asetuksilla Oikea CTRL + C.)

![Live Debian](https://github.com/user-attachments/assets/c2cb33fb-8a5b-4e2f-9642-b6338985cd3f)

Käynnistysprosessi ei tuntunut sujuvan täysin ongelmitta, sillä sain ilmoituksen, ettei virtuaalikone reagoi hiireeni. Lisäksi käynnistysruutu meni noin minuutiksi kokonaan mustaksi, minä aikana ajattelin koko prosessin aloittamista uudelleen. Ennen kuin kuitenkin ehdin tehdä tätä ohjeiden näköinen aloitusruutu avautui viimein ja koneen hiirikin toimi ongelmitta (kts. kuva alla).

![Live start](https://github.com/user-attachments/assets/3137264f-1a05-4570-bd16-130add5a527a)

Virtuaalikoneen toimimiseksi testasin verkkoselaimen avaamista. Selain avautui hyvin hitaasti, mutta avautui kuitenkin, minkä jälkeen pääsin onnistuneesti siirtymään osoitteeseen terokarvinen.com (kts. kuva alla). Suljin tämän jälkeen selaimen.

![terokarvinen](https://github.com/user-attachments/assets/f2e154ed-a6d6-4081-9976-485e512ed4fd)

Käynnistin sitten virtuaalisella työpöydällä olleen "Install Debian" -ohjelman käyttöjärjestelmän asentamiseksi. Sain kysymyksen, luotanko kyseiseen tiedostoon (kts. kuva alla). Valitsin "Launch Anyway" ja asennus ohjelmisto lähti käyntiin.

![Trust](https://github.com/user-attachments/assets/6deb8fd0-98d8-42f0-b857-ee23852de31e)

Järjestelmäkieleksi valitsin American English ja sijainniksini Helsingin (Suomi). Näppäimistöksi otin suomen Default-version, jolla kirjoittaminen toimi (kts. kuva alla).

![Keyboard](https://github.com/user-attachments/assets/ca45479b-f7f8-4e2e-9d7f-93d0686a0e50)

Alustin virtuaalisen kovalevyn täysin, mutten salakirjoittanut sen sisältöä. Ohjeiden mukaisesti valitsin myös "Master Boot Record...":n boot loaderin sijainniksi (kts. kuva alla).

![HDD ositus](https://github.com/user-attachments/assets/175ecda9-fcdf-4adf-8966-544e6b8be1be)

Sudo-käyttäjän tiedot löytyvät alla olevasta kuvasta.

![User](https://github.com/user-attachments/assets/c5a5b7cb-fa00-4810-a404-74fa60b1ab2d)

Seuraavana olleena Summaryssä kaikki näytti olevan oikein, mutta "Install"-nappi näytti puuttuvan (kts. alla oleva kuva). Tarkemmalla tarkastelulla ruudun alalaidassa näyttäisi olevan kolme nappia lähes kokonaan piilossa. Tämä johtunee käyttämästäni View-asetuksesta, joka ei selvästikään vaikuta olleen paras ratkaisu. Edellisten vaiheiden perusteella veikkasin Install-napin olevan keskimmäinen, jota painoin toiveikkaana (kts. kuva alla). 

![Piilossa](https://github.com/user-attachments/assets/d59887c2-ebaf-442f-91d6-e07cce92664a)

Ilokseni asennusprosessi lähti käyntiin. Reilun viiden minuutin jälkeen asennus valmistui ja jouduin jälleen arpomaan alhaalla olevien näkymättömien nappien kanssa. Klikkasin oikealla olevaa, sillä keskellä ollut ei tuntunut reagoivan painalluksiini. Hetken odottelun jälkeen Login-ruutu avautui eteeni (kts. alla oleva kuva). Kirjautuminen edellä luomallani käyttäjällä onnistui nopeasti ja pääsin työpöytänäkymään.

![login](https://github.com/user-attachments/assets/4ee2f2b2-77a7-4181-bc96-fd16f56b6ddc)

### Näkymän muuttaminen

Saatuani asennuksen onnistuneesti maaliin, päätin sulkea ja käynnistää uudelleen virtuaalikoneen, jotta saisin muokattua käyttämääni ruutunäkymää paremmaksi. Alla oleva kuva ilmoitti käynnistyksen yhteydessä siirtymisestä jälleen Scale modeen, mutta tällä kertaa ymmärsin katsoa komennon, jolla Windowed modeen palataan.

![Scale mode](https://github.com/user-attachments/assets/62083311-f67a-4475-99a8-ee4fb92f15e4)

Päästyäni takaisin tähän tilaan hetken kokeilun jälkeen päädyin valitsemaan Viewin Virtual Screen 1:stä 250 % skaalauksen, minkä lisäksi venytin virtuaalikoneen ruudun kokoa hieman, jotta näkymän ympärille syntyi ohut harmaa reuna (kts. kuva alla).

![Virtual screen](https://github.com/user-attachments/assets/e9f59451-fe95-4cd6-bcc9-af5e1a0abb55)

### Linuxin asetusten säätäminen

Saatuani näkymän toimimaan tällä kertaa toivottavasti täysin oikein, palasin Karvisen (8.11.2023) ohjeisiin. Kirjautumisen jälkeen testasin verkon toimintaa selaimella, joka aukesi huomattavasti rivakammin kuin edellisellä kerralla. Avasin sitten Applications-valikosta Terminal Emulatorin ja lähdin päivittämään tietoja siitä, mitä koneella voisi päivittää käyttäen komentoa

    sudo apt-get update

minkä jälkeen annoin käyttäjäni salasanan. Perään päivitin kaiken päivitettävissä olevan komennolla

    sudo apt-get -y dist-upgrade

Kyseinen prosessi lähti käyntiin ilman salasanan syöttämistä (kts. alla kuva keskeneräisestä prosessista). Prosessi vei suhteellisen pitkään (arviolta päälle 10 minuuttia) ja Linux ilmeisesti meni välissä horrostilaan, minkä jälkeen jouduin kirjautumaan uudelleen sisälle. Päivitysprosessi jatkui kuitenkin suoraan kirjautumisen jälkeen ja valmistui noin minuuttia myöhemmin. Varmuuden vuoksi ajoin päivityskomennon uudelleen, mutta kaikki päivitettävissä olevat asiat oli tullut päivitettyä onnistuneesti jo ensimmäisellä kerralla huolimatta uloskirjautumisesta (kts. jälkimmäinen alla oleva kuva).

![Paivitysprosessi](https://github.com/user-attachments/assets/d3c938cd-93de-46aa-a598-f3c4202128de)

![dist-upgrade uudelleen](https://github.com/user-attachments/assets/de574cce-dfe7-445e-8942-d201595bfe70)

Seuraavaksi asensin palomuurin komennolla

    sudo apt-get -y install ufw

ja otin palomuurin heti perään käyttöön komennolla (kts. kuva lopputuloksesta alla koodikomennon jälkeen)

    sudo ufw enable

![Palomuuri](https://github.com/user-attachments/assets/15923b87-f411-4bde-a9ff-93dfa069ae0e)

Käynnistin tämän jälkeen virtuaalikoneen uudelleen vasemman ylälaidan Applications-valikon Log out:sta valitsemalla Restartin. Tässä kohtaa virtuaalikone vaihtoi jälleen käyttämänsä ikkunan resoluutiota (aiemmin automaattinen Resize 800x600, näkyvillä yllä olevassa Virtual Screen 1 kuvassa) automaattisesti muuttamattomaan "Resize 1280x800" kokoon, jonka päädyin tällä kertaa skaalaamaan 175 % kokoon.

### VirtualBoxin Guest Additionsit

Karvisen (8.11.2023) ohjeiden lopuksi on vapaaehtoisena toimena VirtualBoxin Guest Additions lisäosien asennus, jonka tein vielä, koska toivoin tätä kautta löytäväni ratkaisun resoluutio-ongelmiini (minkä lisäksi leikkaa-liimaa fyysisen ja virtuaalisen tietokoneiden välillä on myös hyödyllinen ominaisuus). Virtuaalikoneen ollessa päällä valitsin virtuaalikoneen ikkunan Devices välilehdestä "Insert Guest Additions CD Image..." (kts. kuva alla).

![Devices](https://github.com/user-attachments/assets/a2a7d5ec-6bbe-4132-9af0-6bf9402abc7a)

Tämä loi virtuaalikoneeseen CD-levyn, johon pääsin käsiksi Applicationsin File Managerin Devices välilehdeltä (kts. kuva alla).

![File Manager](https://github.com/user-attachments/assets/8d8d8ad7-3f25-4f63-b1e3-cdad4cd96a8f)

Avasin sitten Applicationsista Terminal Emulatorin ja ajoin kolme koodia alla olevan kuvan mukaisesti. Ensimmäisenä oleva cd-komento siirtää tarkasteltavan sijainnin CD-levylle. Toisena oleva ls-komento näyttää levyn sisällön. Viimeisenä oleva sudo-komento suorittaa perässä olevan skriptin, joka tässä tapauksessa suorittaa asennuksen.

![Guest-asennus](https://github.com/user-attachments/assets/af359360-ed0d-4f46-8ad3-54e42d93e146)

Tämän jälkeen valitsin Applicationsin kautta Log out ja Restart virtuaalikoneen käynnistämiseksi uudelleen, jotta äsken tehty asennus tulisi päätökseen. Huomasinkin heti, että nyt muuttaessani VirtualBoxin ikkunan kokoa myös näkymä skaalautui ikkunan koon mukaisesti oikein (hieman nykien), eli pääsin haluamaani lopputulokseen. Myös fyysisen ja virtuaalisen koneiden välinen leikkaa-liimaa toimii nyt, kun VirtualBoxin ikkunan Devices-välilehden Shared Clipboard kohdasta valitaan Bidirectional (kts. kuva alla).

![Jaettu copypaste](https://github.com/user-attachments/assets/83162f4b-de47-486c-9b91-bd34b807e1df)

## k) Linuxin suosikkiohjelma?

En ole käyttänyt liiemmin Linuxia aiemmin, mutta asia, josta pidän, on komentorivin käyttäminen. Erityisesti Linuxin asentamisessakin esiintullut useamman asian asentaminen ja päivittäminen yhdellä komennolla on mielestäni erinomainen ominaisuus tehokäyttäjälle. Normaalissa arkikäytössä komentoriviä ei välttämättä halua käyttää graafisen käyttöliittymän sijasta, mutta erityisesti useampaa laitetta hallinnoidessa ymmärrän hyvin, minkä takia komentorivin käyttäminen on mielekkäämpää kuin graafisen käyttöliittymän käyttö.

## Lähdeluettelo

Debian 6.8.2024. Download Debian. Luettavissa: https://www.debian.org/distrib/. Luettu: 25.8.2024.

Free Software Foundation, Inc. 1.1.2024. What is Free Software? Luettavissa: https://www.gnu.org/philosophy/free-sw.html. Luettu: 24.8.2024.

Haaga-Helia, 2024. Raportointiohje pitkille raporteille ja opinnäytetyölle. Luettavissa: https://www.haaga-helia.fi/sites/default/files/file/2024-08/raportointiohje-pitkille-raporteille-ja-opinnaytetoille.pdf. Luettu: 24.8.2024.

Karvinen, T. 4.6.2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/. Luettu: 24.8.2024.

Karvinen, T. 8.11.2023. Install Debian on Virtualbox - Updated 2023. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/. Luettu: 25.8.2024.

Oracle 2023. Download VirtualBox. Luettavissa: https://www.virtualbox.org/wiki/Downloads. Luettu: 25.8.2024.
