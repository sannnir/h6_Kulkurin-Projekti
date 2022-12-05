# h6_Kulkurin-Projekti

## x) Lue ja tiivistä (muutamalla ranskalaisella viivalla per artikkeli, poimi esim itsellesi keskeisimmät komennot)

- Karvinen 2017: Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds (Suosittelen käyttämään tässä koneena 'vagrant init debian/bullseye64')
- Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant
- Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

## a) Hello Vagrant. Asenna virtuaalikone Vagrantilla.

Vagrant on ohjelma, jolla pystyy luomaan useita virtuaalikoneita heposti ja nopeasti.
Se on avoimen lähdekoodin ohjelmisto virtualisoitujen kehitysympäristöjen luomiseen ja hallintaan.
Vagrant tukee VirtualBoxia, joka toimii puolestaan Hypervisorina luodessaan virtuaalikoneita.
Lisäksi se tukee Windows-, Linux, sekä MacOS-pohjaisia käyttöjärjestelmiä.

Vagrantin käyttämiseen tarvitaan siis Vagrant sekä Hypervisor - kuten VirtualBox.
Vagrant kannattaa asentaa omalle host-koneelle, jonka kautta hallinnoi muita virtuaalikoneita.
Koska oman host-koneeni käyttöjärjestelmä on Microsoft Windows 11 Home, asensin Vagrantin sille käyttikselle.

### Vagrantin asennus

Ladataan sopiva Vagrant-tiedosto. 
Ise latasin version nimeltä: AMD64 (Versio 2.3.3)
Tiedosto löytyi [täältä](https://developer.hashicorp.com/vagrant/downloads)

Tämän jälkeen avasin Powershellin "run as a administrator" ja avasin ladatun tiedoston downloads-kansiosta.

    cd C:/Users/sanni/Downloads>
    ./vagrant_2.3.3_windows_amd64.msi

KUVA 1

Suoritin Vagrantin asennuksen, jonka jälkeen pystyttiin aloittamaan Vagrantin käyttö.

### Virtuaalikoneen asennus Vagrantilla

Vagrantissa idea on ns. napata boxeja. Boxit ovat ns. VMimageja, joita voi kloonata omaan virtuaaliympäristöönsä.
Erilaisia boxeja löytyy mm. [täältä](https://app.vagrantup.com/boxes/search)
Tässä esimerkissä aiomme käyttää "debian/bullseye64"-nimistä boxia, joka kloonaa Debian 11 käyttöjärjestelmällä asennetun virtuaalikoneen VirtualBoxiin.
Windowsissa Vagrant toimii PowerShellillä.

Lähtötilanne VirtualBoxissa:
LÄHTOTILANNE KUVA

Luodaan ensin tyhjä kansio ja siirrytään sinne

    mkdir vms
    cd vms

Ajetaan Debian Vagrantilla "vagrant init <boxin nimi>, jonka jälkeen käynnistetään virtuaalikoneen luominen:

    vagrant init debian/bullseye64
    vagrant up

KUVA 2

Virtuaalikone on melko nopeasti valmis, jonka jälkeen voidaan ottaa hostilla etäyhteys luomaamme koneeseen:

    vagrant ssh

Sisällä ollaan! Tehdään tällä kertaa vain nopea testaus, onnistuuko päivittäminen ja poistutaan virtuaalikoneesta.

    sudo apt-get update
    exit

Toimii! VirtualBoxissakin näyttää nyt olevan kaksi virtuaalikonetta.

LOPPUTILANNE KUVA


## b) Yksityisverkko. Asenna kaksi virtuaalikonetta samaan verkkoon Vagrantilla. Laita toisen koneen nimeksi "isanta" ja toisen "renki1". Kokeile, että "renki1" saa yhteyden koneeseen "isanta" (esim. ping tai nc). Tehtävä tulee siis tehdä alusta, vaikka olisit ehtinyt kokeilla tätä tunnilla.

## c) Salt master-slave. Toteuta Salt master-slave -arkkitehtuuri verkon yli. Aseta edellisen kohdan kone renki1 orjaksi koneelle isanta.

## d) Oma suola. Tee ensimmäinen työversio projektistasi. Miniprojektilla tulee olla jokin tarkoitus, vaikka se olisi keksitty. Projektilla tulee olla sivu (esim. Github, Gitlab...), josta selviää projektin perustiedot. Toiminnallisuutta tulee olla kokeiltu, mutta sen ei tarvitse olla valmis. Valmiit projektit esitellään viimeisellä tapaamiskerralla. Tässä tehtävässä palautettava työversio ei siis ole vielä lopullinen.
