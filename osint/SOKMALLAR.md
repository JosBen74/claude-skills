# Sökmönster och operatorer för OSINT

---

## Google/Bing — avancerade operatorer

### Grundoperatorer

| Operator | Syntax | Exempel |
|----------|--------|---------|
| Exakt fras | `"..."` | `"civilt försvar" "Västra Götaland"` |
| Site-sökning | `site:` | `site:msb.se cybersäkerhet 2025` |
| Filtyp | `filetype:` | `filetype:pdf "risk- och sårbarhetsanalys"` |
| Uteslut | `-` | `beredskap -försäkring` |
| ELLER | `OR` | `"hybridhot" OR "påverkanskampanj"` |
| Inom titel | `intitle:` | `intitle:"regleringsbrev 2026"` |
| Datumfilter | `after:` / `before:` | `MSB rapport after:2025-01-01` |
| Wildcard | `*` | `"länsstyrelsen * beslut"` |

### Sammansatta sökmönster

```
# Myndighetsdokument om ett ämne
site:gov.se OR site:msb.se OR site:foi.se "energiberedskap" filetype:pdf after:2024-01-01

# Regional nyhetsbevakning
"Västra Götaland" ("civilt försvar" OR "krisövning" OR "beredskap") site:svt.se OR site:gp.se

# EU-lagstiftning på svenska
site:eur-lex.europa.eu "kritisk infrastruktur" lang:sv after:2024-01-01

# Riksdagsdokument
site:riksdagen.se "totalförsvar" filetype:pdf after:2025-01-01

# Akademisk sökning
site:diva-portal.org OR site:swepub.kb.se "krisberedskap" "Västsverige"

# Pressmeddelanden myndigheter
"pressmeddelande" site:lansstyrelsen.se "Västra Götaland" after:2025-01-01
```

---

## MCP-verktyg — sökmönster

### Riksdag och regering

```
# Propositioner om ett ämne (senaste)
get_propositioner → filtrera på nyckelord

# Anföranden om totalförsvar (senaste riksmötet)
search_anforanden: {"sok": "totalförsvar", "rm": "2024/25"}

# Sök dokument (SOU, propositioner, motioner)
search_dokument: {"sok": "civilt försvar", "doktyp": "prop", "from": "2024-01-01"}

# Sök i fulltexten
search_dokument_fulltext: {"sok": "hybridhot energiinfrastruktur"}

# Voteringar om ett ämne
search_voteringar: {"rm": "2024/25", "sok": "beredskapslag"}
```

### Kolada (kommunala KPI:er)

```
# Sök KPI-nyckeltal
search_kpis: {"query": "befolkning"}

# Hämta trend för en kommun
get_kpi_trend: {"kpi_id": "N00945", "municipality_id": "1480", "years": 5}

# Jämför kommuner i VG
compare_municipalities: {"kpi_id": "N00945", "municipality_ids": ["1480","1481","1482"]}
```

### VISS (vattenförekomster)

```
# Sök vattenförekomst
search_waterbody: {"name": "Göta älv"}

# Hämta MKN-status
get_environmental_quality_standard: {"waterbody_id": "..."}
```

---

## Nyhetssökning — strategier

### Snabb medieöversikt (daglig bevakning)

1. Sök med WebSearch: `[ämne] site:svt.se OR site:dn.se OR site:gp.se`
2. Komplettera med: `[ämne] site:msb.se OR site:forsvarsmakten.se`
3. Internationellt: `[ämne] site:reuters.com OR site:apnews.com`

### Djupare medieanalys

```
# Hitta alla artiklar om ett ämne senaste månaden
"[ämne]" after:2026-01-27 before:2026-02-27

# Jämför rapportering — sök samma ämne på flera medier
"[ämne]" site:svt.se
"[ämne]" site:gp.se
"[ämne]" site:aftonbladet.se

# Hitta ursprungsartikel (undvik vidarecitering)
"[citat eller rubrik]" → identifiera äldsta träff = trolig ursprungskälla
```

### Verifiering av påstående

```
Steg 1: Sök påståendet exakt inom citationstecken
Steg 2: Identifiera primärkälla (ej andrahandscitat)
Steg 3: Sök: [påstående] "falskt" OR "felaktigt" OR "dementi"
Steg 4: Kolla faktakollektivet: site:faktisk.no OR site:snopes.com
```

---

## Personssökning (offentliga roller)

> Använd **enbart** för offentliga personer i deras offentliga roll. Aldrig för privatpersoner.

```
# Offentlig tjänsteman / politiker
"[Namn]" site:riksdagen.se
"[Namn]" site:lansstyrelsen.se
"[Namn]" "landshövding" OR "länsöverdirektör"

# Uttalanden och anföranden
"[Namn]" anförande site:riksdagen.se
"[Namn]" "pressmeddelande" after:2025-01-01
```

---

## RSS-prenumeration och löpande bevakning

### Manuell RSS-läsning (WebFetch)

```python
# Hämta RSS-flöde och extrahera senaste artiklar
WebFetch("https://www.msb.se/sv/rss/nyheter/", "Lista de 5 senaste artiklarna med titel, datum och URL")
```

### n8n-bevakningsmönster

För löpande bevakning — bygg n8n-workflow med:
- **RSS Feed Trigger** (schema: varje timme eller dagligen)
- **HTTP Request** mot RSS-URL (se KALLOR.md → RSS-flöden)
- **Filter** på nyckelord i titel/beskrivning
- **Merge** om flera källor
- **Email/Slack/Notion** som output

> Se `n8n-workflow-patterns`-skill för implementationshjälp.

---

## Domänspecifika söktips

### Civilt försvar och säkerhet

```
site:foi.se filetype:pdf after:2024-01-01
site:msb.se "totalförsvar" filetype:pdf
"höjd beredskap" site:riksdagen.se OR site:regeringen.se
hybridhot site:hybridcoe.fi OR site:nato.int
```

### Regional planering och miljö

```
site:lansstyrelsen.se "Västra Götaland" "detaljplan" OR "översiktsplan"
site:vgregion.se "regional utveckling" filetype:pdf
"Västra Götaland" site:naturvardsverket.se OR site:havochvatten.se
VISS MCP: search_waterbody + get_status_classification
```

### EU och lagstiftning

```
site:eur-lex.europa.eu "[direktiv/förordning]" lang:sv
"NIS2" OR "CER-direktivet" site:pts.se OR site:msb.se
Riksdag MCP: search_dokument → EU-propositioner
```

### Ekonomi och näringsliv

```
SCB PxWebApi: TAB638 (befolkning), RAMS (företag)
Kolada: search_kpis → kommunala nyckeltal
site:tillvaxtverket.se "Västra Götaland" filetype:pdf
```
