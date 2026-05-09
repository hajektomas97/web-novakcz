# 📖 Návod: Jak nasadit web klientovi (krok za krokem)

## Co máš v šabloně

```
web-sablona/
├── index.html          ← samotný web (neupravuj strukturu, jen CSS/design)
├── netlify.toml        ← konfigurace Netlify (neměň)
├── admin/
│   ├── index.html      ← přihlašovací stránka adminu (neměň)
│   └── config.yml      ← CO může klient editovat ← TOTO upravuješ pro každý projekt
└── content/
    └── data.json       ← OBSAH webu ← TOTO vyplníš pro každý projekt
```

---

## KROK 1 – Připrav GitHub účet (jednou, navždy)

1. Jdi na **github.com** → Sign up → vytvoř si účet
2. Hotovo, GitHub budeš používat pro každý projekt

---

## KROK 2 – Pro každý nový projekt: Vytvoř repozitář

1. Na GitHubu klikni **"New repository"**
2. Název: `web-novakcz` nebo cokoliv popisného
3. Nastav na **Public** (zdarma, Decap to vyžaduje)
4. Klikni **"Create repository"**

---

## KROK 3 – Nahraj šablonu na GitHub

Máš dvě možnosti:

### Varianta A – přes GitHub web (jednodušší na začátek)
1. V repozitáři klikni **"uploading an existing file"**
2. Přetáhni všechny soubory ze složky `web-sablona`
3. Klikni **"Commit changes"**

### Varianta B – přes příkazový řádek (rychlejší dlouhodobě)
```bash
cd web-sablona
git init
git add .
git commit -m "prvni verze"
git remote add origin https://github.com/TVUJUCET/REPOZITAR.git
git push -u origin main
```

---

## KROK 4 – Nasaď na Netlify

1. Jdi na **netlify.com** → Sign up (přihlásit přes GitHub)
2. Klikni **"Add new site"** → **"Import an existing project"**
3. Vyber GitHub → vyber svůj repozitář
4. Nastav:
   - **Branch to deploy:** `main`
   - **Build command:** (nechej prázdné)
   - **Publish directory:** `.`
5. Klikni **"Deploy site"**

Web je online! Netlify ti dá adresu jako `random-name-123.netlify.app`

---

## KROK 5 – Zapni administraci (Netlify Identity)

1. V Netlify jdi do **Site settings → Identity**
2. Klikni **"Enable Identity"**
3. Dolu najdi **"Git Gateway"** → klikni **"Enable Git Gateway"**
4. Jdi na **Identity → Invite users**
5. Zadej emailovou adresu klienta a pošli pozvánku

Klient dostane email, klikne na odkaz, nastaví si heslo a může se přihlásit na `jehoWeb.cz/admin`

---

## KROK 6 – Přidej klientovu doménu (zdarma)

1. Netlify → **Site settings → Domain management**
2. Klikni **"Add custom domain"**
3. Zadej doménu: `novak-instalater.cz`
4. Netlify ti ukáže DNS záznamy – zadáš je do správy domény (u registrátora jako Wedos, Forpsi apod.)
5. Počkáš 15 minut až 2 hodiny → web běží na klientově doméně

---

## KROK 7 – Vyplň obsah pro klienta

Otevři soubor `content/data.json` a vyplň vše:

```json
{
  "firma_nazev": "Novák Instalatér",
  "meta_popis": "Instalatérské služby v Brně...",
  "hero_kicker": "Instalatér · Brno",
  "hero_nadpis": "Rychlá pomoc s instalacemi.",
  ...
}
```

Nebo nech klienta, ať si to vyplní sám přes admin po přihlášení.

---

## JAK FUNGUJE ÚPRAVA PRO KAŽDÉHO KLIENTA

Pro každého klienta uděláš jen toto:

1. **Duplikuješ repozitář** (nebo zkopíruješ soubory)
2. **Upravíš design** v `index.html` – barvy v `:root { }` a fonty
3. **Upravíš `config.yml`** – odebereš nebo přidáš pole podle potřeby klienta
4. **Vyplníš `data.json`** – obsah webu
5. **Nasadíš na Netlify** – 5 minut práce

---

## ÚPRAVA BAREV PRO KAŽDÝ PROJEKT

V `index.html` najdi tuto část (začátek `<style>`):

```css
:root {
  --green: #10b981;        ← hlavní akcentní barva
  --green-dim: rgba(16,185,129,0.10);   ← světlá verze (background)
  --green-border: rgba(16,185,129,0.22); ← border
  ...
}
```

Stačí změnit `--green` na jinou barvu. Vše ostatní se přizpůsobí automaticky.

Příklady:
- Modrá: `#3b82f6`
- Fialová: `#8b5cf6`
- Oranžová: `#f59e0b`
- Červená: `#ef4444`

---

## JAK PŘIDAT/ODEBRAT SEKCI

Chceš přidat sekci "Ceník"? Řekni Claudovi:

> "Přidej do šablony sekci Ceník s kartami pro tři balíčky. Ceny a popisy ať jdou editovat přes admin."

Claude upraví `index.html` i `config.yml`.

---

## ČASTÉ DOTAZY

**Q: Kolik stojí hosting?**
A: Zdarma na Netlify. Doména .cz stojí cca 150–200 Kč/rok.

**Q: Může klient rozbít design?**
A: Ne. V administraci vidí jen textová pole – barvy ani rozvržení měnit nemůže.

**Q: Co když klient zapomene heslo?**
A: V Netlify Identity mu pošleš nový reset email.

**Q: Jak rychle se zobrazí změna po uložení v adminu?**
A: Do 30–60 sekund. Netlify automaticky znovu sestaví web.

**Q: Kde se ukládají fotky?**
A: Přímo do repozitáře na GitHubu, do složky `images/`.

---

## CHECKLIST PŘED ODEVZDÁNÍM KLIENTOVI

- [ ] Web funguje na Netlify URL
- [ ] Klientova doména ukazuje na web
- [ ] Klient má pozvánku do administrace
- [ ] Klient umí změnit text a uložit
- [ ] Formulář odesílá (otestuj přes Netlify Forms v dashboardu)
- [ ] Web vypadá dobře na mobilu
- [ ] Favicon nastaven (optional)
- [ ] Google Analytics přidány (optional)
