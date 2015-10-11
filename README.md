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
per creare moduli. La prossima sezione riporta alcune informazioni utili
ad affrontare il tutorial con un po' di consapevolezza.

**Nota:** Dopo aver creato un modulo, prima di poterlo installare, può essere
necessario su `Settings > Modules > Update Modules List`.

## Architettura dei moduli Odoo

Un modulo è costituito essenzialmente da dati e interfacce per la gestione di
tali dati.

I dati vanno modellati attraverso classi Python. Ciascuna classe raggruppa un
insieme omogeneo di dati (es. i dati relativi ad un cliente in un modulo che
gestisce vendite). Ciascun dato viene descritto attraverso un attributo della
classe, ad esempio indicandone il tipo, o il fatto se sia necessario
valorizzarlo o se è opzionale. Ecco quindi un esempio di _modello_ Odoo:

``` python
class Course(models.Model):
    _name = 'openacademy.course'

    name = fields.Char(string="Title", required=True)
    description = fields.Text()
```

Sono ovviamente possibili associazioni fra modelli ed è Odoo a gestire la
persistenza, offrendo sostanzialmente lo stesso servizio di uno strumento ORM.
Inoltre Odoo consente di fornire dei dati di partenza, pre-caricati al momento
in cui il modulo viene installato. Tali dati vanno forniti attraverso un file
XML.

Tramite XML vengono anche descritte le interfacce per la gestione dei dati.
In prima istanza bisogna immaginare la barra principale di Odoo, dove sono
elencati (alcuni) dei moduli installati. Tramite XML è possibile richiedere
per il proprio modulo la presenza di un elemento sulla barra.

![](https://raw.githubusercontent.com/msl-at-synclab/odoo/master/img/001.png)

Una volta cliccato su quell'elemento si apre l'interfaccia del proprio modulo,
a sua volta composta da una barra laterale ed una sezione principale.

![](https://raw.githubusercontent.com/msl-at-synclab/odoo/master/img/002.png)

Nella barra laterale vengono riportati i modelli definiti dal modulo. Nella
sezione principale è possibile visualizzare, cercare, creare, modificare e
cancellare i record appartenenti al modello selezionato. Molte di queste
funzioni sono disponibili di default. Altre possono essere aggiunte, così
come è possibile personalizzare quelle già presenti, il tutto attraverso
XML.

Ovviamente questa è una panoramica molto rapida, per i dettagli [si rimanda al
tutorial](https://www.odoo.com/documentation/8.0/howtos/backend.html).
