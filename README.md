# h6_Kulkurin-Projekti

### Työympäristö

Työympäristön host-koneena: Microsoft Windows 11 Home-käyttöjärjestelmä (versio 10.0.22621).
Lisäksi käytössä on ollut myös Virtual Box (Versio 6.1), jota hyödynnetään tehtävissä.

Kurssikuvaus ja tarkemmat tehtävänannot löytyvät [täältä](https://terokarvinen.com/2022/palvelinten-hallinta-2022p2/). 
Tehtävät on tehty joulukuussa 2022 ja tehtävän tekemisessä on hyödynnetty luennolla tehtyjä muistiinpanoja sekä muita lähteitä, jotka on merkitty loppuun. 
Luennon piti Tero Karvinen (1.12.2022) ja se oli kurssin kuudes luento, jonka aiheena oli "Pakettivarastot". Luennolla käytiin läpi Vagrant:ia sekä Salt herra-orja -arkkitehtuuria kahden virtuaalikoneen välillä.
Tehtävät on kirjoitettu Windows-koneelle ladattuun Git:iin (versio: 2.38.1.windows.1). 

### TEHTÄVÄT

## x) Lue ja tiivistä (muutamalla ranskalaisella viivalla per artikkeli, poimi esim itsellesi keskeisimmät komennot)

**- Karvinen 2017: Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds (Suosittelen käyttämään tässä koneena 'vagrant init debian/bullseye64')**

Artikkelissa kerrotaan, kuinka Vagrantin avulla virtuaalikoneen luominen tapahtuu jopa 31 sekunnissa. Arkitteli sisältää komennot uuden vkoneen luomiseen sekä ssh yhteyden muodostamiseen.

    vagrant init <boxin tiedoston nimi>
    vagrant up
    vagrant ssh

Luodun virtuaalikoneen tuhoaminen käy yhtä näppärästi komennolla `vagrant destroy`.

**- Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant**

Artikkelissa kerrotaan, kuinka useiden virtuaalikoneiden luominen onnistuu yhdellä kertaa. 
Esimerkissä ohjeistetaan kahden koneen luomiseen Vagrantfile- nimisen tiedoston avulla.
Sieltä löytyy myös Vagrantfilen-sisältö esimerkki, jonka avulla saa luotua tiedoston oikein.
Kun virtuaalikoneet on ylhäällä, artikkeli ohjeistaa myös ssh-yhteyden luomisessa sekä yhteyden toimimisen tarkistamisessa. Lopussa on myös Destroy-ohjeet luoduille virtuaalikoneille.


**- Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux**

Artikkeli ohjeistaa Salt masterin ja Salt minionin luomisessa, joka on hyödyllistä, kun luodaan virtuaalikoneita, joissa halutaan opetella käyttämään Salt:tia herra-orja -arkkitehtuurissa.

Artikkelissa käydään step-by-step tyylisesti läpi, kuinka Saltin asennuksessa edetään: master, minion, salt-keys, testi. Lopussa kerrataan muutamia komentoja, joita voi testata orjilla ja tarkistaa, toimiiko luotu arkkitehti oikein omassa virtuaaliympäristössä.


## a) Hello Vagrant. Asenna virtuaalikone Vagrantilla.

Vagrant on ohjelma, jolla pystyy luomaan useita virtuaalikoneita heposti ja nopeasti.
Se on avoimen lähdekoodin ohjelmisto virtualisoitujen kehitysympäristöjen luomiseen ja hallintaan.
Vagrant tukee VirtualBoxia, joka toimii puolestaan Hypervisorina luodessaan virtuaalikoneita.
Lisäksi se tukee Windows-, Linux, sekä MacOS-pohjaisia käyttöjärjestelmiä. (Hashicorp 2022.)

Vagrantin käyttämiseen tarvitaan siis Vagrant sekä Hypervisor - kuten VirtualBox.
Vagrant kannattaa asentaa omalle host-koneelle, jonka kautta hallinnoi muita virtuaalikoneita.
Koska oman host-koneeni käyttöjärjestelmä on Microsoft Windows 11 Home, asensin Vagrantin sille käyttikselle. (Karvinen 2022.)

### Vagrantin asennus

Ladataan sopiva Vagrant-tiedosto. 
Itse latasin version nimeltä: AMD64 (Versio 2.3.3). 
Tiedosto löytyi [täältä](https://developer.hashicorp.com/vagrant/downloads).

Tämän jälkeen avasin Powershellin "run as a administrator" ja avasin ladatun tiedoston downloads-kansiosta.

    cd C:/Users/sanni/Downloads>
    ./vagrant_2.3.3_windows_amd64.msi

<img width="372" alt="1" src="https://user-images.githubusercontent.com/117899949/205603922-dc1a52a4-6796-4e10-9dd3-71dc540efa10.png">

Suoritin Vagrantin asennuksen, jonka jälkeen pystyttiin aloittamaan Vagrantin käyttö.

### Virtuaalikoneen asennus Vagrantilla

Vagrantissa idea on ns. napata boxeja. Boxit ovat ns. VMimageja, joita voi kloonata omaan virtuaaliympäristöönsä.
Erilaisia boxeja löytyy mm. [täältä](https://app.vagrantup.com/boxes/search)
Tässä esimerkissä aiomme käyttää "debian/bullseye64"-nimistä boxia, joka kloonaa Debian 11 käyttöjärjestelmällä asennetun virtuaalikoneen VirtualBoxiin.
Windowsissa Vagrant toimii PowerShellillä. (Vagrant 2022.)

Lähtötilanne VirtualBoxissa:

<img width="553" alt="lahtotilanne" src="https://user-images.githubusercontent.com/117899949/205604005-6d45e3f8-150b-4b60-9ddd-47cb252f4627.png">

Luodaan ensin tyhjä kansio ja siirrytään sinne

    mkdir vms
    cd vms

Luodaan Debian 11 varustettu virtuaalikone Vagrantilla `vagrant init <boxin nimi>`, jonka jälkeen käynnistetään virtuaalikone `vagrant up`-komennolla:

    vagrant init debian/bullseye64
    vagrant up

<img width="737" alt="2" src="https://user-images.githubusercontent.com/117899949/205603956-18bc2227-12d1-49f7-b88d-d604d8e101b1.png">

Virtuaalikone tuli todella nopeasti (taikuutta?). 
Seuraavaksi otetaan hostilla etäyhteys luomaamme koneeseen:

    vagrant ssh

Sisällä ollaan! Tehdään tällä kertaa vain nopea testaus, onnistuuko päivittäminen ja poistutaan virtuaalikoneesta.

<img width="449" alt="image" src="https://user-images.githubusercontent.com/117899949/205612214-138219d5-a029-4d4d-8a83-0933c0f1cf31.png">

    sudo apt-get update
    exit
    
Toimii! VirtualBoxissakin näyttää nyt olevan kaksi virtuaalikonetta.

<img width="560" alt="LOPPUTIlANNE" src="https://user-images.githubusercontent.com/117899949/205604040-5b713db3-8705-4056-84ac-7d64d33b8292.png">

## b) Yksityisverkko. Asenna kaksi virtuaalikonetta samaan verkkoon Vagrantilla. Laita toisen koneen nimeksi "isanta" ja toisen "renki1". Kokeile, että "renki1" saa yhteyden koneeseen "isanta" (esim. ping tai nc). Tehtävä tulee siis tehdä alusta, vaikka olisit ehtinyt kokeilla tätä tunnilla.

Tehtävään soveltuvat ohjeistukset löytyvät [täältä](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/).
Koska Vagrant asennettiin kohdassa a, voimme siirtyä suoraan tiedoston luomiseen, jossa määritellään kahden virtuaalikoneen speksit.
Kun tiedosto on valmis, voidaan ajaa tiedosto Vagrantilla `vagrant init <tiedoston nimi>` ja `vagrant up`, jotta saadaan homma käynnistymään.
Tärkeintä onkin, että tiedoston luomisessa speksit on kunnossa ja määritelty oikein, sillä teoriassa homman pitäisi olla helppoa ja nopeaa. (Karvinen 2021.)

Aloitetaan menemällä aiemmin luotuun `vms` kansioon ja luodaan sinne VagrantFile-niminen tiedosto.
Käytän itse notepadia.
Kopion Tero Karvisen luoman tiedostopohjan ja muutan nimet tehtävänannon mukaan isannaksi ja renki1:seksi.
Tiedostossa siis määritellään Vagrantille, että luodaan kaksi virtuaalikonetta.
Käyttöjärjestelmänä Debian 11 (box: Debian/bullseye64). (Karvinen 2021.)

alkutilanne:
    
<img width="560" alt="LOPPUTIlANNE" src="https://user-images.githubusercontent.com/117899949/205604079-17efcae2-6d87-4fd1-9904-6d44df8e22c5.png">

Ensin luodaan isanta-kone ja sen jälkeen renki1-kone.
Tallennetaan tiedosto ja ajetaan komennot.

<img width="890" alt="4" src="https://user-images.githubusercontent.com/117899949/205604102-01d3fea8-0859-4024-a8df-0f56f93208a2.png">

    vagrant init Vagrantfile
    
Tulee errorviesti, joka viittaa, että line 19 on jokin virhe. Avataan tiedosto uudelleen ja tarkistetaan.

<img width="389" alt="6_error" src="https://user-images.githubusercontent.com/117899949/205604145-fb2aaeea-3fe1-47c2-bcad-4c1121cc2e40.png">

Näyttää siltä, että olin muokkaillut virtuaalikoneiden nimiä hieman liian innokkaasti, ja isanta/renki1 nimet olivat lipsahtaneet liian moneen paikkaan.
Pieni fiksaus tiedostoon ja uusi yritys.

<img width="464" alt="7" src="https://user-images.githubusercontent.com/117899949/205604175-4d034a0c-990f-4e59-8bb8-9531f6be7670.png">

    vagrant init Vagrantfile
    vagrant up

Nyt toimii ja molemmat virtuaalikoneet pyörähti käyntiin

<img width="832" alt="8" src="https://user-images.githubusercontent.com/117899949/205604199-fb1fbf0b-1464-479e-9bf9-a123d27c1c54.png">

Seuraavaksi kokeillaan, että yhteys näiden kahden välillä toimii, sillä muutoin salt masterin ja minionin asennus on turhaa.
Tehtään ping-testi.

    vagrant ssh isanta
    ip addr
    exit

Kopsataan isannan ip-osoite.

    vagrant ssh renki
    ping <isannan ip-osoite>
    
<img width="382" alt="9" src="https://user-images.githubusercontent.com/117899949/205604220-c09fba43-0523-45a6-84f7-a84d5243b544.png">

Pingaus toimii, eli yhteys kahden koneen välillä toimii.

## c) Salt master-slave. Toteuta Salt master-slave -arkkitehtuuri verkon yli. Aseta edellisen kohdan kone renki1 orjaksi koneelle isanta.

Avataan ssh-yhteys Powershellillä masterille. Tämän voisi tehdä niin, että avaa virtualboxissa molemmat virtuaalikoneet, mutta laiskuus iski, ja teen koko homman PowerShellillä.

Kun ollaan sisällä isanta-koneessa, tehdään ensin päivitykset (`sudo apt-get update` jne.), jonka jälkeen asennetaan salt-master ja potkaistaan ohjelma käyntiin:

    vagrant ssh isanta
    sudo apt-get install salt-master
    sudo systemctl restart salt-master.service

Tarkistetaan, mitä portteja isanta kuuntelee. 
`4504` sekä `4506` näyttää olevan avoinna.

<img width="677" alt="10" src="https://user-images.githubusercontent.com/117899949/205604288-8e8b2b3d-0d6d-4aec-b235-60f4da700d3d.png">

    exit

Ja siirrytään renki1-koneeseen `vagrant ssh renki1`. Tehdään myös renki1 koneessa ensin päivitykset ennen Saltin-minionin asennusta.
Kurkataan kuitenkin ensin, että myös renki1-koneessa on halutut portit 4504 sekä 4506 auki.
Asennan netcatin `sudo apt-get installe netcat` ja testataan, onko renki1:sellä halutut portit auki.

    nc -nvz  192.168.88.101 4505

Tämä ok.

<img width="323" alt="11" src="https://user-images.githubusercontent.com/117899949/205604367-10e5d877-f544-42f5-b880-e71ed40bb5f7.png">

Sitten aloitetaan Salt-minionin asennus.

    sudo apt-get install salt-minion
    sudo systemctl restart salt-minion.service  

Sitten määritetään minionille isanta-ip avaamalla minion tiedosto salt-kansiosta.

    sudoedit /etc/salt/minion

<img width="462" alt="12" src="https://user-images.githubusercontent.com/117899949/205604413-ee92efd7-65e5-4bc5-b740-6cc4977835ae.png">

    exit

Tämän jälkeen siirrytään hyväksymään isannalla uudet avaimet. Siirrytään vagrantilla taas isanta-koneelle
ja kurkataan odottavat avaimet `sudo salt-key`, joka oli kohdallani tyhjä.
Pienen pään rapsuttelun jälkeen muistin, että salttia olisi pitänyt potkaista minion-dokkarin muokkauksen jälkeen, joten käyn tekemässä sen tässä välissä.
Sitten uusi yritys. 

<img width="248" alt="13" src="https://user-images.githubusercontent.com/117899949/205604438-e24f24f4-c96f-483a-ae14-ab16316fd278.png">

Nyt näyttää paremmalta. Hyväksytään avaimet:

    sudo salt-key -A

Sitten on vuorossa vielä testi. Kokeillaan, jutteleeko renki isannalle, kun annetaan orjille salt-state:

    sudo salt '*' cmd.run *hostname*

Vastaus tuli: 

<img width="344" alt="14" src="https://user-images.githubusercontent.com/117899949/205604473-dd801932-322a-494a-a314-54a629db24cb.png">


### d) Oma suola projektin hahmottelu ja luominen aloitettu täällä:
https://github.com/sannnir/Project-My-own-Salt-state/blob/main/README.md

*******
    
### LÄHTEET:

Hashicorp 2022. Vagrant Luettavissa: https://github.com/hashicorp/vagrant. Luettu: 5.12.2022
    
Tero Karvinen 2017. Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds. Luettavissa: https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/. Luettu: 5.12.2022
    
Tero Karvinen 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 5.12.2022
    
Tero Karvinen 2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/. Luettu: 5.12.2022
    
Tero Karvinen 2022. Configuration Management Systems - Palvelinten Hallinta. Luettavissa: https://terokarvinen.com/2022/palvelinten-hallinta-2022p2/. Luettu: 4.12.2022
    
Vagrant 2022. Install and Specify a Box. Luettavissa: https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-boxes. Luettu: 5.12.2022
