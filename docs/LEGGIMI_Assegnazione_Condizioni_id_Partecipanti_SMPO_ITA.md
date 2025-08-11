# LEGGIMI - Assegnazione Condizioni Partecipanti SMPO ITA v4

File CSV per assegnare i partecipanti agli ID e alle condizioni sperimentali con generazione automatica dei link di partecipazione per la **versione v4 con sistema Like/Rimozione Like**.

Nel subfolder `ESEMPIO_Assegnazione_condizioni_partecipanti/` è disponibile un file esempio:
* `partecipanti_smpo_ita_v4.csv`

## 📋 Struttura del File CSV

| **Campo** | **Descrizione** | **Esempio** |
|-----------|-----------------|-------------|
| Nome | Nome del partecipante | Marco |
| Cognome | Cognome del partecipante | Rossi |
| Data_Nascita | Data di nascita (YYYY-MM-DD) | 1995-03-15 |
| Sesso | Genere (M/F) | M |
| ID | Identificativo numerico univoco (formato 001, 002...) | 001, 002, 003 |
| Condizione | Condizione sperimentale (1-3) | 1, 2, 3 |
| Link_Partecipazione | URL generato automaticamente (formula) | - |

## 🎯 Condizioni Sperimentali v4

| **Valore** | **Condizione** | **Descrizione** | **Like Ricevuti** |
|------------|----------------|-----------------|-------------------|
| 1 | OSTRACISMO | Feedback sociale minimo | 1 like a 12 secondi |
| 2 | INCLUSIONE | Feedback sociale normale | 6 like distribuiti |
| 3 | SOVRAINCLUSIONE | Feedback sociale elevato | 9+ like frequenti |

## 🔧 Formula per Link Automatici v4

### Per Excel/LibreOffice:
```excel
=CONCATENA("https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=";F2;"&p=";E2;"&redirect=";G1)
```

### Per Google Sheets:
```
="https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c="&F2&"&p="&E2&"&redirect="&$G$1
```

**Dove:**
* `F2` = Cella della Condizione (colonna F)
* `E2` = Cella dell'ID (colonna E, formato 001, 002...)
* `G1` = Cella contenente l'URL del questionario già codificato (riferimento assoluto)

## 🆕 Novità v4 - URL Aggiornato

**Nuovo URL base v4:**
```
https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html
```

**Differenze dalla versione precedente:**
- ✅ Sistema Like con possibilità di rimozione
- ✅ Tracking completo delle interazioni (like dati + like rimossi)
- ✅ Animazioni feedback visivo migliorate
- ✅ Dati comportamentali più dettagliati inviati al questionario

## 🔐 Come Preparare l'URL Codificato

1. **Prendi il tuo link del questionario:**
   ```
   https://tuapiattaforma.qualtrics.com/jfe/form/SV_TUOCODICE
   ```

2. **Codificalo usando un tool online (cerca "URL encoder"):**
   ```
   https%3A//tuapiattaforma.qualtrics.com/jfe/form/SV_TUOCODICE
   ```

3. **Inserisci nella cella G1** del foglio di calcolo
4. **La formula farà riferimento a G1** per tutti i link

## 📊 Esempio di Dati v4

### Template con URL codificato in G1

| G1 (URL Codificato) |
|---------------------|
| https%3A//tuapiattaforma.qualtrics.com/jfe/form/SV_TUOCODICE |

### Dati Partecipanti

| Nome | Cognome | Data_Nascita | Sesso | ID | Condizione | Link_Partecipazione |
|------|---------|--------------|-------|----|-----------|--------------------|
| Marco | Rossi | 1995-03-15 | M | 001 | 1 | https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=1&p=001&redirect=https%3A//tuapiattaforma... |
| Giulia | Bianchi | 1997-07-22 | F | 002 | 2 | https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=2&p=002&redirect=https%3A//tuapiattaforma... |
| Alessandro | Verdi | 1993-11-08 | M | 003 | 3 | https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=3&p=003&redirect=https%3A//tuapiattaforma... |

## 💡 Utilizzo Setup v4

### Setup Iniziale

1. **Apri** un nuovo foglio di calcolo
2. **Inserisci** nella cella G1 il tuo URL Qualtrics codificato
3. **Compila** i dati dei partecipanti (Nome, Cognome, Data_Nascita, Sesso)
4. **Assegna** ID numerici con zero padding (001, 002, 003...)
5. **Assegna** condizioni (1, 2, 3) secondo il tuo disegno sperimentale
6. **Copia** la formula nella colonna Link_Partecipazione per tutti i partecipanti
7. **Testa** almeno un link per ogni condizione prima della distribuzione
8. **Invia** il link personalizzato a ciascun partecipante

### Verifica Funzionamento

**Test rapido delle condizioni:**
- Condizione 1: https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=1&p=999
- Condizione 2: https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=2&p=999
- Condizione 3: https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=3&p=999

## 🆕 Dati v4 Inviati al Questionario

Con la versione v4, oltre ai parametri base vengono automaticamente inviati:

**Parametri Base:**
- `p`: ID partecipante (001, 002...)
- `c`: Condizione (1, 2, 3)
- `u`: Username scelto
- `av`: Avatar selezionato
- `d`: Descrizione scritta

**Nuovi Parametri Comportamentali v4:**
- `total_likes`: Numero like attivi finali
- `liked_usernames`: Lista utenti con like
- `liked_avatars`: Lista avatar con like
- `like_times`: Timestamp dei like
- `total_unlikes`: Numero like rimossi
- `unliked_usernames`: Lista utenti da cui rimosso like
- `unliked_avatars`: Lista avatar da cui rimosso like
- `unlike_times`: Timestamp rimozioni like

## 🔐 Sicurezza e Privacy v4

**Vantaggi di questo approccio:**
- ✅ Repository pubblico senza link privati esposti nel codice
- ✅ URL completo direttamente utilizzabile dai partecipanti
- ✅ Formula semplice con riferimento centralizzato (cella G1)
- ✅ Redirect automatico al questionario con tutti i dati v4
- ✅ Tracking comportamentale dettagliato per analisi avanzate

## 🛠️ Strumenti Utili

- **URL Encoder online**: Cerca "URL encoder" su Google
- **Test GitHub Pages**: https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/
- **Fogli di calcolo**: Excel, LibreOffice Calc, Google Sheets
- **Documentazione v4**: README.md nel repository

## 📈 Bilanciamento Sperimentale

Per un disegno bilanciato tra-soggetti con 3 condizioni:

### Assegnazione Sequenziale
```
Partecipanti 001, 004, 007, 010... → Condizione 1 (OSTRACISMO)
Partecipanti 002, 005, 008, 011... → Condizione 2 (INCLUSIONE)  
Partecipanti 003, 006, 009, 012... → Condizione 3 (SOVRAINCLUSIONE)
```

### Assegnazione per Blocchi
```
Blocco 1: 001-003 → Condizioni 1,2,3
Blocco 2: 004-006 → Condizioni 2,3,1
Blocco 3: 007-009 → Condizioni 3,1,2
```

### Formula Excel per Assegnazione Automatica
```excel
=MOD(E2-1;3)+1
```
(Dove E2 è la cella dell'ID partecipante)

## 🚨 Checklist Pre-Distribuzione

- [ ] URL base v4 corretto nel foglio di calcolo
- [ ] URL Qualtrics codificato correttamente in G1
- [ ] Formula applicata a tutti i partecipanti
- [ ] ID in formato 001, 002, 003... (con zero padding)
- [ ] Condizioni bilanciate tra partecipanti
- [ ] Almeno un link testato per ogni condizione
- [ ] Questionario Qualtrics configurato per ricevere nuovi parametri v4
- [ ] Embedded Data Fields impostati per dati comportamentali

## 📋 Template Formula Completa

**Per Excel/LibreOffice (copia in colonna G):**
```excel
=CONCATENA("https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c=";F2;"&p=";E2;"&redirect=";$G$1)
```

**Per Google Sheets (copia in colonna G):**
```
="https://VILLINODIPPSI.github.io/smpo-socialmedia-ita_v4__LIKE_DISLIKE/index.html?c="&F2&"&p="&E2&"&redirect="&$G$1
```

La formula genererà automaticamente l'URL corretto per ogni partecipante con il proprio ID, condizione assegnata e redirect al questionario configurato per ricevere tutti i nuovi dati comportamentali v4.

---

*Versione 4.0 - Aggiornato Agosto 2025*  
*Contatto: emiliano.pes@uniroma1.it*
