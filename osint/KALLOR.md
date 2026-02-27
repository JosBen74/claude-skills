# OSINT Källkatalog

Organiserad efter källtyp. Prioritera primärkällor. Verifiera alltid med KALLKRITIK.md.

---

## Svenska myndigheter

### Länsstyrelsen och regionala myndigheter
| Källa | URL | RSS | Vad |
|-------|-----|-----|-----|
| LST VG | `https://www.lansstyrelsen.se/vastra-gotaland` | Nej | Beslut, rapporter, nyheter |
| Västra Götalandsregionen | `https://www.vgregion.se` | Nej | Regional hälsa, kultur, trafik |
| Länsstyrelsernas gemensamma | `https://www.lansstyrelsen.se` | Nej | Nationella ärenden |

### Nationella beredskapsmyndigheter
| Källa | URL | RSS | Vad |
|-------|-----|-----|-----|
| MSB | `https://www.msb.se` | Ja | Krisberedskap, publikationer |
| Försvarsmakten | `https://www.forsvarsmakten.se` | Ja | Militär lägesbild, nyheter |
| FOI | `https://www.foi.se` | Ja | Försvarsforskningsrapporter |
| MUST (öppen del) | `https://www.forsvarsmakten.se/sv/organisation/militara-underrattelse-och-sakerhetstjansten-must/` | Nej | Öppna hotbedömningar |
| SÄPO | `https://www.sapo.se` | Nej | Säkerhetspolitisk information |
| Energimyndigheten | `https://www.energimyndigheten.se` | Ja | Energiberedskap, statistik |
| PTS | `https://www.pts.se` | Ja | Digital infrastruktur, cybersäkerhet |
| Livsmedelsverket | `https://www.livsmedelsverket.se` | Ja | Livsmedelsberedskap |
| Socialstyrelsen | `https://www.socialstyrelsen.se` | Ja | Hälso- och sjukvårdsberedskap |
| Transportstyrelsen | `https://www.transportstyrelsen.se` | Nej | Transportinfrastruktur |

### Riksdag och regering
| Källa | MCP-verktyg | Vad |
|-------|-------------|-----|
| Riksdagen | `search_dokument`, `search_anforanden` | Propositioner, motioner, anföranden |
| Regeringskansliet | `search_regering`, `get_propositioner` | Regleringsbrev, direktiv, propositioner |
| SOU / Ds | `search_dokument` (typ: SOU) | Statliga utredningar |

> Använd MCP-verktyget `Riksdag och regering` för dessa — snabbare och mer strukturerat än webssökning.

### Statistik och öppen data
| Källa | URL / Verktyg | Vad |
|-------|--------------|-----|
| SCB | PxWebApi 2.0 (se MEMORY.md) | Befolkning, näringsliv, ekonomi |
| Kolada | MCP `kolada-mcp` | Kommunala nyckeltal, KPI-trender |
| Jordbruksverket | `https://jordbruksverket.se` | Lantbruk, landsbygd |
| Boverket | `https://www.boverket.se` | Samhällsplanering, bostäder |
| Havs- och vattenmyndigheten | `https://www.havochvatten.se` | Vattenförekomster (+ VISS MCP) |
| VISS | MCP `viss-mcp` | Vattenförekomster, MKN |
| Naturvårdsverket | `https://www.naturvardsverket.se` | Miljödata, klimat |
| Riksantikvarieämbetet | `https://www.raa.se` | Kulturmiljö, fornlämningar |

---

## EU och internationellt

### EU-institutioner
| Källa | URL | Vad |
|-------|-----|-----|
| EUR-Lex | `https://eur-lex.europa.eu` | EU-lagstiftning, förordningar, direktiv |
| European Commission | `https://ec.europa.eu` | EU-politik, initiativ |
| ENISA | `https://www.enisa.europa.eu` | EU cybersäkerhet |
| EEA (European Environment Agency) | `https://www.eea.europa.eu` | Miljödata Europa |
| Eurostat | `https://ec.europa.eu/eurostat` | EU-statistik |
| EU Civil Protection | `https://civil-protection-humanitarian-aid.ec.europa.eu` | Katastrofskydd, beredskap |

### NATO och säkerhetspolitik
| Källa | URL | Vad |
|-------|-----|-----|
| NATO | `https://www.nato.int` | Officiella uttalanden, rapporter |
| IISS | `https://www.iiss.org` | Säkerhetspolitisk analys (betald men sammanfattningar fria) |
| SIPRI | `https://www.sipri.org` | Fredsforskningsinstitut, rustningsdata |
| Hybrid CoE (Helsingfors) | `https://www.hybridcoe.fi` | Hybridhot, analys |

---

## Nyhetsmedier och press

### Svenska riksmedier (primär)
| Källa | URL | RSS |
|-------|-----|-----|
| SVT Nyheter | `https://www.svt.se/nyheter` | Ja — `https://www.svt.se/nyheter/rss.xml` |
| SR (Sveriges Radio) | `https://sverigesradio.se` | Ja |
| TT Nyhetsbyrån | `https://tt.se` | Nej (prenumeration) |
| DN (Dagens Nyheter) | `https://www.dn.se` | Ja (begränsat) |
| SvD (Svenska Dagbladet) | `https://www.svd.se` | Ja (begränsat) |
| Expressen | `https://www.expressen.se` | Ja |
| Aftonbladet | `https://www.aftonbladet.se` | Ja |
| Göteborgs-Posten | `https://www.gp.se` | Ja |

### Västra Götaland (regional)
| Källa | URL | RSS |
|-------|-----|-----|
| Göteborgs-Posten | `https://www.gp.se` | Ja |
| Bohusläningen | `https://www.bohuslaningen.se` | Ja |
| Skaraborgs Allehanda | `https://www.sla.se` | Ja |
| Alekuriren | `https://www.alekuriren.se` | Nej |
| Ttela (Trollhättan/Vänersborg) | `https://www.ttela.se` | Ja |
| Strömstads Tidning | `https://www.stromstadstidning.se` | Nej |
| Västnytt (SVT) | `https://www.svt.se/nyheter/lokalt/vast` | Ja |

### Fackpress och specialiserade
| Källa | URL | Domän |
|-------|-----|-------|
| Altinget Sverige | `https://www.altinget.se` | Politik, myndigheter |
| Riksdag & Departement | `https://rod.se` | Offentlig sektor |
| Ny Teknik | `https://www.nyteknik.se` | Teknik, innovation |
| Computer Sweden | `https://computersweden.idg.se` | IT, cyber |
| Miljöaktuellt | `https://miljoaktuellt.se` | Miljö, hållbarhet |
| Lag & Avtal | `https://www.lag-avtal.se` | Juridik, arbetsrätt |
| Säkerhetspolisen / SäkerhetsNytt | `https://sakerhetsnytt.se` | Säkerhet, beredskap |

### Internationella nyhetskällor
| Källa | URL | Styrka |
|-------|-----|--------|
| Reuters | `https://www.reuters.com` | Faktabaserad nyhetsbyrå |
| AP News | `https://apnews.com` | Faktabaserad nyhetsbyrå |
| BBC | `https://www.bbc.com/news` | Bred täckning, pålitlig |
| The Guardian | `https://www.theguardian.com` | Europa/politik |
| Politico Europe | `https://www.politico.eu` | EU-politik |
| Defense News | `https://www.defensenews.com` | Försvar och säkerhet |
| Kyiv Independent | `https://kyivindependent.com` | Ukraina/Ryssland (verifiera mot andra) |

---

## Akademi och grå litteratur

| Källa | URL | Vad |
|-------|-----|-----|
| DiVA (universitetsuppsatser) | `https://www.diva-portal.org` | Akademiska avhandlingar och uppsatser |
| SwePub | `https://swepub.kb.se` | Svenska vetenskapliga publikationer |
| Google Scholar | `https://scholar.google.com` | Bred akademisk sökning |
| OECD iLibrary | `https://www.oecd-ilibrary.org` | Internationell statistik och analys |
| Världsbanken | `https://data.worldbank.org` | Globala utvecklingsindikatorer |
| ECDC | `https://www.ecdc.europa.eu` | Smittskydd Europa |

---

## RSS-flöden för n8n-bevakning

Direkt användbara RSS-URLs för n8n HTTP-noder:

```
MSB nyheter:          https://www.msb.se/sv/rss/nyheter/
FOI nyheter:          https://www.foi.se/rss
Energimyndigheten:    https://www.energimyndigheten.se/rss/nyheter/
PTS nyheter:          https://www.pts.se/sv/om-pts/press/nyheter/rss/
SVT Nyheter:          https://www.svt.se/nyheter/rss.xml
SVT Västnytt:         https://www.svt.se/nyheter/lokalt/vast/rss/
GP nyheter:           https://www.gp.se/rss
Riksdagen (nyheter):  https://www.riksdagen.se/sv/rss/?type=nyheter
```

> Notering: RSS-URL:er förändras. Verifiera med WebFetch om ett flöde slutar fungera.
