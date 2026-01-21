
# Workshop: Refactoring - Från Spagetti till Arkitektur

**Uppdrag:** Idag ska vi städa! Du ska ta ditt befintliga TypeScript-projekt och strukturera om koden.

Målet är inte att ändra *hur* appen ser ut för användaren, utan att göra koden mer lättläst, skalbar. Vi ska gå från en stor `main.ts` eller `index.ts` (vad ni nu döpt eran huvudfil) till en modulär struktur.

---

## Förberedelser tips (Viktigt!)

Innan du rör en enda rad kod:

1.  Se till att ditt projekt fungerar och är sparat (committat) på git.
2.  Skapa en **ny branch** för dagens arbete. Detta är din säkerhetslina om något går sönder.
    ```bash
    git checkout -b refactor
    ```

---

## Målbild

När du är klar bör din `src`-mapp se ut ungefär så här. Namnen beror på vad din app handlar om (t.ex. `Movie`, `Product`, `Todo`).

```text
src/
 ├── models/          (Dina interfaces/typer - "Ritningarna")
 ├── components/      (Funktioner som skapar HTML - "Målarna")
 ├── services/        (Hanterar din data/fetch - "Lagret")
 ├── utils/           (Små hjälpfunktioner - "Verktygen")
 └── main.ts          (Dirigenten som styr allt)
```

Steg för steg
1. Flytta Ritningarna (Models) 
Leta upp dina interface eller type-definitioner i din kod.
Gör: Skapa mappen src/models.
Filnamn: Döp filen efter det den beskriver (t.ex. Todo.ts, Weather.ts).
Kod: Klipp ut interfacet, klistra in det och lägg till nyckelordet export.
Fixa: Gå tillbaka till main.ts och importera det.

2. Flytta Målar-koden (Components) 
Leta efter funktioner som skapar HTML-element (t.ex. document.createElement, innerHTML, append).
Gör: Skapa mappen src/components.
Filnamn: T.ex. TodoList.ts, ProductCard.ts.
Refactoring:
Se till att funktionen tar emot data som argument (parametrar) istället för att läsa globala variabler.
Exempel: renderList(list: Todo[]) istället för att läsa en global todoList.

3. Flytta Datan (Services) 
Har du en hårdkodad lista (mock data) eller kod som gör fetch()?
Gör: Skapa mappen src/services.
Filnamn: T.ex. TodoService.ts eller ApiService.ts.
Kod: Flytta datan/fetch-anropet hit. Exportera en funktion som heter t.ex. getTodos() som returnerar datan.

4. Flytta Verktygen (Utils) 
Har du kod som inte handlar om din specifika app, utan är generell logik? T.ex. spara till localStorage, slumpa tal eller formatera datum/tid?
Gör: Skapa mappen src/utils.
Filnamn: T.ex. storage.ts eller helpers.ts.
Tänk på: Dessa funktioner ska vara "rena". Skicka in data -> Få ut resultat.

5. Städa Dirigenten (Main.ts) 
Nu ska din main.ts vara mycket kortare!

Kvar ska finnas:
Initiering av appen (hämta data).
Event Listeners (klick på knappar, submit av formulär).
Anrop till dina nya moduler.
Bort ska: All logik som skapar HTML eller hanterar data direkt.

### Vad ska jag flytta? (Lathund)

Använd lathunden nedan för att avgöra var din kod hör hemma:

| Om koden... | Flytta till: |
| :--- | :--- |
| Definierar `interface` eller `type` | 📂 **`src/models/`** |
| Använder `createElement`, `innerHTML` eller `append` | 📂 **`src/components/`** |
| Innehåller `fetch()` eller listor med data | 📂 **`src/services/`** |
| Använder `localStorage` eller räknar ut matte/tid | 📂 **`src/utils/`** |
| Lyssnar på `addEventListener` eller startar appen | 📄 **`src/main.ts`** (Låt ligga kvar) |


