# Tiedostot jar:n sisälle

**Huom! Jos kyseessä on tiedosto jota tulee pystyä muokkaamaan (esim. highscore-lista), ei sitä pakata jar:n sisään koska jar:n sisällä olevia tiedostoja ei voi muokata. Tälläisissä tapauksissa oikea tapa on käyttää Fileä tjsp**

Staattisten tiedostojen tai kuvien, jotka haluat pakata projektiisi mukaan lataamiseen ei voi käyttää File-luokkaa, koska kun projekti pakataan JAR-pakettiin, ei File-luokan avulla pysty lukemaan paketin sisältä. Yleensä projekteissa on myös ongelmana tiedostopolut: tiedostot ehkä löytyvät kotikoneella, mutta muiden koneella ei.

Kaikki resurssitiedostot tulisi sijoittaa ``<projektikansio>/src/main/resources/`` -kansioon. Resources-kansion sisällä saa toki myös tiedostoja jakaa kansioihin, mutta tämä tulee huomioida tiedostoa ladatessa.

Tiedosto ladataan resources-kansiosta seuraavasti:

``InputStream is = getClass().getClassLoader().getResourceAsStream("tiedosto.txt");``

Tämä hakisi tiedoston polusta ``<projektikansio>/src/main/resources/tiedosto.txt`` InputStreamiksi jota pystyy lukemaan esimerkiksi Scannerilla:

``Scanner lukija = new Scanner(is);``

Jos tiedosto olisi ollut esimerkiksi kuva ``munkuva.jpg`` kansiossa ``<projektikansio>/src/main/resources/images/munkuva.jpg``, voidaan se ladata seuraavasti:

``InputStream is = getClass().getClassLoader().getResourceAsStream("images/munkuva.jpg");``

Ja lukea streamista BufferedImageksi:

``BufferedImage bf = ImageIO.read(is);``
