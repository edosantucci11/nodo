# Nodo

Note, attività, progetti e calendario in un'unica app, con un assistente AI che trasforma gli impegni lunghi in passaggi con le date.

Nodo è una **web app installabile**: si apre dal browser e si aggiunge alla schermata Home di iPhone e Android, come un'app normale. Funziona anche offline e i dati restano sul dispositivo.

## Funzioni

- **Presentazione iniziale** al primo avvio, con la scelta tra dati di esempio e agenda vuota (si rivede da Impostazioni).
- **Oggi**: eventi della giornata su una linea del tempo, attività in scadenza, note recenti.
- **Cattura rapida** in linguaggio naturale: «Riunione con Marco venerdì alle 10 @Lavoro» diventa un evento con data, ora e progetto.
- **Progetti** che raccolgono attività, eventi e note, con avanzamento.
- **Note collegate**: `[[Titolo]]` collega due note, `- [ ] cosa fare domani` crea un'attività legata alla nota, `#tag` per i tag.
- **Attività** con priorità (`!1`–`!4`), scadenze, filtri.
- **Calendario** mensile.
- **Focus**: timer Pomodoro collegato a un'attività.
- **Assistente AI** (Claude o OpenAI) con la tua chiave API.
- **Notifiche**: promemoria per attività ed eventi, riepilogo del mattino, ore di silenzio.
- **Impostazioni**: tema, colori, animazioni, trasparenza, sezioni di Oggi, valori predefiniti, backup.

## Struttura

```
nodo/
├── index.html            l'app (HTML, CSS e JavaScript in un unico file)
├── manifest.webmanifest  nome, colori e icone per l'installazione
├── sw.js                 service worker: funzionamento offline e notifiche
├── icons/                icone dell'app (logo, favicon, icone per iOS e Android)
├── .nojekyll             dice a GitHub Pages di servire i file così come sono
└── README.md
```

## Pubblicare su GitHub Pages

GitHub Pages ospita l'app gratis e con HTTPS, che serve per installarla e per farla funzionare offline. Con un account GitHub gratuito il repository deve essere **pubblico**.

1. Su GitHub crea un nuovo repository chiamato `nodo`.
2. Carica i file:
   - **dal sito**: nel repository vuoto scegli *uploading an existing file* e trascina tutto il contenuto della cartella `nodo`, compresa la cartella `icons` e il file `.nojekyll`; poi *Commit changes*;
   - **da terminale**:
     ```bash
     cd nodo
     git init
     git add .
     git commit -m "Prima versione di Nodo"
     git branch -M main
     git remote add origin https://github.com/TUO-UTENTE/nodo.git
     git push -u origin main
     ```
3. Nel repository vai in **Settings › Pages**. In *Build and deployment* scegli *Deploy from a branch*, poi il ramo `main` e la cartella `/ (root)`. Salva.
4. Dopo uno o due minuti l'app è online su `https://TUO-UTENTE.github.io/nodo/`.

## Installare l'app

- **iPhone**: apri il link con **Safari** › tasto Condividi › *Aggiungi alla schermata Home*.
- **Android**: apri il link con **Chrome** › menu ⋮ › *Installa app*.

## Aggiornare l'app

1. Modifica i file e caricali di nuovo su GitHub.
2. In `sw.js` aumenta il numero di versione (per esempio da `nodo-v0.6.0` a `nodo-v0.6.1`), così i telefoni scaricano la versione nuova invece di quella salvata.
3. Sul telefono chiudi e riapri Nodo: al secondo avvio vedrai la versione aggiornata.

## Assistente AI

Serve una chiave API personale, da inserire in **Impostazioni › Assistente**:

- **Claude**: crea la chiave su [console.anthropic.com](https://console.anthropic.com). Se lasci vuoto il campo *Modello* viene usato `claude-sonnet-5-5`.
- **OpenAI**: crea la chiave su [platform.openai.com](https://platform.openai.com) e scrivi il nome del modello che vuoi usare.

La chiave resta salvata **solo su quel dispositivo** e non viene inclusa nei backup. La richiesta parte direttamente dal telefono verso il servizio scelto. Usa una chiave personale e imposta un limite di spesa nel tuo account. Non usare questa configurazione se l'app dovesse essere usata da altre persone: in quel caso la chiave va spostata su un server.

## Notifiche

- Gli avvisi compaiono dentro l'app mentre è aperta.
- Attivando *Notifiche del sistema* nelle impostazioni arrivano anche quando Nodo è in secondo piano. Su iPhone serve Nodo aggiunto alla Home e iOS 16.4 o successivo.
- Con l'app **chiusa del tutto** una web app non può programmare promemoria: servirà la versione per App Store e Google Play (vedi Prossimi passi).

## Dati e backup

I dati sono salvati nel browser del dispositivo, non su un server. Non si sincronizzano tra telefono e computer. Fai un backup ogni tanto da **Impostazioni › Dati › Esporta**: scarichi un file JSON che puoi reimportare su qualsiasi dispositivo.

## Prossimi passi

1. Sincronizzazione tra dispositivi con un piccolo backend (per esempio Supabase, server in UE).
2. Pubblicazione su App Store e Google Play con **Capacitor**, riusando lo stesso codice: promemoria anche ad app chiusa, widget, calendari Google e Outlook.

## Crediti

- Carattere [Geist](https://vercel.com/font), licenza SIL Open Font License.
- Codice e marchio Nodo: tutti i diritti riservati.
