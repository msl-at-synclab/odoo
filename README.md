# Odoo

Appunti su Odoo.

## Installazione

Le istruzioni generali
[si trovano qui](https://www.odoo.com/documentation/8.0/setup/install.html).

Di seguito sono riassunte quelle testate per l'ultima versione di OS X (e ci
sono alcune differenze rispetto alle istruzioni nel link precedente, che quindi
non sono del tutto corrette).

### OS X

Scaricare Odoo:

``` bash
wget -O- https://raw.githubusercontent.com/odoo/odoo/master/odoo.py | python
```

**Nota:** Su OS X `wget` non è installato di default. Lo si può installare
usando il package manager [Homebrew](http://brew.sh/).

Installare [Postgres](http://postgresapp.com/) (ricordare di [aggiornare la
variabile d'ambiente](http://postgresapp.com/documentation/cli-tools.html)
`PATH`), [Node.js](https://nodejs.org/en/) e poi dare i seguenti comandi (per
installare le ultime dipendenze ed avviare Odoo):

``` bash
sudo npm install -g less less-plugin-clean-css
cd odoo
pip install -r requirements.txt
python odoo.py
```

Aprire poi il browser per effettuare il primo login (`email`: admin, `password`:
admin) all'indirizzo [http://localhost:8069/](http://localhost:8069/).

## Primi passi

Andare su `Settings > Users` per abilitare le `Technical Features` per l'utente
amministratore (necessario ad esempio per lo sviluppo di moduli).

Provare poi ad installare qualche modulo e a interagire con l'interfaccia.
Seguire poi
[questo tutorial](https://www.odoo.com/documentation/8.0/howtos/backend.html)
per creare moduli.

**Nota:** Dopo aver creato un modulo, prima di poterlo installare, può essere
necessario su `Settings > Modules > Update Modules List`.
