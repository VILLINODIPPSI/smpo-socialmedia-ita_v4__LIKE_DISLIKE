# LEGGIMI - Risultati Qualtrics SMPO ITA v4 🇮🇹

Nel subfolder `ESEMPIO_Risultati_Qualtrics/` sono disponibili due file esempio di risultati esportati da Qualtrics con le **nuove funzionalità v4**:
- `Risultati_Qualtrics_esempio.csv`
- `Risultati_Qualtrics_esempio.xlsx`

## 📊 Colonne Sistema Qualtrics

| **Colonna** | **Interpretazione** |
|-------------|-------------------|
| StartDate | Data/ora inizio questionario |
| EndDate | Data/ora fine questionario |
| Status | Tipo risposta (Preview, IP Address, etc.) |
| Progress | Percentuale completamento (0-100) |
| Duration (in seconds) | Tempo impiegato per completare |
| Finished | Questionario completato (True/False) |
| ResponseId | ID univoco risposta Qualtrics |
| IPAddress | Indirizzo IP partecipante |

---

## 🎯 Parametri Esperimento SMPO (Base)

| **Colonna** | **Interpretazione** |
|-------------|-------------------|
| **p** | ID partecipante (001, 002, 003...) |
| **c** | Condizione: 1=Ostracismo, 2=Inclusione, 3=Sovrainclusione |
| **u** | Nome utente scelto (es. "nomepippo") |
| **d** | Descrizione scritta dal partecipante |
| **av** | ID avatar utilizzato (0, 1, 2...) |

---

## 🆕 Dati Comportamentali v4 - Sistema Like (Metti/Togli)

### 👍 Dati Like Dati dal Partecipante

| **Colonna** | **Interpretazione** | **Esempio** |
|-------------|-------------------|-------------|
| **total_likes** | Numero totale like dati (attualmente attivi) | `8` |
| **liked_usernames** | Lista nomi utenti che hanno ricevuto like | `Sarah,John,George,AncaD` |
| **liked_avatars** | Lista avatar che hanno ricevuto like | `other_sarah,other_john,other_george,other_anca` |
| **like_times** | Timestamp precisi dei like (millisecondi dall'inizio task) | `15000,32000,45000,67000` |

### 🔄 Dati Like Rimossi dal Partecipante

| **Colonna** | **Interpretazione** | **Esempio** |
|-------------|-------------------|-------------|
| **total_unlikes** | Numero totale like rimossi (click per togliere) | `2` |
| **unliked_usernames** | Lista nomi utenti da cui rimosso like | `Sarah,John` |
| **unliked_avatars** | Lista avatar da cui rimosso like | `other_sarah,other_john` |
| **unlike_times** | Timestamp precisi delle rimozioni like (millisecondi dall'inizio task) | `89000,124000` |


---

## 📝 Scale di Misurazione

### Appartenenza (Nbelong1_1 → Nbelong1_5)
| **Colonna** | **Interpretazione** | **Polarità** |
|-------------|-------------------|--------------|
| Nbelong1_1 | "Mi sono sentito/a scollegato/a" | ❌ Negativo |
| Nbelong1_2 | "Mi sono sentito/a rifiutato/a" | ❌ Negativo |
| Nbelong1_3 | "Mi sono sentito/a escluso/a" | ❌ Negativo |
| Nbelong1_4 | "Ho sentito di appartenere al gruppo" | ✅ Positivo |
| Nbelong1_5 | "Altri del gruppo interagirebbero molto con me" | ✅ Positivo |

### Autostima (Nsest1_1 → Nsest1_5)
| **Colonna** | **Interpretazione** | **Polarità** |
|-------------|-------------------|--------------|
| Nsest1_1 | "Mi sono sentito/a bene con me stesso/a" | ✅ Positivo |
| Nsest1_2 | "La mia autostima era alta" | ✅ Positivo |
| Nsest1_3 | "Mi sono sentito/a apprezzato/a" | ✅ Positivo |
| Nsest1_4 | "Mi sono sentito/a insicuro/a" | ❌ Negativo |
| Nsest1_5 | "Mi sono sentito/a soddisfatto/a" | ✅ Positivo |

### Esistenza Significativa (Nmexist1_1 → Nmexist1_5)
| **Colonna** | **Interpretazione** | **Polarità** |
|-------------|-------------------|--------------|
| Nmexist1_1 | "Mi sono sentito/a invisibile" | ❌ Negativo |
| Nmexist1_2 | "Mi sono sentito/a privo/a di significato" | ❌ Negativo |
| Nmexist1_3 | "Mi sono sentito/a inesistente" | ❌ Negativo |
| Nmexist1_4 | "Mi sono sentito/a importante" | ✅ Positivo |
| Nmexist1_5 | "Mi sono sentito/a utile" | ✅ Positivo |

### Controllo (Nctrl1_1 → Nctrl1_5)
| **Colonna** | **Interpretazione** | **Polarità** |
|-------------|-------------------|--------------|
| Nctrl1_1 | "Mi sono sentito/a potente" | ✅ Positivo |
| Nctrl1_2 | "Ho sentito di avere controllo sul corso dell'interazione" | ✅ Positivo |
| Nctrl1_3 | "Ho sentito di avere capacità di influenzare significativamente" | ✅ Positivo |
| Nctrl1_4 | "Ho sentito di non riuscire a influenzare le azioni degli altri" | ❌ Negativo |
| Nctrl1_5 | "Ho sentito che le altre persone del gruppo decidevano tutto" | ❌ Negativo |

### Umore (Mood1_1 → Mood1_8)
| **Colonna** | **Interpretazione** | **Polarità** |
|-------------|-------------------|--------------|
| Mood1_1 | "Buono" | ✅ Positivo |
| Mood1_2 | "Cattivo" | ❌ Negativo |
| Mood1_3 | "Amichevole" | ✅ Positivo |
| Mood1_4 | "Ostile" | ❌ Negativo |
| Mood1_5 | "Arrabbiato" | ❌ Negativo |
| Mood1_6 | "Piacevole" | ✅ Positivo |
| Mood1_7 | "Felice" | ✅ Positivo |
| Mood1_8 | "Triste" | ❌ Negativo |

---

## 🔍 Domande di Controllo e Percezioni

| **Colonna** | **Interpretazione** | **Opzioni Risposta** |
|-------------|-------------------|---------------------|
| Check1 | Riuscito a vedere avatar e descrizioni altri | Sì / No |
| Check2 | Riuscito a mettere "mi piace" e vedere like | Sì / No |
| Q26_1 | "Sono stato/a ignorato/a" | 1-5 (Per niente → Moltissimo) |
| Q26_2 | "Sono stato/a escluso/a" | 1-5 (Per niente → Moltissimo) |
| Q26_3 | "Agli altri è piaciuta la mia descrizione" | 1-5 (Per niente → Moltissimo) |
| Q28 | Valutazione like ricevuti vs media (~5) | Sotto la media / Nella media / Sopra la media |

---


*Versione 4.0 - Aggiornato Agosto 2025*  
*emiliano.pes@uniroma1.it*
