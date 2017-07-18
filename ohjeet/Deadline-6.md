# Lopullinen palautus

### Clean-code
* Ohjelmasi tulisi noudattaa [koodin laatuvaatimuksia](Koodin-laatuvaatimukset.md) mahdollisimman hyvin
* Checkstyle raportti toimii hyvänä suunnannäyttäjänä
* Kiinnostuneiden kannattaa tutustua [SonarQubeen](http://www.sonarqube.org/)

### JavaDoc
* Kaikki luokat, attribuutit ja julkiset metodit dokumentoidaan
* Javadocia **ei** tarvitse kirjoittaa...
  * Testeille
  * @Override -metodeille
  * Yksityisille (private) metodeille
  * Gettereille ja Settereille, jotka eivät tee mitään ylimääräistä
  * Käyttöliittymäluokkien metodeille (esim Netbeanssin generoimat JFramet yms.)
* Generoi HTML javadoc [ohjeiden](JavaDoc.md#javadocin-generointi) mukaan.
* Docit generoityvat kansioon `target/site/apidocs`
* Kopioi apidocs repositorion juureen (ks. [kansiorakenne](Deadline-1.md#noudata-kansiorakennetta))
* JavaDoc kannattaa myös linkata pit- ja checkstyle-raporttien tapaan README:hen

### Kirjoita rakennekuvaus
* Kirjoita lyhyt, muutaman tekstikappaleen kuvaus ohjelmasi rakenteesta
* Toisin sanoen: Avaa luokkakaaviotasi sanallisesti
* Tallenna kuvaus omaan tiedostoonsa tai aihemäärittelyn jatkoksi

### Kirjoita käyttöohjeet
* Ajattele käyttäjää, joka ei ole käyttänyt ohjelmaasi
* Jos ohjelmasi on yksinkertainen käyttää, ei käyttöohjeidenkaan tarvitse olla pitkät

### Luo ajettava jar-tiedosto
* Shade-pluginin pitäisi paketoida mukaan ohjelmasi tarvitsemat riippuvuudet, jos sellaisia on.
* Lisää pom.xml-tiedostoosi uusi plugin:

```xml
<build>
    <plugins>
        <!-- ... -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.4.3</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <transformers>
                            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>PÄÄLUOKAN_SIJAINTI</mainClass>
                                <!-- mainClass on muotoa "fi.omanimi.superprojekti.Main" -->
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

* Korvaa PÄÄLUOKAN_SIJAINTI omalla pääluokallasi (siis haluamallasi `main`-metodin toteuttavalla luokalla, esimerkiksi `fi.omanimi.superprojekti.Main`).
* Valitse Netbeansista "Clean & Build". Komentoriviltä paketin saa luotua komennolla `mvn package`. Jar-tiedosto luodaan projektikansiosi `target`-kansion sisään.
* Kokeile .jar -tiedoston toimivuus. Komentoriviltä jar-tiedosto voidaan ajaa komennolla `java -jar paketti.jar`.
   * Jos ohjelma ei toimi, tarkista erityisesti ohjelmasi käyttämät tiedostopolut - ne ovat suhteellisia .jar-tiedoston sijaintiin
     * **Javan File-toiminnot on tarkoitettu vain ulkoisten tiedostojen avaamiseen (esim. kuvankäsittelyohjelmassa jonkun kuvan avaamiseen). Jos projektisi sisältää jotain tiedostoja, jotka haluat pakata sen mukaan, [lue tämä](tiedostot-jarissa.md).**
* Kokeile ajaa ohjelmaasi myös jollain muulla kuin omalla koneellasi. Esimerkiksi natiivikirjastojen kanssa paketointi saattaa vaatia ylimääräistä säätöä - näissä tapauksissa esimerkiksi kirjaston dokumentaatio saattaa kertoa sopivimman paketointitavan.

### Release
* Luo projektista [GitHub-release](https://github.com/mluukkai/OTM2016/wiki/Viikon-5-paikanpaalla-tehtavat#github-release), ja liitä siihen mukaan target-hakemistosta löytyvä, juuri luomasi jar-tiedosto.


### Generoi Checkstyle-raportti uudestaan
* Generoi uusi Checkstyle raportti
* Lisää generoitu raportti dokumentaatiokansioon

### Generoi PIT-raportti uudestaan
* Generoi uudestaan PIT-raportti
* Lisää uusi generoitu raportti dokumentaatioon

###  Kirjoita testausdokumentaatio
* **Vapaaehtoinen**
* Testausdokumentaatio korvaa yksikkötestauksen puutteita maksimissaan +2 pistettä
* Kirjoita esimerkiksi seuraavista
  * Mitä et testannut automaattisesti?
  * Miten näitä on testattu käsin?
  * Raportoi myös mahdolliset bugit

### Varmista kaikki vielä kerran
* Tarkista, että kaikki dokumentaatio on .md, .png tai .jpg -tiedostomuodoissa
* Puske kaikki vaadittava repositorioon ennen deadlinea, viimeisin ennen deadlinea tehty commit arvostellaan
* Tarkista selaimesta, että kaikki on varmasti Githubissa
* Tarkista, että dokumentaatio on ajan tasalla: luokkakaavio vastaa koodia, ja GitHubissa ovat viimeisimmät raportit
* Tarkista, että ohjelma toimii varmasti laitoksen koneilla
* **Tarkista, että kaikki on kunnossa käyttäen [muistilistaa](Muistilista.md)**
* **Tutustu vielä tarkasti [arvosteluperusteisiin](Arvosteluperusteet.md)**
