# Fælles budget – GitHub Pages + synkronisering

Denne version synkroniserer det samme budget mellem flere telefoner/computere via Supabase. Hvis Supabase ikke er konfigureret, virker siden stadig med lokal browserlagring.

## 1. Opret GitHub Pages
1. Opret et GitHub repository, fx `budget`.
2. Upload `index.html`.
3. Gå til **Settings → Pages**.
4. Vælg **Deploy from a branch → main → /(root)**.

## 2. Opret Supabase
1. Opret et Supabase-projekt.
2. Åbn **SQL Editor**.
3. Kør hele `supabase-setup.sql`.
4. Find din **Project URL** og **Publishable key** under projektets Connect/API Keys-indstillinger.

## 3. Indsæt Supabase-oplysninger i index.html
Find disse linjer tæt på bunden:

```js
const SUPABASE_URL = "PASTE_YOUR_SUPABASE_URL_HERE";
const SUPABASE_PUBLISHABLE_KEY = "PASTE_YOUR_SUPABASE_PUBLISHABLE_KEY_HERE";
const BUDGET_ID = "vores-budget";
```

Erstat URL og publishable key med værdierne fra dit Supabase-projekt.

Skift også `BUDGET_ID` til et unikt navn, fx:

```js
const BUDGET_ID = "vores-husholdning-2026";
```

## 4. Første gang siden åbnes
Siden spørger efter en **fælles budgetkode**. Vælg en lang kode, som kun I kender. Første enhed opretter budgettet med denne kode. På andre telefoner/computere indtaster I præcis den samme kode.

Budgetkoden gemmes lokalt på den enkelte enhed. Selve Supabase-tabellen kan ikke læses direkte fra browserens public key; data hentes og gemmes via funktioner, der validerer budgetkoden.

## Sikkerhed
- Brug kun Supabases **publishable key** i HTML-filen. Brug aldrig en secret/service-role key i GitHub eller browserkode.
- Brug en lang, unik budgetkode.
- Gem ikke CPR-numre, adgangskoder, kortnumre eller andre stærkt følsomme oplysninger i budgettet.
