# prorespektera-assets

Publika varumärkesfiler för Prorespektera. Repot finns för att byggverktyg
ska kunna hämta filerna direkt, utan inloggning — därför är det publikt.

## Vad som får ligga här

Endast material som redan är publikt i praktiken: logotyper, ikoner och
grafiska element som syns på prorespektera.se eller i utskickat material.

**Följande får aldrig läggas här:** kunddokument, offerter, prislistor,
filer med personuppgifter, interna underlag eller något som rör en enskild
kund. Det hör hemma i `prorespektera-web` (privat) eller i OneDrive.

## Filer

| Fil | Mått | Används till |
|---|---|---|
| `Pro vit logga smal.png` | 2739 × 432 px, RGBA | Vit ordbild med korallhjärta. **Kräver mörk bakgrund** — lägg den aldrig direkt på vitt |
| `markning-90-konto.png` | 179 × 47 px, RGBA | 90-konto – Svensk Insamlingskontroll. Vit bakgrund i filen. Liten upplösning; visa högst ca 50 px hög |
| `markning-giva-sverige.png` | 154 × 88 px, RGBA | Tryggt givande – Giva Sverige. Skalad till dubbel visningshöjd (44 px) |

Prorespektera-loggans proportioner är 6,34:1. Äldre kod räknar med
720 × 114 (6,32:1) från en tidigare variant; skillnaden är liten men sätt
alltid höjden utifrån filens egna mått i stället för en hårdkodad kvot.

### Märkningsloggorna

Märkningsloggorna är Svensk Insamlingskontrolls och Giva Sveriges märken
(fått av CAF 8 okt 2026). De får bara visas för en organisation som faktiskt
har märkningen. På Propagos kampanjsidor styrs det av tabellen
`organisation_markningar` i gaming-databasen, inte av handskrivna listor.

## Hämta i ett bygge

```bash
curl -sL -o logo.png \
  "https://raw.githubusercontent.com/Increvendi/prorespektera-assets/main/Pro%20vit%20logga%20smal.png"
```

Filnamnet innehåller mellanslag och måste därför URL-kodas som `%20`.

## Färger och typsnitt

Navy `#143446`, korall `#E65A5A`, kräm `#F7F1EB`, grå `#6B7A83`,
ljusgrå `#DDE3E6`. Poppins i rubriker, Inter i brödtext — båda hämtas från
Fontsource via npm, se `verktyg/offertmallar/hamta-typsnitt.sh` i
`prorespektera-web`.
