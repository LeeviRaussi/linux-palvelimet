# h6 Hello Django

> ## Tiivistelmä
>
> Raportissa asennetaan ensin Django Debian 12 pohjaiselle virtuaalikoneelle. Tämän jälkeen tällä luodaan kevyt CRM-ohjelma, joka myös valmistellaan tuotantotyyppistä käyttöä varten.

> ### Käytetty laitteisto
>
> Lenovo Ideapad Pro 5 14APH8 kannettava tietokone
> - Prosessori: AMD Ryzen 7 7840HS
> - GPU: Radeon 780M Graphics (prosessoriin integroitu)
> - RAM: 32 GB, 6400 MT/s
> - OS: Windows 11 Home 23H2
> - Näytön resoluutio: 2880x1800 (175% skaalaus)
> - SSD: 777/951 GB vapaana

## a) Yksinkertainen esimerkkiohjelma Djangolla

Tehtävässä oli tarkoitus tehdä esimerkkiohjelma Djangolla, joten ensiksi minun piti asentaa kyseinen ohjelmisto virtuaalikoneelleni. Käytin ohjeina Karvisen (13.2.2022a) artikkelia, ja päätin heti alkuun, että ensiksi tekisin kyseisen artikkelin mukaisen esimerkkiohjelman, ja vasta sitten, kun olin saanut kunnollisen käsityksen, mistä Djangossa oli kyse, katsoisin lähtisinkö rakentamaan täysin omaa ohjelmaa.

0:00 Aloitin päivittämällä saatavilla olevien ohjelmistojen tiedot komennolla `sudo apt-get update`, minkä jälkeen asensin Virtualenv-ohjelmiston komennolla `sudo apt-get -y install virtualenv`. Kyseistä ohjelmaa käytetään Python-ympäristöjen luomiseen. Asennusprosessi vei reilun minuutin.

0:01 Loin seuraavaksi uuden ympäristön kotihakemistooni komennolla `virtualenv --system-site-packages -p python3 env/`. Samainen komento myös loi uuden hakemiston, minne kyseinen ympäristö asetettiin. Otin ympäristön käyttöön komennolla `source env/bin/activate` ja tarkistin komennolla `which pip`, että olin todella tekemässä asennuksia oikeaan paikkaan (ks. kuva alla).

![virtualenv pip](https://github.com/user-attachments/assets/2052c70d-eb25-42b1-bfd2-f7e1929110cb)

0:02 Minulta löytyi jo asennettuna artikkelissa mainittu Micro-editori, joten loin suoraan vain tekstidokumentin requirements.txt, johon kirjoitin sanan "django". Tämän jälkeen käytin dokumenttia Djangon asennusprosessin käynnistämiseen, mikä tapahtui komennolla `pip install -r requirements.txt`. Asennus vei pari minuuttia, minkä jälkeen tarkistin komennolla `django-admin --version`, että asennettu versio oli uusin (ks. kuva alla). Versionumero oli sama, mikä oli esitelty keskiviikon luennolla, joten kaikki oli sujunut onnistuneesti.

![django install](https://github.com/user-attachments/assets/e6d61e75-0a40-4915-b631-f2c8c7ce4d8f)

0:05 Lähdin sitten luomaan ensimmäistä Django-projektiani. Käytin komentoa `django-admin startproject raussi.me` tarkoituksenani luoda projekti "raussi.me", mutta sainkin ilmoituksen, että nimi oli epäkelpo. Selvästikään piste ei ollut hyväksyttävä osa nimeä, sillä sen poistaminen tuotti tulosta. Siirryin sitten kyseiseen hakemistoon komennolla `cd raussime` ja pyrin käynnistämään kehityspalvelimen. Sain kuitenkin pienen varoituksen, ettei projekti välttämättä toimisi oikein ennen kuin olisin siirtänyt kasan ohjelmistoja (ks. kuva alla).

![migrate herja](https://github.com/user-attachments/assets/493499bd-c89d-4ab7-9ae6-36e39b859cf3)

Karvisen (13.2.2022a) artikkelissa tästä ei ollut minkäänlaista mainintaa [Jälkihuomio: tämä mahdollisesti käsitellään heti tämän osion jälkeen], mutta päätin noudattaa varoitusta ja suoritin komennon `python manage.py migrate`, joka käynnisti kiltisti siirtoprosessin. Lyhyen odotuksen jälkeen siirrot valmistuivat ja ajoin uudelleen komennon `./manage.py runserver` palvelimen käynnistämiseksi. Tällä kertaa en saanut varoituksia, vaan komento suoritettiin onnistuneesti (ks. ensimmäinen alla oleva kuva) ja Djangon tervetuloa-sivu avautui osoitteeseen 127.0.0.1:8000 (ks. jälkimmäinen alla oleva kuva).

![manage py runserver](https://github.com/user-attachments/assets/ed877064-30bf-4b61-a82a-ad8971d723ca)

![runserver selaimessa](https://github.com/user-attachments/assets/7b2d67e5-785b-40b7-851e-d659c8355205)

0:08 Karvisen (13.2.2022a) artikkelissa lähdetään seuraavaksi luomaan pääkäyttäjää, ja osana tätä prosessia ajetaan komennot `./manage.py makemigrations` ja `./manage.py migrate`, jotka eivät kuitenkaan vaikuttaneet tuottavan minkäänlaista tulosta (ks. kuva alla). Tämä mahdollisesti johtui siitä, että ajoin edellisessä vaiheessa jo komennon `python manage.py migrate`, joka saattoi tehdä tämän työvaiheen tehtävät. Tässä yhteydessä myös huomasin, että jotta pystyin ajamaan komentoja, minun piti aina sammuttaa kehityspalvelin. Tämä ei tuntunut erityisen käytännölliseltä, joten päädyin avaamaan toisen komentorivin, jonka siirsin myös käyttämääni ympäristöön komennolla `source env/bin/activate`. Nyt pystyin pitämään palvelinta päällä yhdellä komentorivillä, kun samalla tein muita asioita toisella.

![makemigrations tulokseton](https://github.com/user-attachments/assets/2d009008-44d7-4b1a-bc9a-d509388fc45b)

0:09 Karvisen (13.2.2022a) artikkelissa asennetaan seuraavaksi pwgen-niminen ohjelma komennolla `sudo apt-get install pwgen`, joten asensin sen ja tarkastin `man pwgen`-komennolla ohjelman manuaalista, mitä ohjelma oikeastaan tekee. Ohjelmaa käytetään salasanojen generoimiseen, joten päätin käyttää sitä generoimaan pääkäyttäjälle salasanan. Generoin salasanan komennolla `pwgen -s 20 1`, joka loi 20 merkkiä pitkän satunnaisen salasanan. Otin salasanan talteen ja lähdin luomaan pääkäyttäjää komennolla `./manage.py createsuperuser`. Jätin pääosan kohdista tyhjäksi, joten käyttäjänimekseni tuli "leevi" ja salasanaksi annoin edellä generoidun salasanan (ks. ensimmäinen alla oleva kuva). Tämän jälkeen pääsin onnistuneesti kirjautumaan Djangon pääkäyttäjän käyttöliittymään selaimen osoitteessa 127.0.0.1:8000/admin/ (ks. jälkimmäinen alla oleva kuva).

![createsuperuser](https://github.com/user-attachments/assets/48fe624e-9300-4b81-a722-a92887241905)

![admin interface](https://github.com/user-attachments/assets/20a98033-ca34-4a31-9988-8c7d2ddd56b4)

0:14 Loin seuraavaksi nettiselaimen käyttöliittymässä uuden käyttäjän "staff", jolle generoin salasanan komentorivillä edellä käytetyllä pwgen-komennolla (ks. ensimmäinen alla oleva kuva). Käyttäjän luomisen jälkeen pääsin suoraan säätämään tarkemmin käyttäjään liittyviä asetuksia, ja annoin kyseiselle käyttäjälle "Staffin" ja "Superuserin" oikeudet (ks. keskimmäinen alla oleva kuva). Kirjauduin sitten ulos pääkäyttäjältäni ja testasin staff-käyttäjän toimimista onnistuneesti (ks. viimeinen alla oleva kuva).

![staff luonti](https://github.com/user-attachments/assets/985c4df5-ac0b-49a8-8ea2-5ee7455c0623)

![staff ryhmät](https://github.com/user-attachments/assets/433a74b6-fc60-44bc-a3e3-39edbdab71a8)

![staff kirjautuminen](https://github.com/user-attachments/assets/f01b7e1a-40fa-49a8-a693-b1805cb1eb12)

0:16 Nyt pääsin viimein käsiksi varsinaiseen tehtävään, eli esimerkkiohjelman luomiseen, tässä tapauksessa CRM-ohjelmiston. Loin ensiksi komennolla `.manage.py startapp crm` crm-nimisen hakemiston ohjelmaa varten ja lisäsin tämän sitten raussimen asetuksiin komennolla `micro raussime/settings.py` (ks. kuva alla).

![settings crm](https://github.com/user-attachments/assets/6bf8dbac-6390-4570-b82d-567fe21faf99)

Loin sitten models.py-nimisen python-tiedoston komennolla `micro crm/models.py`, jonka tehtävänä on luoda asiakkaita (ks. alla oleva kuva käytetystä koodista). Tämän jälkeen ajoin komennot `./manage.py makemigrations` ja `./manage.py migrate`, jotka tällä kertaa reagoivat selvästi juuri luomaani python-tiedostoon.

![crm koodi alku](https://github.com/user-attachments/assets/61373c29-8e54-4b45-aea5-9d7f430b14b2)

Seuraavaksi muokkasin python-tiedostoa admin.py komennolla `micro crm/admin.py`, jotta Admin-oikeuden haltijat saisivat näkyviinsä äsken luodut ominaisuudet (ks. koodin sisältö alla olevassa kuvassa).

![admin koodi](https://github.com/user-attachments/assets/cd2ecd74-493a-4e85-ba95-67b6cf396e4b)

Koska pidin palvelinta päällä toisella komentorivillä, minun riitti vain päivittää sivu, ja tekemäni muutokset tulivat näkyviin. Uusien asiakkaiden luonti ja poistaminen onnistui kätevästi nettiselaimen käyttöliittymässä (ks. alla olevat kuvat).

![päivittynyt näkymä](https://github.com/user-attachments/assets/850f14bc-1dbb-4ed5-8940-1843be86a7a5)

![crm sisällä](https://github.com/user-attachments/assets/2cbc7864-51bb-4a06-985c-49c9b0096a91)

![asiakkaan poisto](https://github.com/user-attachments/assets/b716e6a2-ea93-465d-9bdc-6ed9e5009cd4)

![crm tyhjä](https://github.com/user-attachments/assets/93e2ca0b-cb77-498f-b071-5234d1303a64)

0:23 Uusia asiakkaita lisätessä nämä näkyivät hyvin epämääräisillä nimillä, kuten edellä olevista kuvista voidaan nähdä. Tehtävän lopuksi muokkasin models.py-tiedostoa komennolla `micro crm/models.py` palauttamaan sen nimen, joka käyttöliittymässä asiakkaalle oli määritelty, sekä muutin artikkelin ohjeiden mukaisesti nimen pituuden maksimiksi 160 merkkiä aiemman 300 sijasta (ks. ensimmäinen kuva alla muokatusta koodista). Tämän päivityksen jälkeen käyttöliittymässäkin nimet muuttuivat halutuiksi (ks. jälkimmäinen kuva alla).

![crm koodi update](https://github.com/user-attachments/assets/9bcc7e37-cff8-412a-9430-aa9ce377fda3)

![crm interface update](https://github.com/user-attachments/assets/3beab1a7-ade1-44cc-9bc8-ce70aedb5042)

Koska olin saanut nyt kuvan, mistä Djangossa oli kyse, päätin, etten lähde rakentamaan täysin omaa ohjelmaani, koska python-taitoni ovat hieman ruosteessa, minkä lisäksi minulla ei varsinaisesti ollut minkäänlaista ideaa, minkälaisen ohjelman tekisin. Tyydyin siis esimerkkinä olevaan ohjelmaan.

## b) Djangon tuontantotyyppinen asennus

Tehtävän tarkoituksena oli yhdistää Apache ja Django. Karvisen (13.2.2022b) artikkelissa käydään läpi kaikki mahdolliset vaiheet aina Apachen ja Djangon asennuksesta alkaen, mutta koska olen jo aiemmin tehnyt nämä asiat herää kysymys, miten näiden soveltaminen yhteen oikein tapahtuu? Karvisen (13.2.2022b) artikkelissa luodaan varta vasten kotihakemistoon hakemisto "publicwsgi", jonne sekä Apachen sivut että VirtualEnv-virtuaaliympäristö asennetaan. Kuitenkin aiemmin kurssilla Apachen nettisivuja on luotu hakemistoon "publicsites" ja edellä kohdassa a) VirtualEnv asennettiin kotihakemistoon luotuun "env"-hakemistoon. Artikkeli antaa ymmärtää, että tämän a) kohdan projektin voisi kopioida uuteen hakemistoon, mutta tämä taas jättää auki, onko todella tarkoitus asentaa aina uusi VirtualEnv-ympäristö jokaiseen hakemistoon? Koska artikkelissa hakemiston "publicwsgi" alla hakemistot "teroco" ja "env" ovat erillään toisistaan, tulkitsen tämän, ettei näiden sijainneilla ole niin suurta väliä. Lähden yrittämään tehtävän suoritusta jo olemassa olevalla nettisivupohjallani raussi.me, joka sijaitsee hakemistossa /home/leevi/publicsites/raussi.me/ sekä kohdassa a) luomallani raussime-projektilla, joka sijaitsee hakemistossa /home/leevi/env/.

0:25 Vaikka päätinkin hyödyntää jo olemassa olevia hakemistoja, päädyin luomaan Karvisen (13.2.2022b) artikkelin hengessä raussi.me-hakemistoon "static" hakemiston ja tänne tiedoston "static.html" tekstillä "Staattinen". Käynnistin Apachen uudelleen, mutta selaimessa osoite localhost/static/ antoi vain virhettä. Ensihätäilynä annoin lisää oikeuksia (mahdollisesti olen tehnyt tämän jo aiempina viikkoina, jolloin mitään muutosta ei todellisuudessa tapahtunut) eri käyttäjäryhmille koskien kotihakemistoni "publicsites"-hakemistoa, ennen kuin tajusin, etten koskaan ollut luonut conf-tiedostoa uudelle sivulle. Ajattelin ensin muokata jo olemassaolevaa raussi.me.conf-tiedostoa, mutta päädyin luomaan uuden tiedoston, jonka sisällön kopioin Karvisen (13.2.2022b) artikkelista pyrkien muokkaamaan hakemistojen polut oikeiksi. Laitoin sivun päälle käynnistäen Apachen uudelleen samalla, tarkastin asetusten toimimisen, otin vanhan raussi.me sivun alas, käynnistin Apachen uudelleen ja tarkistin asetusten toimisen (toimivat). (Alla kuva kaikista tämän vaiheen komennoista)

![raussi me static1](https://github.com/user-attachments/assets/1e694712-9b46-4b60-bddd-f373c6356fb7)

Odottaen kaiken toimivan käytin curl-komentoa saadakseni eteeni vain 403-virheen. Hetken mietittyäni, päätin muuttaa sivuston tiedoston nimen static.html:stä index.html:ään. Asetusten tarkastus ja Apachen boottaus eivät muuttaneet 403-virhettä. Sokkona löin samoja oikeuksia syvemmälle hakemistoon, vaikka näin jälkikäteen miettien tämän ei pitäisi vaikuttaa millään tapaa, koska oikeudet on annettu jo ylemmälle tasolle, eli niiden pitäisi periytyä myös alempiin hakemistoihin. (Alla kuva käytetyistä komennoista)

![raussi me static2](https://github.com/user-attachments/assets/72257a21-7c94-48e8-bba9-539c0254c4b2)

Curl ei tuottanut vieläkään oikeaa tulosta, joten päätin muuttaa komennon pelkäksi `curl http://localhost`. Suureksi hämmennykseni sain vastauksena Apachen oletussivuille muokkaamani tekstin, vaikka olin kyseisen sivun laittanut pois päältä jo aikoja sitten. Apachen boottaus ja oletussivujen conf-tiedoston toteaminen alhaalla oleviksi sai minut viimein muistamaan mahdollisesti todennäköisimmän vaihtoehdon, eli kirjoitusvirheen mahdollisuuden. Ja tästähän oli lopulta kyse, sillä kopioidessani Karvisen (13.2.2022b) artikkelista conf-tiedostoa varten pätkän, olin epähuomiossa jättänyt yhteen polkuun kotihakemistoksi "tero" omani sijasta. Virheen korjaus ja Apachen boottaus, jonka jälkeen testasin pari kertaa väärää osoitetta ennen kuin sain viimein haluamani sivun näkyviin. (Alla kuva käytetyistä komennoista)

![raussi me static3](https://github.com/user-attachments/assets/1968af15-2be8-4adb-aadf-cb7b5aad5859)

0:37 Karvisen (13.2.2022b) artikkelia lukiessa ja tarkastellessa omien hakemistojeni sijainteja päädyin siirtämään kohdassa a) luodun raussime-projektin hakemiston publicsites/raussi.me -hakemiston alle komennolla `mv raussime/ /home/leevi/publicsites/raussi.me/`. Tämän jälkeen siirryin kansiosta toiseen hakien oikeita polkuja muokatakseni raussi.me.static.conf-tiedosto python yhteensopivaksi. Pohjana käytin Karvisen (13.2.2022b) artikkelista löytyvää pohjaa, johon muokkasin sopivat hakemistopolut (ks. kuva alta).

![raussi me static conf muokattu](https://github.com/user-attachments/assets/bc88e142-5ec6-46e6-b7cd-d0d185cd1a75)

0:44 Jatkoin Karvisen (13.2.2022b) artikkelin ohjeiden seuraamista asentamalla Apachen WSGI-moduulin. Tarkastin konfiguraation toimimisen, jonka jälkeen boottasin Apachen. Nyt käyttäessäni curl-komentoa sain vastauksena tiedon, että asennus oli ollut onnistunut (ks. ensimmäinen kuva alla käytetyistä komennoista ja toinen kuva Djangosta localhost-osoitteessa).

![mod_wsgi asennus](https://github.com/user-attachments/assets/f2792da4-0cca-4805-b91e-1c0176b6e536)

![mod_wsgi localhost](https://github.com/user-attachments/assets/09377ed7-20e8-4b66-8258-4e8bd3268244)

0:47 Muokkasin seuraavaksi projektin asetuskooditiedostossa Debug-tilan pois päältä, sekä sallituiksi verkkoasemiksi localhostin ja raussi.me:n, mikäli siirtäisin sivun julkisesti nähtäville (ks. kuva alla).

![debug false](https://github.com/user-attachments/assets/18d21aa5-e23b-4e12-901b-b2c347683426)

Käytin normaalin käyttäjän oikeuksia ottamaan wsgi.py:n muutokset käyttöön (touch-komento), mutta ohjeiden mukaan myös koko Apachen käynnistäminen uudelleen olisi suositeltavaa, joten tein senkin. Nyt curl ei tuottanut mitään tuloksia, mutta sivut selvästi toimivat, koska pystyin kirjautumaan osoitteeseen localhost/admin kohdassa a) luomillani staff-käyttäjän tunnuksilla, joskin sivun ulkoasu oli rikkinäinen (ks. ensimmäinen alla oleva kuva käytetyistä komennoista ja jälkimmäinen kuva rikkinäisestä Admin-käyttöliittymästä). Huomattavaa on myös, että toisin kuin kohdassa a), nyt Django selvästi toimi Apachen kautta, koska en ollut missään vaiheessa ajanut `./manage.py runserver`-komentoa.

![micro debug](https://github.com/user-attachments/assets/d8027096-8133-4a38-8eae-cd13c1a057f2)

![rikkinäinen admin](https://github.com/user-attachments/assets/0cab074d-09d1-433d-b3c5-b17ba16fed79)

0:50 Lähdin muokkaamaan tyyliasetuksia uudelleen settings.py-tiedostoon. Tiedostossa ei ollut valmiina tuotuna os:ää tai STATIC_ROOT-objektia, joten lisäsin ne koodin alkuun (ks. ensimmäinen kuva alla). Jotain kuitenkin meni pieleen, koska kun ajoin komennon `./manage.py collectstatic` nimenomaan juuri luodun STATIC_ROOT:a määrittelevä BASE_DIR aiheutti virheen (ks. jälkimmäinen kuva alla).

![static_root väärä](https://github.com/user-attachments/assets/8171584d-92b1-436b-9acc-526664846524)

![static_root virhe](https://github.com/user-attachments/assets/3cb6e559-d3b1-433a-bb4c-5ed15b62709e)

Karvisen (13.2.2022b) artikkelissa ei ollut sen tarkemmin käsitelty asiaa, joten hetken pohdinnan jälkeen päädyin määrittelemään BASE_DIR:n kuten aiemmin olin määritellyt asioita raussi.me.static.conf-tiedostossa Definella (vaikka näin jälkikäteen ajateltuna conf- ja py-tiedostot ovat täysin eri formaattia, joten vaikka pythonia kirjoitetaankin pitkälti kuten normaalia kieltä, ei tämän olisi edes pitänyt toimia. Oikea muoto olisi BASE_DIR = ...). Ollessani juuri sulkemassa tiedostoa muokkaamisen jälkeen silmääni osui kahta riviä alempana kuin mihin olin STATIC_ROOT:n määritellyt tiedostossa ennestään ollut BASE_DIR:n määrittely. Muokkasin koodia sitten sen verran, että siirsin STATIC_ROOT:n määrittelyn BASE_DIR:n jälkeen (ks. ensimmäinen kuva alla), jonka jälkeen komento `./manage.py collectstatic` toimi ongelmitta (ks. jälkimmäinen kuva alla).

![static_root oikea](https://github.com/user-attachments/assets/8bbd3539-a60d-4b73-bb0f-80d8af681512)

![static_root komennot](https://github.com/user-attachments/assets/1bf30d41-740f-4d99-8aeb-441bbc643b30)

Nyt selaimen käyttöliittymässäkin asiat alkoivat näyttämään toimivilta (ks. kuva alla) ja sain täten tehtävän valmiiksi.

![localhost wsgi toimii](https://github.com/user-attachments/assets/c21c7652-62da-4a50-af0b-cc15703bd28a)

## Lähdeluettelo

Karvinen, T. 13.2.2022a. Django 4 Instant Customer Database Tutorial. Luettavissa: https://terokarvinen.com/2022/django-instant-crm-tutorial/. Luettu: 29.9.2024.

Karvinen, T. 13.2.2022b. Deploy Django 4 - Production Install. Luettavissa: https://terokarvinen.com/2022/deploy-django/. Luettu: 29.9.2024.
