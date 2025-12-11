# 🌍 Földrajz Kvíz Alkalmazás

## 📦 Mit tartalmaz a csomag?

- **index.html** - A főoldal
- **style.css** - Reszponzív stílusok
- **script.js** - Kvíz logika
- **csillagaszat.xlsx** - Minta Excel (**16 kérdés**: 7 könnyű, 5 közepes, 4 nehéz)

## 🚀 Használat

### 1. Fájlok elhelyezése
Helyezd el az összes fájlt egy mappába:
```
/kviz-projekt
  ├── index.html
  ├── style.css
  ├── script.js
  ├── csillagaszat.xlsx
  ├── kozetbolygo.xlsx
  ├── legkor.xlsx
  ├── vizburok.xlsx
  ├── geoszferak.xlsx
  └── kepek/
      ├── csillagaszat/
      ├── kozetbolygo/
      ├── legkor/
      ├── vizburok/
      └── geoszferak/
```

### 2. Excel fájlok készítése

**FONTOS: Az Excel első sora a ponthatárokat tartalmazza!**

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| **Ponthatárok** | **30** | **40** | **50** | | | |
| **kerdés** | **tipus** | **helyes_valaszok** | **hibas_valaszok** | **pontErtek** | **nehezseg** | **kep** |
| Válaszd ki... | egyszeres | VI. 22. | III. 21.;... | 2 | könnyű | jupiter.jpg |

**1. sor (Ponthatárok):**
- **B1**: Bronz szint minimális pontja (alapértelmezett: 30)
- **C1**: Ezüst szint küszöbe (alapértelmezett: 40)
- **D1**: Arany szint küszöbe (alapértelmezett: 50)

**2. sor (Header):**
Oszlopnevek

**3. sortól (Kérdések):**

| Oszlop neve | Leírás | Példa |
|-------------|--------|-------|
| **kerdés** | A kérdés szövege | "Mi az eltérítő erő másik neve?" |
| **tipus** | "egyszeres", "tobbszoros" vagy "szoveges" | "szoveges" |
| **helyes_valaszok** | Helyes válaszok, pontosvesszővel elválasztva | "Coriolis;coriolis erő" |
| **hibas_valaszok** | Hibás válaszok, pontosvesszővel elválasztva | "Newton;Kepler" |
| **pontErtek** | Hány pontot ér a kérdés (szám!) | 8 |
| **nehezseg** | "könnyű", "közepes" vagy "nehéz" | "közepes" |
| **kep** | Kép fájlnév (opcionális) | "jupiter.jpg" |

**Fontos:**
- Az **első sor** mindig a **Ponthatárok** (3 szám: bronz, ezüst, arany)
- A **második sor** a **header** (oszlopnevek)
- A **harmadik sortól** kezdődnek a **kérdések**
- Pontosvesszővel (`;`) válaszd el a több választ
- Szöveges kérdéseknél a `hibas_valaszok` üres lehet
- Szöveges kérdéseknél több szinonimát is megadhatsz (pl. "66,5;66.5")
- Típus értékek: `egyszeres`, `tobbszoros`, `szoveges` (ékezet nélkül!)
- Nehézség értékek: `könnyű`, `közepes`, `nehéz`
- A `pontErtek` legyen **szám formátum** (nem szöveg!)
- A `kep` oszlop **opcionális** - ha nincs kép, hagyd üresen

### 2a. Képek használata (opcionális)

**Mappa struktúra:**
```
/kviz-projekt
  ├── index.html
  ├── script.js
  ├── csillagaszat.xlsx
  └── kepek/
      ├── csillagaszat/
      │   ├── jupiter.jpg
      │   └── mars.png
      ├── kozetbolygo/
      ├── legkor/
      ├── vizburok/
      └── geoszferak/
```

**Támogatott formátumok:** JPG, PNG, GIF

**Használat:**
- Az Excel `kep` oszlopában add meg a fájlnevet: `jupiter.jpg`
- A kép automatikusan a kérdés alatt jelenik meg
- Reszponzív: telefonon és tableten is jól néz ki
- Max méret: 400px magasság (desktop), automatikus szélesség

### 3. Futtatás

**Helyi gépről:**
1. Nyisd meg az `index.html` fájlt böngészőben
2. ⚠️ **Fontos:** Néhány böngésző nem engedi az Excel fájlok betöltését `file://` protokollal
3. **Megoldás:** Használj helyi szervert:

**Python 3:**
```bash
python -m http.server 8000
```

**Node.js:**
```bash
npx http-server
```

Majd nyisd meg: `http://localhost:8000`

**GitHub Pages:**
1. Hozz létre egy új repository-t
2. Töltsd fel az összes fájlt
3. Engedélyezd a GitHub Pages-t a Settings menüben
4. Az alkalmazás elérhető lesz: `https://[felhasználónév].github.io/[repo-név]`

## 🏆 Szintrendszer

A kvíz **mindig megy 10 kérdésig** (vagy amíg vannak kérdések), nem áll meg 30 pontnál!

### Szintek:
- 🥉 **Bronz szint** (30-39 pont)
  - Bronz színű tanúsítvány
  - ⭐ egy csillag
  
- 🥈 **Ezüst szint** (40-49 pont)
  - Ezüst színű tanúsítvány
  - ⭐⭐ két csillag
  
- 🥇 **Arany szint** (50+ pont)
  - Arany színű tanúsítvány
  - 3 véletlenszerű emoji (☄️🚀🛸🌌🔭💫 + max 1 Föld középen)
  - **Sárga emojik kizárva** (jobb láthatóság sárga háttéren)

### Játékmenet:
1. Válassz témakört
2. Minden kérdés előtt választhatsz nehézséget
3. A visszajelzésnél látod az aktuális pontszámod és szinted
4. 30 pont alatt látod: "Még X pont kell a bronz szinthez!"
5. 30 pont felett látod: "🥉 Bronz szint elérve! Még X pont az ezüstig!"
6. **50 pontnál (arany szint) automatikusan vége a kvíznek** - nincs értelme tovább menni!
7. Vagy válaszolsz 10 kérdésre (ha van annyi), vagy elfogynak a kérdések
8. A végén az elért szintnek megfelelő színes tanúsítványt töltesz le

**Stratégia:** 
- 10× könnyű (2-3 pont) = max ~30 pont → csak bronz
- Mix: 5× közepes + 5× nehéz = 40-60 pont → ezüst vagy arany! 🏆

## ✨ Funkciók

✅ 5 témakör választás  
✅ Nehézségi szintek (könnyű, közepes, nehéz)  
✅ **Változó kérdésszám**: Maximum 10 kérdés (vagy 50 pont, vagy ha elfogynak a kérdések)  
✅ **Ponthatárok témakörönként beállíthatók** az Excel első sorában  
✅ **Szintrendszer**:
  - 🥉 Bronz szint (alapértelmezett: 30-39 pont)
  - 🥈 Ezüst szint (alapértelmezett: 40-49 pont)
  - 🥇 Arany szint (alapértelmezett: 50+ pont) - **automatikus vége!**
✅ **Véletlenszerű űr emojik** tanúsítványokon (15 különböző)
  - Arany tanúsítványon: Csak jól látható emojik (sárgák kizárva)
  - Föld emoji automatikusan középre kerül (ha van)
  - Maximum 1 Föld típus tanúsítványonként
✅ **Automatikus folytatás**: Nem áll meg 30 pontnál, de 50 pontnál (arany) igen!  
✅ **Valós idejű információk**:
  - Aktuális szint és következő szint távolsága
  - Hátra lévő kérdések száma (kivéve arany szintnél)
✅ Feleletválasztós (egyszeres és többszörös)
  - Teljes válasz mező kattintható (nem csak a checkbox/radio)
✅ Szöveges válaszok
  - Több szinonima támogatása (pl. "66,5;66.5")
  - Autocomplete kikapcsolva (nem jegyez)
✅ **Képes kérdések** (opcionális)
  - JPG, PNG, GIF formátumok támogatva
  - Reszponzív megjelenítés (mobil/tablet/desktop)
  - Témakörönkénti képmappák
✅ Pontozás kérdésenként beállított pontértékekkel  
✅ **Színes tanúsítványok** szintenként (bronz/ezüst/arany)  
✅ Tanúsítvány csak egyszer letölthető  
✅ Reszponzív dizájn (mobil, tablet, desktop)  
✅ Helyes válaszok megjelenítése a végén  

## 🎨 Testreszabás

### Színek módosítása
A `style.css` fájlban található a színséma. Főbb változók:
- Főszín: `#667eea` és `#764ba2` (gradiens)
- Könnyű gomb: `#2ecc71` (zöld)
- Közepes gomb: `#3498db` (kék)
- Nehéz gomb: `#e74c3c` (piros)

### Kérdések száma és pontküszöb

**Ponthatárok beállítása témakörönként:**
- Az Excel **első sorában** (Ponthatárok sor) állítsd be a B, C, D cellákban
- **B1**: Bronz minimum (pl. 30)
- **C1**: Ezüst küszöb (pl. 40)
- **D1**: Arany küszöb (pl. 50)
- Minden témakörnek lehet más ponthatára!

**Kódban (ha globálisan szeretnéd módosítani):**
A `script.js` fájlban:
- **Maximális kérdésszám**: Keress rá: `selectedQuestions.length >= 10` és változtasd meg a 10-et
- **Alapértelmezett pontok**: Keress rá: `window.minPoints || 30` - a 30, 40, 50 az alapértelmezett, ha nincs Excel-ben beállítva

### Tanúsítvány színek
A `script.js` `generateCertificate()` függvényében:
- **Bronz**: `color1 = '#CD7F32'`, `color2 = '#A0522D'`
- **Ezüst**: `color1 = '#C0C0C0'`, `color2 = '#A8A8A8'`
- **Arany**: `color1 = '#FFD700'`, `color2 = '#FFA500'`

### Tanúsítvány emojik
A `script.js` fájl `generateCertificate()` függvényében:
- **Emoji lista**: `const spaceEmojis = [...]` - 15 űr témájú emoji
- **Sárga emojik** (aranyról kizárva): `const yellowEmojis = [...]`
- **Föld emojik** (max 1, középre kerül aranyon): `const earthEmojis = [🌎, 🌍, 🌏]`
- Arany tanúsítványon: 3 random emoji (sárgák nélkül, Föld középen ha van)
- Ezüst: 2 random emoji
- Bronz: 1 random emoji

### Tanúsítvány dizájn
A `script.js` fájl `generateCertificate()` függvényében testreszabható:
- Méret: `canvas.width` és `canvas.height` (jelenleg 800x600)
- Színek: `color1`, `color2`, `borderColor`
- Betűtípusok: `ctx.font`

## 🐛 Hibakeresés

**Probléma:** "A fájl nem található"
- Ellenőrizd, hogy az Excel fájl neve pontosan megegyezik-e (pl. `csillagaszat.xlsx`)
- Használj helyi szervert a futtatáshoz

**Probléma:** "Hiba a kérdések betöltésekor"
- Nyisd meg a böngésző konzolt (F12)
- Ellenőrizd az Excel fájl oszlopneveit
- Győződj meg róla, hogy nincs üres sor az Excel-ben

**Probléma:** "Beragadtam, nincs tovább gomb"
- Ez akkor fordul elő, ha elfogynak a kérdések
- **Megoldva!** Most automatikusan megjelenik az eredmény, ha nincs több kérdés
- **Javaslat:** Készíts legalább 15-20 kérdést témakörönként minden nehézségből

**Probléma:** A tanúsítvány nem tölthető le
- Ellenőrizd a böngésző popup blokkolóját
- Próbáld meg másik böngészővel

## 📝 Megjegyzések

- A minta Excel fájl **16 kérdést** tartalmaz (7 könnyű, 5 közepes, 4 nehéz)
- Ajánlott legalább **15-20 kérdés** témakörönként a zavartalan játékélményhez
- A rangsorolásos kérdések későbbre maradtak (még nincs implementálva)
- A képeket tartalmazó kérdések későbbre maradtak
- A válaszok NEM a HTML kódban vannak, hanem az Excel fájlokban
- A LocalStorage használata miatt a letöltés korlátozás csak azonos böngészőben működik

## 🆘 Támogatás

Ha bármi kérdésed van, nézd meg a konzolt (F12 → Console) a részletes hibaüzenetekért!

---

**Készítette:** Claude Assistant  
**Verzió:** 1.0  
**Dátum:** 2024
