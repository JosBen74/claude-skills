---
name: osint
description: OSINT-sökning och informationsinhämtning från öppna källor för Länsstyrelsen VG
auto_activation: false
activation_keywords: [osint, omvärldsbevakning, informationsinhämtning, källsökning, bevaka, nyhetssökning, mediebevakning]
integrates_with: [analysis-report, osint-bevakning, n8n-workflow-patterns]
---

# Skill: osint

## Syfte

Systematisk informationsinhämtning och omvärldsbevakning från öppna källor (OSINT).
Täcker myndigheter, riksdag, EU, akademi, media och nyheter — med källkritik inbyggd i varje steg.

## Stödfiler

- **Källkatalog** (myndigheter, media, EU, öppen data): se `KALLOR.md`
- **Källkritikram** (bedömning, flaggning, konfidensgradering): se `KALLKRITIK.md`
- **Sökmönster och operatorer** (Google, Bing, site:-sökning, RSS): se `SOKMALLAR.md`

## Aktiveras när

Användaren vill:
- Bevaka ett ämne, aktör eller händelse
- Söka bakgrundsinformation om en organisation, person eller fråga
- Ta fram underlag om ett specifikt beslut, rapport eller uttalande
- Följa nyheter inom civilt försvar, regional utveckling eller annan LST-relevant domän
- Bygga en n8n-bevakning för löpande informationsinhämtning

---

## Workflow (steg-för-steg)

### Steg 1 — Klargör uppdraget

Ställ max 3 frågor om dessa är oklara:

1. **Vad** ska bevakas? (ämne, händelse, aktör, beslut)
2. **Varför** — hur ska informationen användas? (bakgrundsanalys, löpande bevakning, beslutsunderlag)
3. **Tidshorisont** — engångssökning eller löpande bevakning?

### Steg 2 — Välj källnivå

| Nivå | Passar för | Källor |
|------|-----------|--------|
| **Snabb** | Aktuell händelse, vad händer nu | Nyhetsmedier, myndighetsnyheter |
| **Djup** | Bakgrundsanalys, utredning | Myndighetsrapporter, riksdag, akademi |
| **Löpande** | Bevakning över tid | RSS, n8n-workflow, Kolada-trend |

### Steg 3 — Källsökning (i prioritetsordning)

1. **Primärkällor** (myndigheter, riksdag, EU): se KALLOR.md → sektion Myndigheter
2. **Nyhets- och mediekällor**: se KALLOR.md → sektion Media
3. **Akademiska och grå källor**: se KALLOR.md → sektion Akademi & Öppen data
4. **Webb-sökning** med sökmönster: se SOKMALLAR.md

Använd WebSearch och WebFetch för sökning och läsning.
Använd MCP-verktyg (Riksdag, Kolada, VISS) när de passar bättre.

### Steg 4 — Källkritisk bedömning

För varje källa, bedöm enligt KALLKRITIK.md:
- Ursprung och avsändare
- Aktualitet (datum, version)
- Syfte och eventuell bias
- Konfidensgradering (HÖG / MEDEL / LÅG)

### Steg 5 — Strukturera fynd

Presentera alltid med:

```
## Fynd: [ämne] — [datum ÅÅÅÅ-MM-DD]

### Sammanfattning
[2–4 meningar. Vad är det viktigaste fyndet?]

### Fynd
| # | Fynd | Källa | Datum | Konfidens |
|---|------|-------|-------|-----------|
| 1 | ... | [URL] | ÅÅÅÅ-MM-DD | HÖG |
| 2 | ... | [URL] | ÅÅÅÅ-MM-DD | MEDEL |

### Osäkerheter
- [Vad är oklart eller obekräftat]
- [Motstridiga uppgifter om finns]

### Rekommenderade nästa steg
- [Fördjupa: vilken källa/sökning]
- [Bevaka: vad och var]

---
Sökt: [ÅÅÅÅ-MM-DD HH:MM]  Källor: [antal]  Metod: [WebSearch / MCP / RSS]
```

### Steg 6 — Löpande bevakning (valfritt)

Om användaren vill ha löpande bevakning:
- Föreslå n8n-workflow med RSS-noder (se KALLOR.md → RSS-flöden)
- Hänvisa till `n8n-workflow-patterns`-skill för implementation
- Dokumentera vilka källor och söktermer som används

---

## Constraints (hårda regler)

- ALDRIG presentera information utan källhänvisning med URL och datum
- ALDRIG spekulera om fakta — markera explicit om något är osäkert eller obekräftat
- ALDRIG fabricera citat, siffror eller dokument
- ALDRIG utelämna motstridiga uppgifter om de finns
- ALLTID tidsstämpla varje sökning (datum + tid)
- ALLTID ange konfidensgradering för varje fynd
- ALLTID skilja på primärkälla och andrahandskälla
- Om en källa är partisk eller har tydligt intresse: flagga det explicit

## Kvalitetschecklista

Innan leverans:

- [ ] Alla fynd har URL + datum
- [ ] Konfidensgradering angiven för varje fynd
- [ ] Primär- och andrahandskällor är åtskiljda
- [ ] Osäkerheter explicit redovisade
- [ ] Söktidpunkt angiven
- [ ] Inga fabricerade citat eller siffror
- [ ] Motstridiga uppgifter är noterade om de finns
