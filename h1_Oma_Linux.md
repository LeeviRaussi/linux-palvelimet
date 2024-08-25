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

Käynnistin seuraavaksi luomani virtuaalikoneen kaksoisklikkauksella. Mitättömän pienen kokoinen ikkuna ei kelvannut itselleni, joten muutin ylhäällä olevasta View-valikosta Scaled-tilan päälle, jolloin ikkunan koon muuttaminen muutti myös näkymän kokoa (kts. kuva alla). (Jälkihuomio: tämä näkymä vaihtoehto saattaa tulla ongelmalliseksi asennuksen myöhemmässä vaiheessa.)

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

Seuraavana olleena Summaryssä kaikki näytti olevan oikein, mutta "Install"-nappi näytti puuttuvan (kts. alla oleva kuva). Tarkemmalla tarkastelulla ruudun alalaidassa näyttäisi olevan kolme nappia lähes kokonaan piilossa. Tämä johtunee käyttämästäni View-asetuksesta, joka ei selvästikään vaikuta olleen paras ratkaisu. Edellisten vaiheiden perusteella veikkasin Install-napin olevan keskimmäinen, jota painoin toiveikkaana. Ilokseni asennusprosessi lähti käyntiin.

## Lähdeluettelo

Debian 6.8.2024. Download Debian. Luettavissa: https://www.debian.org/distrib/. Luettu: 25.8.2024.

Free Software Foundation, Inc. 1.1.2024. What is Free Software? Luettavissa: https://www.gnu.org/philosophy/free-sw.html. Luettu: 24.8.2024.

Haaga-Helia, 2024. Raportointiohje pitkille raporteille ja opinnäytetyölle. Luettavissa: https://www.haaga-helia.fi/sites/default/files/file/2024-08/raportointiohje-pitkille-raporteille-ja-opinnaytetoille.pdf. Luettu: 24.8.2024.

Karvinen, T. 4.6.2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/. Luettu: 24.8.2024.

Karvinen, T. 8.11.2023. Install Debian on Virtualbox - Updated 2023. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/. Luettu: 25.8.2024.

Oracle 2023. Download VirtualBox. Luettavissa: https://www.virtualbox.org/wiki/Downloads. Luettu: 25.8.2024.
