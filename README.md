# ReactJS Kehitysympäristön pystyttäminen
[TOC]

## Suomenkielinen opas ReactJS / React käyttöönottoon

Tervetuloa GitHub sivulleni. Ilmeni tarve suomenkieliselle React käyttöönotto oppaalle ja tässä semmoinen nyt sitten olisi.

Tulen päivittämään tähän lisää tietoa myös ite Reactin käytöstä, sitä mukaan kun ehdin.



### Ladattava ja asennettava tässä järjestyksessä

### Ohjelmat

* [Git](https://git-scm.com) Versionhallintaa varten
* [NodeJS](https://nodejs.org/en/download) tarvitaan paketinhallintaa ja lokaalia serveriä varten
* [Yarn](https://yarnpkg.com/lang/en/) paketinhallintaan
* [GitKraken](https://gitkraken.com) Graafinen GIT clientti, joka helpottaa elämää **(vapaaehtoinen)**



### IDE

[Visual Studio Code](https://code.visualstudio.com/download) 

VSCode on Microsoftin kehittämä ilmainen, kehittäjien suosima IDE, joka on laajennustensa ansiosta yksi mukautuvimpia koodi-editoreita.



#### Suositellut laajennukset (Extensions)

* **Debugger for Chrome** (debuggausta varten)
* **ESLint** - ilmoittaa virheistä ja parhaansa mukaan ehdottaa korjauksia
* **GitLens** - kätevä 
* **Prettier** - tekee koodista mahdollisimman nättiä
* **vscode-icons** - iconi paketti jotta hakemistot erottaa paremmin toisistaan.
* **GitKreaken Glo** - integroi GitKrakenin Glo Boardin, jotta pääsee helposti katsomaan mitä kaikkia taskeja on projektille määritelty.



Suositeltu selain on Google Chrome, johon on hyvä ladata pari laajennusta:

[React Developer Tools](<https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi>
) 

[Redux Devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) 


## create-react-app Asennus

Jos haluat luoda React-projektin, tulee sinun ensin asentaa "create-react-app" käyttäen esimerkiksi nodejs asennuksen mukana tullutta npm-paketinhallinta työkalua.

```
npm install -g create-react-app

// -g tarkoittaa global
```



### React projekin luominen

1. Avaa Visual Studio Code
2. File -> Open Folder - navigoi kansioon johon haluat luoda React-projektisi kansion
3. Avaa Visual Studio Coden terminaali (Ctrl + Ö)
4. Luo projekti seuraavalla komennolla:
5. ```create-react-app projekti```
6. navigoi luomaasi kansioon
7. ```cd projekti```
8. aja yarn komento
9. ``yarn``
10. Yarn hakee kaikki package.jsonissa määritellyt paketit ja pitää huolen niiden riippuvuuksista.
11. React projekti on valmis ajettavaksi komennolla:
12. ```yarn start``` 

Sivu löytyy localhost:3000 osoitteesta oletuksena.



## Yarn

Yarn on nopeaan ja turvalliseen paketinhallintaan tarkoitettu sovellus jonka käyttö on äärimmäisen helppoa komentoriviltä. Mikäli kyseessä on paketti jota tarvitaan vain devaukseen, eikä production buildissa, voidaan käyttää flagia -D tai --save-dev



Yleisimpiä komentoja:

**Aloita uusi projekti** (tätä ei create-react-appin kanssa tarvi tehdä)

```yarn init```



**Asenna/tarkista kaikki moduulit ja riippuvuudet**

``yarn`` 

tai

```yarn install``` 



**Paketin / riippuvuuden lisääminen**

```yarn add paketti```

```yarn add paketti@versionumero (esim @1.0.0)```

```yarn add paketti@tagi```



**Paketin / riippuvuuden lisääminen eri riippuvuus kategorioihin**

```yarn add paketti --dev```		(devDependencies)

```yarn add paketti --peer```		(peerDependencies)

```yarn add paketti --optional```	(optionalDependencies)



**Paketin / riippuvuuden päivittäminen**

```yarn upgrade paketti```

```yarn upgrade paketti@versio (esim @1.0.0) ```

```yarn upgrade paketti@tagi```



**Paketin / riippuvuuden poistaminen**

```yarn remove paketti```



**Kehitys-serverin käynnistäminen**

```yarn start```



## webpackin konfigurointi 

Sivun tyylien osalta on toisinaan kätevää pystyä määrittelemään jokaiselle komponentille omat tyylit, ilman että nämä erilliset css-tiedostot vaikuttavat globaalisti kaikkiin tiedostoihin. "out-of-the-box" tämä ei kuitenkaan onnistu ja se vaatii pieniä säätöjä konepellin alle. 



Jotta saamme ns. CSS-moduulit käyttöön, kirjoitamme terminaaliin:

```npm run eject```

Tämä komento ejektoi projektin ja pääset muokkaamaan webpack tiedostoja jotka löytyvät kansiosta "config". Komennon jälkeen sinulta kysytään vielä varmistus, johon tulee vastata "Y". Tämä komento on peruuttamaton.

Meidän täytyy muokata kahta tiedostoa jotka löytyvät vasta ilmestyneestä "config" kansiosta.

### webpack.config.dev.js

Hae sivulta paikka missä lukee "css-loader". (Ctrl + F)

Loaderin "options" alle lisäämme kaksi riviä "importLoader: 1," kohdan alle:

```
modules: true,
localIdentName: '[name]__[local]__[hash:base64:5]'
```

Tallenna tiedosto!



### webpack.config.prod.js

Samat rivit lisätään myöskin tähän tiedostoon hakemalla jälleen "css-loader" ja lisäämällä ne "sourceMap: shouldUseSourceMap," kohdan alle:

```
modules: true,
localIdentName: '[name__[local]__[hash:base64:5]'
```

Tallenna tiedosto



## CSS-moduulien käyttö

esimerkki.css

```
.Luokka1 {
    text-align: center;
}
.Luokka2 {
    // css määrittelyä
}

```

esimerkki.js 

```
import React, {Component} from 'react'
import classes from './Esimerkki.css'

class Esimerkki extends Component {
    
    render() {
        return (
        <div className={classes.Luokka1}>
        	<div className={classes.Luokka2}
        		<p>Hello React!</p>
        	</div>
        </div>
        )
    }
}

export default Esimerkki;

```

Yläpuolella olevassa esimerkissä ei oikein ole mitään järkeä, mutta siitä näkee kuinka voimme käyttää css tiedostosta luokkia eri elementteihin kätevästi käyttäen niitä classesin kautta.

Huomioitavaa on että kun moduuliin importoidaan asioita, esimerkiksi toisia .js moduuleja, meidän ei tarvitse kirjoittaa .js päätettä esim:

```
import Moduuli from './Sivu/Sivu'
```

CSS tiedostojen osalta meidän tulee määritellä myöskin tiedostotyyppi:

```
import classes from './Sivu.css'
```