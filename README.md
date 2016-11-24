# Bots of black friday

> Shoppers' favorite sale is always the day after Thanksgiving sale, a.k.a. Black Friday.

![bots shopping to the death](bots.png)

## Running the server

### How to start

1. `cd server/`
2. Prepare the frontend: `npm install && npm run-script build`
3. Run the backend: `mvn spring-boot:run`

After this, the GUI can be accessed from http://localhost:8080/

### How to create a new map

```
sudo mkdir -m 777 -p /bobf-maps
touch /bobf-maps/example-map
echo "map name" >> /bobf-maps/example-map
-- limit the number of items on map to 3
echo 3 >> /bobf-maps/example-map
echo "xxxxxxxxx" >> /bobf-maps/example-map
-- x is wall, o is exit # is a trap which decreases bots health
echo "x_o____#x" >> /bobf-maps/example-map
echo "xxxxxxxxx" >> /bobf-maps/example-map
```

### How to change the map

`curl -H "Content-Type: application/json" --data "example-map" localhost:8080/changemap/`

also works for the predefined maps (see server/src/main/resources/maps)

`curl -H "Content-Type: application/json" --data "split_trap.map" localhost:8080/changemap/`

### How to increase or decrease game speed

Change the GameEngine.PAUSE_BETWEEN_ROUNDS_MILLIS and reboot. The best value depends on network latency, bot count and bot quality.

## Developing the server

You can develop the frontend with `npm run watch`.
The backend does not support live reloading, but you can run the app with your IDE, and most IDEs support hot deployment of static resources and Java code.

## Architecture

The server and the bots both provide REST API's to each other: the
server, for bots to register and tell where their REST endpoint is; the
bots, to get the current game status from server and tell the server (in
reply) what they want to do.

## Rules of the game

### In English

* The server sends the current game situation to the bots.  Every bot
  has to answer with some kind of action, be it movement (UP, DOWN,
  LEFT, RIGHT), picking up an item (PICK) or using one (USE).
* Faulty responses are penalised by decreasing the bot's health.  Dead
  bots are removed from the shop by guards.  Faulty actions include
  running into a wall, trying to pick nonexistent items, taking too long
  to form a response, protocol errors etc.
* The items in the shop have a price and a discount percentage.  The
  better the discount, the longer it takes to pick up.
* Every bot has a given amount of money, which is spent on shopping.
* The higher the value of items collected, the better will be the bot's
  position on the top list.
* Because it's Black Friday, some items are weapons that can be used to
  harm the nearest shopper.
* When the bot is out of money, it has to exit the shop by the cash
  register.  After this it is safely out of the game.  Stealing will be
  punished.
* Don't go too early to the cash register.  You won't be able to get
  back.
* The shops may have walls.

### Suomeksi

* Serveri lähettää botille pelitilan, johon botin on vastattava omalla siirrollaan, joka on liikkuminen (UP, DOWN, LEFT, RIGHT), esineen nostaminen (PICK) tai esineen käyttäminen (USE).
* Virheellisistä siirroista (seinään juokseminen, olemattoman esineen hamuilu, siirron palauttamisessa viivästely, rajapintavirheet yms) botin kunto vähenee. Kuolleet botit poistetaan kaupasta vartijoiden toimesta.
* Kaupan esineillä on hinta ja alennusprosentti. Mitä kovempi alennus, sitä kauemmin esineen nostamisessa kestää.
* Botilla on tietty määrä rahaa, joka kuluu ostoksia tehdessä.
* Mitä enemmän rahallista arvoa saa koottua pelin aikana, sitä korkeammalle pääsee top-listalla.
* Koska Black Friday, osa esineistä on aseita, joita käyttämällä voi vahingoittaa lähintä kanssashoppailijaa.
* Kun botilla ei ole enää varaa ostaa esineitä, on sen suunnattava pois kaupasta kassan kautta, jolloin peli päättyy sen osalta. Varastaminen on rangaistava teko, josta saa sakinhivutusta.
* Kassalle ei kannata hortoilla kesken pelin, jos ei halua poistua ennenaikaisesti.
* Kaupoissa voi olla seiniä, jotka hankaloittavat kulkua.

## Rajapinta

* Rajapinnan tietosisältö on nähtävissä esimerkkibotissa.  Voit katsoa
  serverin lähettämää [esimerkkiviestiä](./example-message.md)

