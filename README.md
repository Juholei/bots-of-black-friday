# bots-of-black-friday

## Pelin kulku

* Serveri lähettää botille pelitilan, johon botin on vastattava omalla siirrollaan, joka on liikkuminen (UP, DOWN, LEFT, RIGHT), esineen nostaminen (PICK) tai esineen käyttäminen (USE).
* Virheellisistä siirroista (seinään juokseminen, olemattoman esineen hamuilu, siirron palauttamisessa viivästely, rajapintavirheet yms) botin kunto vähenee. Kuolleet botit poistetaan kaupasta vartijoiden toimesta.
* Kaupan esineillä on hinta ja alennusprosentti. Mitä kovempi alennus, sitä kauemmin esineen nostamisessa kestää.
* Botilla on tietty määrä rahaa, joka kuluu ostoksia tehdessä.
* Jos botti on kertonut nostavansa esinettä siirrolla PICK, lähettää serveri tilaa (PlayerState) PICK niin kauan kuin esineen nostamista pitää jatkaa kunnes se on kokonaan hallussa. Botin on silloin vastattava siirrolla PICK, kunnes serveri
alkaa taas antamaan tilaa MOVE. Jos nostoa ei suoriteta loppuun asti, jää esine kauppaan.
* Mitä enemmän rahallista arvoa saa koottua pelin aikana, sitä korkeammalle pääsee top-listalla.
* Koska Black Friday, osa esineistä on aseita, joita käyttämällä voi vahingoittaa lähintä kanssashoppailijaa.
* Kun botilla ei ole enää varaa ostaa esineitä, on sen suunnattava pois kaupasta kassan kautta, jolloin peli päättyy sen osalta. Varastaminen on rangaistava teko, josta saa sakinhivutusta.
* Kassalle ei kannata hortoilla kesken pelin, jos ei halua poistua ennenaikaisesti.
* Kaupoissa voi olla seiniä, jotka hankaloittavat kulkua.

## Rajapinta

* Rajapinnan tietosisältö on nähtävissä esimerkkibotissa.

#### Esimerkkiviesti

Tilanne botin rekisteröityessä.

```

{
  "id": "d011658d-0d8e-4d37-820b-166f8959647d",
  "player": {
    "name": "ED-209",
    "url": "http://192.168.2.200:3002/round",
    "position": {
      "x": 88,
      "y": 25
    },
    "score": 0,
    "money": 5000,
    "state": "MOVE",
    "timeInState": 0,
    "usableItems": [],
    "actionCount": 0,
    "health": 100
  },
  "gameState": {
    "map": {
      "width": 92,
      "height": 28,
      "maxItemCount": 5,
      "tiles": [
        "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "xx________________________________________________________________________________________xx",
        "xx________________________________________________________________________________________xx",
        "xx_______o_____________######################xx######################_____________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx_____________________######################xx######################_____________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx___________________________________________xx___________________________________________xx",
        "xx_____________________######################xx######################_____________________xx",
        "xx________________________________________________________________________________________xx",
        "xx________________________________________________________________________________________xx",
        "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      ],
      "name": "citymarket",
      "exit": {
        "x": 9,
        "y": 4
      }
    },
    "players": [
      {
        "name": "ED-209",
        "url": "http://192.168.2.200:3002/round",
        "position": {
          "x": 88,
          "y": 25
        },
        "score": 0,
        "money": 5000,
        "state": "MOVE",
        "timeInState": 0,
        "usableItems": [],
        "actionCount": 0,
        "health": 100
      }
    ],
    "finishedPlayers": [
      {
        "name": "ED-209",
        "url": "http://localhost:3002/round",
        "position": {
          "x": 9,
          "y": 4
        },
        "score": 10370,
        "money": 773,
        "state": "MOVE",
        "timeInState": 0,
        "usableItems": [
          {
            "price": 2305,
            "discountPercent": 83,
            "position": {
              "x": 89,
              "y": 18
            },
            "type": "WEAPON",
            "isUsable": true
          },
          {
            "price": 3865,
            "discountPercent": 73,
            "position": {
              "x": 33,
              "y": 12
            },
            "type": "WEAPON",
            "isUsable": true
          }
        ],
        "actionCount": 181,
        "health": 80
      }
    ],
    "items": [
      {
        "price": 3864,
        "discountPercent": 35,
        "position": {
          "x": 27,
          "y": 10
        },
        "type": "JUST_SOME_JUNK",
        "isUsable": false
      },
      {
        "price": 2300,
        "discountPercent": 34,
        "position": {
          "x": 2,
          "y": 24
        },
        "type": "JUST_SOME_JUNK",
        "isUsable": false
      },
      {
        "price": 2994,
        "discountPercent": 20,
        "position": {
          "x": 80,
          "y": 17
        },
        "type": "JUST_SOME_JUNK",
        "isUsable": false
      },
      {
        "price": 1917,
        "discountPercent": 23,
        "position": {
          "x": 35,
          "y": 22
        },
        "type": "JUST_SOME_JUNK",
        "isUsable": false
      },
      {
        "price": 3886,
        "discountPercent": 26,
        "position": {
          "x": 36,
          "y": 22
        },
        "type": "JUST_SOME_JUNK",
        "isUsable": false
      }
    ],
    "round": 111825,
    "shootingLines": []
  }
}

```

### Frontti

* npm install
* npm run-script watch