# Källkritikram för OSINT

Använd denna mall för att bedöma varje källa och fynd systematiskt.

---

## Bedömningsmodell — fyra dimensioner

### 1. Ursprung (Vem är avsändaren?)

| Poäng | Kriterie |
|-------|---------|
| **HÖG** | Statlig myndighet, riksdagen, EU-institution, etablerad nyhetsbyrå (TT, Reuters, AP) |
| **MEDEL** | Etablerat nyhetsmedium (DN, SVT, BBC), erkänd NGO, akademisk institution |
| **LÅG** | Okänd webbplats, anonym blogg, sociala medier utan verifiering |
| **FLAGGA** | Känd desinformationskälla, tydlig partisk agenda, anonym källa |

### 2. Aktualitet (När publicerades det?)

| Poäng | Kriterie |
|-------|---------|
| **HÖG** | Publicerad inom 30 dagar, eller tidlös faktakälla (lagtext, statistikdatabas) |
| **MEDEL** | Publicerad inom 1 år |
| **LÅG** | Äldre än 1 år — verifiera om information fortfarande gäller |
| **FLAGGA** | Inget datum angivet, eller datum verkar manipulerat |

### 3. Syfte och bias (Varför publicerades det?)

| Poäng | Kriterie |
|-------|---------|
| **HÖG** | Informationssyfte, faktabaserad redovisning, myndighetskommunikation |
| **MEDEL** | Journalistisk granskning, opinionsbildning med transparenta utgångspunkter |
| **LÅG** | Marknadsföring, partspolitik, påverkanskampanj |
| **FLAGGA** | Dold avsändare, avsiktlig vilseledning, emotionell manipulation |

### 4. Verifierbarhet (Kan det bekräftas?)

| Poäng | Kriterie |
|-------|---------|
| **HÖG** | Bekräftat av ≥2 oberoende primärkällor |
| **MEDEL** | En primärkälla, eller bekräftat av etablerat medium |
| **LÅG** | Ej bekräftat, enstaka andrahandskälla |
| **FLAGGA** | Obekräftbart, inga källhänvisningar, eller motbevisat av primärkälla |

---

## Sammantagen konfidensgradering

| Gradering | Innebär |
|-----------|---------|
| **HÖG** | Minst 3 av 4 dimensioner HÖG, inga FLAGGA |
| **MEDEL** | Blandning av HÖG och MEDEL, inga FLAGGA |
| **LÅG** | En eller flera LÅG, men inga FLAGGA — notera osäkerheten |
| **FLAGGA ⚠️** | Minst en FLAGGA — redovisa och luta dig INTE på denna källa |

---

## Varningssignaler att alltid flagga

- **Anonym avsändare** utan redaktionell garanti
- **Saknar datum** eller datum ändrades utan notering
- **Citat utan kontext** — kontrollera original
- **Extremt laddade rubriker** som inte speglar innehållet
- **Statistik utan källa** — var kommer siffran ifrån?
- **Bild utan kontext** — verifiera med Google/TinEye bildssökning
- **Känslomässig appell** ersätter faktaargument
- **Bekräftelsecirklar** — källa A citerar källa B som citerar källa A

---

## Hybridhot och desinformation (civilt försvar)

Extra försiktighet vid:
- Information om militära rörelser, beredskapsläge, infrastrukturincidenter
- Rykten om svenska myndigheter eller beslut som inte bekräftats officielt
- Innehåll som sprids snabbt utan verifierbar ursprungskälla
- Påstådda insideruppgifter utan dokumentation

> Regel: Vid tveksamhet kring känslig information — verifiera mot officiell källa eller avvakta.
> Ange alltid "OBEKRÄFTAT" i fyndsammanfattningen om verifiering saknas.

---

## Snabbmall för källbedömning

Kopiera och fyll i för varje källa:

```
Källa:        [URL]
Publicerad:   [datum]
Avsändare:    [organisation/person]
Ursprung:     HÖG / MEDEL / LÅG / FLAGGA
Aktualitet:   HÖG / MEDEL / LÅG / FLAGGA
Syfte/bias:   HÖG / MEDEL / LÅG / FLAGGA
Verifierbar:  HÖG / MEDEL / LÅG / FLAGGA — [bekräftat av: ...]
Konfidens:    HÖG / MEDEL / LÅG / FLAGGA ⚠️
Notering:     [Ev. caveats, bias, motstridiga uppgifter]
```
