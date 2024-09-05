# h3 Hello Web Server

> ## Tiivistelmä
>
> Raportissa ensin esitellään tiivistelminä The Apache Software Foundationin (2024) ja Karvisen (10.4.2018) artikkelit nimipohjaisten virtuaali-isäntien toiminnasta.

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

### Name-based Virtual Host Support (ASF 2024)

ASF:n (2024) artikkelissa esitellään nimipohjaisten virtuaalisten isäntäkoneiden toimintaa. Ideana tässä on, että samaa IP-osoitetta voidaan käyttää viittaamaan useampaan eri verkkosivuun. Virtuaaliselle isäntäkoneelle määritetään oma IP-osoite, mutta kaikkiin muihin sivuihin, joita palvelin sisältää, viitataan nimien mukaan. Järjestelmän toimimisen ehtona onkin, että päätelaitteet ilmoittavat hakemansa verkkosivun nimen osana HTTP-otsaketietoja, kun ne lähettävät pyyntöjä palvelimelle. Tämän tiedon avulla palvelin pystyy hakemaan oikean sivun ja lähettämään sen vastauksena. (ASF 2004.)

Nimipohjaisen järjestelmän käyttö perustuu rajalliseen Ipv4-osoitteiden määrään. Vapaina olevien osoitteiden määrän tyrehtyessä, mutta uusien verkkosivujen määrän jatkaessa kasvua, on nimipohjainen järjestelmän käyttö käytännössä pakollista jollei laitteisto itsessään vaadi IP-pohjaista virtualisointia. Kuitenkin on hyvä huomata, että lähtökohtaisesti IP-pohjainen nimiresoluutio toimii myös nimipohjaisen järjestelmän perustana. Jos virtuaali-isännän IP-osoitteet on määritelty huonosti DNS-palvelimelle, systeemi ei tule toimimaan, vaikka järjestelmä olisi nimetty muuten täydellisesti. Tämä johtuu siitä, että virtuaali-isännän hallinnoimista sivuista valitaan HTTP-otsakkeessa olevaa nimitietoa sopivin vasta sitten, kun sopivin IP-osoite ja porttinumero on tavoitettu. Tämän jälkeen, erityisesti Apachen tapauksessa, jos useampi verkkosivu vastaa samaa IP-osoitetta, virtuaali-isäntä lähtee tarkastelemaan pyynnön palvelinnimeä sekä mahdollisia aliaksia. (ASF 2024.)

### Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address (Karvinen 10.4.2018)

Karvinen (10.4.2018) esittelee artikkelissaan lyhyesti, miten Apache otetaan käyttöön ja kuinka sitä voi hyödyntää ohjaamaan verkkoliikennettä yhden IP-osoitteen kautta useisiin eri kohteisiin. Prosessi käynnistyy asentamalla Apache Linuxiin komennolla `sudo apt-get -y install apache2`. Tämän jälkeen Karvinen muokkaa localhostissa olevaa oletussivua komennolla `echo "Default"|sudo [käyttäjä] /var/www/html/index.html`. (10.4.2018.) Seuraavaksi Karvinen (10.4.2018) luo uuden nimipohjaisen virtuaali-isännän komennolla `sudoedit /etc/apache2/sites-available/pyora.example.com.conf`, minkä jälkeen hän laittaa kyseisen sivun päälle (Fritsch 8.6.2007) komennolla `sudo a2ensite pyora.example.com` ja käynnistämällä Apachen uudelleen komennolla `sudo systemctl restart apache2` tuo tehdyt muutokset luettaviksi (Karvinen 10.4.2018). Tämän jälkeen normaalikäyttäjä pystyy muokkaamaan ja luomaan uusia verkkosivuja esimerkiksi komennoilla `mkdir -p /home/xubuntu/publicsites/pyora.example.com/` ja `echo pyora > /home/xubuntu/publicsites/pyora.example.com/index.html`. Lopuksi on aina hyvä testata, että tehdyt muutokset toimivat, mikä tapahtuu esimerkiksi komennoilla `curl -H 'Host: pyora.example.com' localhost` ja `curl localhost`. (Karvinen 10.4.2018.)

## Lähdeluettelo

Fritsch, S. 8.6.2007. Ubuntu Manpage: a2ensite, a2dissite - enable or disable an apache2 site / virtual host. Luettavissa: https://manpages.ubuntu.com/manpages/focal/en/man8/a2ensite.8.html. Luettu: 5.9.2024.

Karvinen, T. 10.4.2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Luettu: 5.9.2024.

The Apache Software Foundation 2024. Name-based Virtual Host Support. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html. Luettu: 5.9.2024.
