# Familie-Majoren

Familie-Majoren er familiens årlige golfmesterskap, som en app på telefonen. Den følger charteret: mesteren kåres etter Familiemajor-poeng, ikke etter samlet slagscore.

Appen er én nettside. Den ligger på GitHub Pages. Alle som har lenken og familiekoden, ser de samme turneringene, resultatene og bildene.

Versjon nå: **1.33**

## Slik fungerer den for familien

Nederst er fem knapper.

| Knapp | Hva den gjør |
|---|---|
| Hjem | Nedtelling, pågående turnering og mottoet |
| Turnering | Dager, scorekort og resultater |
| Stilling | Sammenlagt mens en turnering pågår og minst én dag er fullført |
| Historikk | Kommer i stedet for Stilling når ingen runde er i gang |
| Media | Bilder, sortert på år og dag |
| Mer | Historikk, Hall of Fame, charter og innstillinger |

En turnering opprettes med sted, startdato og sluttdato. Året settes ut fra datoene. Spillere, handicap og format kan fylles inn senere, under **Turneringsinnstillinger**. De låses når første resultat er lagret.

Hver dag har et format:

- Individuell Stableford
- Ryder Cup Fourball
- Akkumulert Scramble
- Ryder Cup Singler
- Finalerunden, med doble poeng

Admin forbereder scorekortet om morgenen: bane, par, hullindex og tildelte slag. Spillerne fører selv. På hull 18 kan alle trykke **Fullfør runde**. Det lukker bare kortet og åpner Stilling. Runden er ikke avsluttet.

Bare admin avslutter runden. Da deles Familiemajor-poengene ut, og lunsjregelen vises. Er ikke alle ført opp, kommer det et spørsmål først. Admin kan låse opp kortet igjen.

Når året er ferdig, trykker admin **Turnering ferdig**. Den flyttes til historikk og kan ikke endres. En enkelt turnering kan slettes uten å tømme alt annet.

## Admin og alle andre

Familiekoden er nøkkelen. Den skrives inn én gang per telefon. Uten den ser telefonen bare sine egne data, og de deles ikke.

Admin låses opp med en kode under **Mer → Innstillinger**. Da kan du:

- opprette og endre turneringen før første resultat
- forberede scorekort og generere kamper
- avslutte og låse opp en runde
- slette en turnering
- koble Google Foto
- eksportere en sikkerhetskopi

Andre kan føre sine egne slag, se stillingen, historikken, charteret og bildene. De kan ikke endre andres kort.

## Bilder

Bildene lagres i Google Foto, i ett album per år: `Familiemajoren 2027`. Appen sorterer dem på dag. Google-koblingen settes opp én gang under Innstillinger. Hemmeligheten lagres i skyen, ikke i denne mappen.

Sletter du et bilde i appen, slettes det ikke automatisk hos Google. Sletter du det hos Google, forsvinner det i appen når listen hentes på nytt. Selve bildefilen blir ikke liggende i GitHub.

## Filer i denne mappen

Dette er hele appen. Ikke legg inn andre mapper.

| Fil | Hva den er |
|---|---|
| `index.html` | Hele appen: sider, regler, regnestykker og charter |
| `sw.js` | Gjør at telefonen husker siden, og at en ny versjon faktisk lastes |
| `manifest.webmanifest` | Navnet **Familie-Majoren** og ikonene når appen legges på hjemskjermen |
| `icon-192.png` og `icon-512.png` | Appikonet |
| `apple-touch-icon.png` | Ikonet på iPhone |
| `banner.jpg` | Bildet øverst på Hjem |
| `README.md` | Denne instruksen |

`index.html` må hete akkurat det, ellers viser ikke GitHub Pages siden.

## Slik oppdaterer du appen

1. Ta en kopi av den gamle `index.html` før du bytter den.
2. Last opp den nye `index.html`.
3. Last opp den nye `sw.js` i samme omgang. Versjonsnavnet inni filen, `familiemajoren-v37`, må være et nytt tall. Ellers kan telefonen vise den gamle appen.
4. Vent til GitHub Pages er ferdig. Det tar ofte ett minutt.
5. Lukk siden helt og åpne lenken på nytt.
6. Gå til **Mer → Innstillinger**. Der skal det stå den nye versjonen, nå **Versjon 1.33**.

Bytter du bare bildet eller ikonet, last opp den filen og øk tallet i `sw.js` likevel. Ellers kan den gamle utgaven bli hengende.

Ikonet på hjemskjermen oppdateres ikke alltid av seg selv. Da fjerner du snarveien og legger den til på nytt.

## Hvor du endrer vanlige ting

Alt som skal endres i appen, ligger i `index.html`. Åpne den i en teksteditor. Ikke i Word.

| Du vil endre | Søk etter |
|---|---|
| Versjonen som vises i appen | `Versjon 1.33` |
| Kortversjonen av charteret | `const CHARTER` |
| Det fulle charteret | `charter-full-data` |
| Mottoet | `Ett år som mester` |
| Appnavnet på hjemskjermen | `manifest.webmanifest`, feltene `name` og `short_name` |
| Hjem-bildet | bytt ut `banner.jpg`, behold filnavnet |
| Ikonet | bytt ut de tre ikonfilene, behold filnavnene |
| Sky-adressen | `const CLOUD_URL` |

Kortversjonen er en liste med titler og tekst. En tabell skrives slik, med overskrift først og én rad per linje:

```text
table: [['Plass', 'Poeng'], ['1', '6'], ['2', '5']]
```

Det fulle charteret er ett langt avsnitt nederst i filen. Ikke klipp i det med mindre du bytter hele dokumentet. En ny Word-fil oppdaterer ikke appen av seg selv. Teksten må legges inn i `index.html`.

Poeng, tiebreak og de fem formatene regnes ut i funksjonene `calculateStandings`, `awardFromCard` og `saveScoring`. Endre dem bare hvis charteret er endret, og test med en turnering du kan slette etterpå.

## Søk opp bane

På **Forbered scorekort** kan admin trykke **Søk opp bane**. Søket går i familiens egen banebok, ikke i en ekstern database. Finnes ikke banen, trykker du **Opprett bane** og fyller inn klubb, bane, tee, slope og baneverdi for herrer og damer, pluss par og HCP. Tom slope er lov og kan fylles inn senere med **Oppdater**. **Bytt om** under slope bytter tallene med baneverdi hvis de ble skrevet i feil felt. Hullene lagres på banen. En tee som fortsatt er tom, kan arve hullene fra en tee som er fylt ut.

Kjønn velges bare under turneringsinnstillinger, ved siden av navn og handicap. Når banen brukes, spør appen om alle spiller fra samme tee. Slag regnes ut fra spillerens handicap og riktig slope. Mangler slope, står slagene tomme.

Den gamle Supabase-funksjonen `golf-course` brukes ikke lenger. Den og secret-en `GOLF_API_KEY` kan slettes. Ikke slett `google-photo`.

På turneringssiden ser spillerne dagene og stillingen. Turneringsinnstillinger, gruppegenerator, slett og «Marker som ferdig» vises bare for admin. **Publiser dagen** gjør at spillerne får **Før resultat**, og scorekortet hvis det er klart. **Avslutt dagen** og **Avslutt runden** skjuler føringen igjen. Scorene blir liggende, og dagen kan publiseres på nytt.

## Skyen

Turneringen, spillerne, scorene og Hall of Fame ligger i Supabase, i ett dokument per familiekode. Adressen står i `CLOUD_URL`.

Telefonen lagrer også en kopi hos seg selv. Mister den kontakt, kan du fortsatt se det siste. Nye resultater deles igjen når kontakten er tilbake.

Under **Innstillinger** kan du eksportere alt til en JSON-fil, og importere den igjen. Ta en slik kopi før en stor endring.

**Nullstill all data** tømmer turnering, historikk og Hall of Fame for hele familien. Den sletter ikke bildene i Google Foto.

To telefoner som lagrer i samme sekund, kan i sjeldne tilfeller overskrive hverandre på et scramble-hull. Slagene til hver spiller er beskyttet. Skjer det, fører du hullet på nytt.

## Det som ikke skal inn i GitHub

- Familiekoden
- Admin-koden
- Google Client secret
- Supabase secret key, den som ikke er den offentlige nøkkelen

De skrives inn i appen eller ligger i Supabase. De skal ikke stå i denne filen.
