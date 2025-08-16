# SMPO - Social Media Ostracism Paradigm v4 (Like/Unlike)

Paradigma di Ostracismo sui Social Media - Versione italiana v4 con sistema Like/Unlike e tracking delle interazioni per esperimenti di ricerca psicologica.

## 🌐 Demo Online
**Sito Live:** [https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/](https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/)

## 📋 Descrizione

Questa versione v4 del Social Media Ostracism Paradigm (SMPO) italiano introduce le seguenti modifiche per lo studio dell'ostracismo sociale digitale:

- **Sistema Like/Unlike**: I partecipanti possono mettere e rimuovere i "mi piace" sui post
- **Tracking comportamentale**: Registrazione timestamp e dettagli di tutte le interazioni
- **Passaggio dati automatico**: Invio parametri comportamentali al questionario finale
- **Interfaccia web standard**: Simulazione di piattaforma social media

I partecipanti interagiscono con 11 profili virtuali attraverso like e visualizzano commenti automatici. I ricercatori possono manipolare il numero e timing dei like ricevuti tramite 3 condizioni sperimentali predefinite.

## 🆕 Funzionalità v4

### Sistema Like/Unlike
- **Bottone like**: Click per aggiungere/rimuovere like con cambio stato visivo
- **Contatori**: Aggiornamento numerico in tempo reale
- **Stato persistente**: Mantenimento stato like/unlike durante la sessione

### Tracking Interazioni
- **Registrazione like**: Username, avatar, timestamp, tempo relativo dall'inizio
- **Registrazione unlike**: Tutti i dettagli delle rimozioni like
- **Array cronologico**: Sequenza temporale completa delle interazioni
- **Esportazione dati**: Preparazione parametri URL per questionario

### Feedback Visivo
- **Animazione like**: Scaling 1.05x e box-shadow blu (1000ms)
- **Animazione unlike**: Scaling 0.95x e box-shadow rosso (1000ms)
- **Cambio bottone**: Transizione da "Mi piace" (blu) a "Piaciuto!" (rosso)
- **CSS transitions**: 300ms per fluidità

## 🔧 Configurazione Rapida

### 1. File Profili Virtuali - profiles.json

File di configurazione per i profili utente virtuali e timing delle interazioni:

```json
window.others = {
  "posts": [
    {
      "avatar": "avatars/others/george.png",
      "username": "Georgeee", 
      "text": "Sono un ragazzo di 19 anni del Wisconsin...",
      "likes": [45000, 50000, 110000, 150000]
    }
  ]
};
```

**Campi configurabili:**
- `username`: Nome utente del profilo virtuale
- `text`: Contenuto del post
- `likes`: Array timing like automatici (millisecondi dall'inizio task)
- `avatar`: Path file immagine profilo

### 2. Configurazioni Condizioni Sperimentali

**Nel file main.js - funzione set_settings():**

```javascript
function set_settings() {
    // Durata task
    settings.tasklength = 180000; // 3 minuti
    
    // Avatar disponibili per selezione utente
    settings.numberofavatars = 12;
    
    // Condizione 1: Ostracismo (1 like ricevuto)
    settings.condition_1_likes = [12000, 9999999];
    
    // Condizione 2: Inclusione (6 like ricevuti)  
    settings.condition_2_likes = [10000, 15000, 35000, 80000, 132000, 150000];
    
    // Condizione 3: Sovrainclusione (9 like ricevuti)
    settings.condition_3_likes = [10000, 11000, 15000, 35000, 80000, 100000, 110000, 150000, 20000];
    
    // Compensazione like per altri profili
    settings.condition_1_adjusted_likes = [12000, 14000, 15000, 35000, 80000, 100000, 110000, 150000, 20000];
    settings.condition_2_adjusted_likes = [12000, 14000, 15000, 35000, 80000];
    settings.condition_3_adjusted_likes = [12000, 9999999];
    
    // Nomi utenti per notifiche like ricevuti
    settings.likes_by = ['John','AncaD','Sarah','Arjen','Jane','George','Dan','Heather','Ky'];
}
```

**Parametri timing:**
- Valori in millisecondi dall'inizio del task
- `9999999`: Placeholder per like non eseguiti
- Timing bilanciato tra condizioni per controllo sperimentale

### 3. Sistema Tracking

**Variabili globali (main.js):**

```javascript
window.likeData = {
    totalLikes: 0,           // Contatore like dati
    totalUnlikes: 0,         // Contatore unlike eseguiti
    likeHistory: [],         // Array oggetti dettagli like
    unlikeHistory: [],       // Array oggetti dettagli unlike  
    taskStartTime: null      // Timestamp inizio task
};
```

**Struttura oggetti tracking:**
```javascript
// Esempio oggetto like registrato
{
    username: "Sarah",
    avatar: "other_sarah", 
    timestamp: 1691234567890,
    timeFromTaskStart: 15234,
    formattedTime: "2025-08-11T10:15:30.000Z"
}
```

### 4. Configurazione Avatar

**Struttura directory:**
```
avatars/
├── avatar_0.png          # Avatar selezione utente (formato: avatar_N.png)
├── avatar_1.png          
├── ...
├── avatar_11.png         # Numero configurabile in main.js
└── others/               # Avatar profili virtuali
    ├── george.png
    ├── sarah.png
    ├── john.png
    └── ...
```

**Configurazione main.js:**
```javascript
settings.numberofavatars = 12; // Numero avatar disponibili per utente
```

**Specifiche tecniche:**
- Formato: PNG 250x250px
- Denominazione: Sequenza numerica da 0
- Directory others: Nomi corrispondenti a profiles.json

### 5. Parametri URL per Condizioni

**Formato standard:**
```
https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=N&p=ID&redirect=URL
```

**Parametri:**
- `c`: Condizione (1, 2, 3)
- `p`: ID partecipante (formato 001, 002, ...)
- `redirect`: URL questionario codificato

**Esempi implementazione:**
```
Condizione 1: ?c=1&p=001&redirect=https%3A//questionario.com/form/SV_123
Condizione 2: ?c=2&p=002&redirect=https%3A//questionario.com/form/SV_123
Condizione 3: ?c=3&p=003&redirect=https%3A//questionario.com/form/SV_123
```

### 6. Dati Esportati al Questionario

**Parametri base (dalla versione originale):**
- `p`: ID partecipante
- `c`: Condizione assegnata (1-3)
- `u`: Username inserito
- `av`: Numero avatar selezionato
- `d`: Descrizione personale

**Nuovi parametri v4 (comportamentali):**
- `total_likes`: Numero like attivi finali
- `liked_usernames`: Lista CSV utenti con like
- `liked_avatars`: Lista CSV avatar con like
- `like_times`: Lista CSV timestamp like (ms)
- `total_unlikes`: Numero like rimossi
- `unliked_usernames`: Lista CSV utenti unlike
- `unliked_avatars`: Lista CSV avatar unlike
- `unlike_times`: Lista CSV timestamp unlike (ms)

**Esempio URL finale generato:**
```
questionario.com/form/SV_123?p=001&c=2&u=TestUser&av=5&d=Descrizione&total_likes=3&liked_usernames=Sarah,John&like_times=15000,32000&total_unlikes=1&unliked_usernames=Sarah&unlike_times=67000
```

## 📁 Struttura File Principali

```
smpo-socialmedia-ita_v4__LIKE_DISLIKE/
├── index.html                    # Pagina principale con templates
├── main.js                       # Logica principale + tracking like/unlike
├── profiles.json                 # PROFILI VIRTUALI DA PERSONALIZZARE
├── style.css                     # Stili + animazioni like/unlike
├── shortcut.js                   # Gestione scorciatoie tastiera
├── avatars/                      # Directory avatar
│   ├── avatar_0.png             # Avatar selezionabili (numerati)
│   ├── avatar_1.png             
│   ├── ...
│   ├── avatar_11.png
│   └── others/                   # Avatar profili virtuali
│       ├── george.png
│       ├── sarah.png
│       ├── john.png
│       └── ...
└── README.md                     # Questo file
```

## 🎯 Implementazione Tecnica

### Animazioni CSS

**File style.css - Classi implementate:**

```css
.entry.just-liked {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(59, 89, 153, 0.3);
}

.entry.just-unliked {
    transform: scale(0.95);
    box-shadow: 0 2px 8px rgba(220, 53, 69, 0.3);
}

.btn-like:not(.liked) {
    background-color: hsl(195, 60%, 35%) !important;
    border-color: #3B5999;
}

.btn-like.liked {
    background-color: #dc3545 !important;
    border-color: #dc3545 !important;
    color: white !important;
}
```

### Event Handlers

**Main.js - Gestione click like:**

```javascript
$('.btn-like').on('click', function() {
    var isCurrentlyLiked = $(this).hasClass('liked');
    var targetUsername = $(this).closest('.entry').find('h3').text().trim();
    var targetAvatar = /* estrazione da src immagine */;
    
    if (isCurrentlyLiked) {
        registerUnlike(targetUsername, targetAvatar);
        // Aggiornamento UI per unlike
    } else {
        registerLike(targetUsername, targetAvatar);  
        // Aggiornamento UI per like
    }
    
    // Applicazione animazione temporanea (1000ms)
});
```

### Funzioni Tracking

```javascript
function registerLike(targetUsername, targetAvatar) {
    window.likeData.totalLikes++;
    window.likeData.likeHistory.push({
        username: targetUsername,
        avatar: targetAvatar,
        timestamp: new Date().getTime(),
        timeFromTaskStart: new Date().getTime() - window.likeData.taskStartTime
    });
}

function prepareLikeParams() {
    // Costruzione parametri URL per questionario
    var usernames = window.likeData.likeHistory.map(like => like.username).join(',');
    var times = window.likeData.likeHistory.map(like => like.timeFromTaskStart).join(',');
    return `&total_likes=${window.likeData.totalLikes}&liked_usernames=${encodeURIComponent(usernames)}&like_times=${encodeURIComponent(times)}`;
}
```

## 🚪 Accesso e Navigazione Sistema

### Entry Points

**URL base:**
```
https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/
```

**Con parametri sperimentali:**
```
https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=N&p=ID&redirect=URL
```

**Gestione parametri (main.js):**
```javascript
function get_params() {
    // Condizione: validazione 1-3, default 1
    if(window.QueryString.c !== undefined && parseInt(window.QueryString.c) > 0 && parseInt(window.QueryString.c) < 4) {
        window.condition = parseInt(window.QueryString.c);
    } else {
        window.condition = 1;
    }
    
    // ID partecipante: validazione numerica, default 0
    if(window.QueryString.p !== undefined && !isNaN(parseInt(window.QueryString.p))) {
        window.participant = parseInt(window.QueryString.p);
    } else {
        window.participant = 0;
    }
    
    // URL redirect: decodifica automatica
    if(window.QueryString.redirect !== undefined) {
        window.redirect = decode(window.QueryString.redirect);
    }
}
```

### Flusso Interfaccia Utente

**1. Schermata Introduzione (`#intro`)**
- Elemento DOM: `<div id="intro">`
- Trigger: `$('#submit_intro').on('click')`
- Validazione: Nessuna
- Next: `init_name()`

**2. Inserimento Username (`#name`)**
- Campo: `<input id="username">`
- Validazione: `not_alphanumeric()` function
- Limitazioni: Solo caratteri alfanumerici, no spazi
- Storage: `window.username = $('#username').val()`
- Next: `init_avatar()`

**3. Selezione Avatar (`#avatar`)**
- Generazione dinamica: Loop da 0 a `settings.numberofavatars`
- Template: `<img id="avatar_X" src="avatars/avatar_X.png" class="avatar" />`
- Selezione: Click handler aggiunge classe `.selected`
- Storage: `window.avatar` e `window.avatarexport`
- Next: `init_text()`

**4. Descrizione Personale (`#text`)**
- Campo: `<textarea id="description">`
- Contatore caratteri: Real-time con `keyup()` event
- Validazione: 140-400 caratteri
- Storage: `window.description = $('#description').val()`
- Next: `init_fb_intro()`

**5. Istruzioni Task (`#fb_intro`)**
- Elemento: Static content
- Trigger: Click handler
- Next: `init_fb_login()`

**6. Loading Screen (`#fb_login`)**
- Timer: `setTimeout(8000)` per simulazione caricamento
- Indicator: `$("#loader")` con animazione
- Message: `$('#msg_all_done').show()` dopo delay
- Next: `init_task()`

**7. Task Principale (`#task`)**
- **Inizializzazione timing:** `window.likeData.taskStartTime = new Date().getTime()`
- **Setup countdown:** `jQuery("#countdown").countDown()`
- **Rendering posts:** Mustache.js templating
- **Event binding:** Click handlers per `.btn-like`
- **Auto-redirect:** `setTimeout(window.settings.tasklength)`

### Controlli Accesso

**Validazione ingresso:**
```javascript
// Controllo parametri URL validi
if (!validCondition(c) || !validParticipant(p)) {
    // Fallback a valori default, logging errore
}

// Prevenzione uscita accidentale
$(window).bind('beforeunload', function(){
    return 'Sei sicuro di voler abbandonare?';
});

// Disabilitazione tasti sistema
shortcut.add("f5", function() {}); // F5 disabled
shortcut.add("Backspace", function() {}); // Backspace disabled
```

**Stati sessione:**
- **Pre-task:** Raccolta dati utente, no tracking attivo
- **Task attivo:** `window.likeData.taskStartTime` settato, tracking abilitato
- **Post-task:** Countdown terminato, redirect automatico attivato

## 🔗 Processo Sperimentale

### Fasi Esperimento

1. **Setup partecipante**
   - Selezione avatar da griglia 12 opzioni
   - Inserimento username (validazione alfanumerica)
   - Composizione descrizione personale (140-400 caratteri)

2. **Task principale (180 secondi)**
   - Inizializzazione `window.likeData.taskStartTime`
   - Visualizzazione post utente + 11 post profili virtuali
   - Interazione like/unlike con tracking completo
   - Ricezione like automatici secondo condizione

3. **Esportazione dati**
   - Costruzione URL con parametri comportamentali
   - Redirect automatico al questionario configurato

### Controlli Sperimentali

**Bilanciamento tra condizioni:**
- Totale like ricevuti sistema: Costante tra condizioni
- Distribuzione temporale: Controllata tramite timing array
- Compensazione altri profili: Inversamente proporzionale a partecipante

**Validazione dati:**
- Controllo consistenza timestamp
- Verifica coerenza like/unlike ratio
- Log debugging per troubleshooting

## 📊 Output Dati

### Variabili Comportamentali

**Metriche quantitative:**
- Numero like dati (`total_likes`)
- Numero unlike eseguiti (`total_unlikes`) 
- Ratio indecisione: `total_unlikes / (total_likes + total_unlikes)`
- Tempo medio tra like successivi
- Pattern temporale interazioni

**Variabili qualitative:**
- Preferenze utenti (array `liked_usernames`)
- Sequenza temporale decisioni (`like_times`, `unlike_times`)
- Coerenza comportamentale (like → unlike sullo stesso target)

### Integrazione Questionario

**Embedded Data Fields consigliati (Qualtrics):**
```
p, c, u, av, d, total_likes, liked_usernames, liked_avatars, 
like_times, total_unlikes, unliked_usernames, unliked_avatars, unlike_times
```



## 📚 Riferimenti

Base teorica:
> Wolf, W., Levordashka, A., Ruff, J. R., Kraaijeveld, S., Lueckmann, J.-M., & Williams, K. D. (2014). Ostracism Online: A social media ostracism paradigm. *Behavior Research Methods*, 47(4), 973-991.

## 🚀 Modifiche v4

**Implementazione tecnica:**
- Sistema tracking like/unlike con timestamp precisi
- Esportazione dati comportamentali parametrizzata
- Event handlers jQuery per gestione click
- CSS transitions per feedback visivo

**Compatibilità:**
- Mantenimento parametri base versioni precedenti
- Estensione senza breaking changes
- Logging debug per monitoraggio funzionamento

---

*Versione 4.0 - Aggiornato Agosto 2025*  
*emiliano.pes@uniroma1.it*
