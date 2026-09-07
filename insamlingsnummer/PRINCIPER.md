# Insamlingsnummer — principer

## Vad det här är

Ett publikt register över de telefonnummer som svenska insamlingsorganisationer använder för
utgående insamlingssamtal (90-konto är ett verifieringsmärke, inte ett inträdeskrav). Tjänsten säljs som tilläggstjänst till ett
telemarketingbolags egna uppdragsgivare.

Användaren är en privatperson som just blivit uppringd av ett okänt nummer och undrar om det är ett
bedrägeri. Allt på sidorna ska besvara den frågan, snabbt och kontrollerbart.

## Den enda strategin som betyder något

Vi kommer inte att ranka etta på "vem ringde" — Hitta.se, Eniro och Merinfo äger de sökorden.
Vi ska i stället vara **den källa AI-svaret hämtar uppgiften ur** för ett specifikt nummer.
Det urvalet fungerar annorlunda, och de skillnaderna styr all kod i repot:

1. **Hämtning sker på styckenivå, inte sidnivå.** Enheten som konkurrerar är ett stycke på
   130–170 ord. Därför genererar `src/lib/passage.ts` en självbärande svarspassage som ligger först
   på varje nummersida.
2. **Passagen lyfts ur sin kontext.** Den får därför aldrig innehålla "organisationen", "numret",
   "som nämnts ovan" eller andra bakåtreferenser. Skriv alltid ut organisationsnamn och nummer.
3. **Frågan delas i 5–11 delfrågor.** Därför är nummersidan uppbyggd av frågeformulerade H2-block
   som var för sig besvarar en gren: vem ringde, är det bedrägeri, varför ringde de, hur vet jag att
   det är äkta, hur slipper jag samtalen.
4. **Samstämmighet mellan oberoende källor höjer tilliten.** Därför måste organisationens namn,
   organisationsnummer och 90-konto vara ordagrant identiska med organisationens egen webbplats och
   registren. Ändra aldrig stavning eller ordföljd i ett organisationsnamn.
5. **Det finns tak för hur mycket som hämtas per domän.** Vår fördel är att vara den enda sidan med
   ett faktiskt svar för just det numret.

## Regler som inte får brytas

- **Utgångna nummer raderas aldrig.** Sidan ligger kvar och visar när numret togs ur bruk. Ett
  återlämnat nummer kan tilldelas någon annan, och då är den sidan givarens skydd.
- **Varje nummersida måste ha något eget.** Fältet `malgrupp` finns för det. Sex nästan identiska
  nummersidor läses som tunt, duplicerat innehåll och riskerar att ingen av dem plockas.
- **Påstå aldrig mer än vad som kontrollerats.** När `korskontroll` är `false` ska sidan säga att
  organisationen ännu inte publicerat sina nummer — inte visa ett grönt märke.
- **Skriv aldrig att något är verifierat "av Svensk Insamlingskontroll" eller "av myndighet".**
  Vi kontrollerar mot deras register. Vi är inte de.
- **Datum på varje påstående.** `senastVerifierad` ska alltid renderas synligt.
- **Nummer normaliseras alltid via `src/lib/nummer.ts`.** Jämför aldrig nummersträngar direkt.
- **Trygghetstexten om BankID styrs av `organisationer.bankid_i_samtal`.** Flera kampanjer bekräftar
  gåvor med BankID. Skriv aldrig "frågar aldrig efter BankID" hårdkodat.
- **Fasta nummer per kund är en förutsättning.** Sex parallella nummer med samma målgrupp blir sex
  dubbletter. Registret ger effekt först när kunden ringer från ett fåtal fasta nummer med varsin målgrupp.
- **Verifieringssidan beskriver bara det som är byggt.**

## Konventioner

- Svenska i all UI-text, kod och kommentarer.
- Inga UI-bibliotek. Ren CSS med tokens för ljust och mörkt läge (design-tokens.css).
- Servermiljö som standard. `"use client"` bara där interaktion krävs.
- Håll sidorna lätta. En orolig människa öppnar dem på mobil över 4G.
