# Lei Compass pe Netlify, cu AI

Ce e în acest folder:

- `public/` – site-ul (index.html, iconițe pentru telefon).
- `netlify/functions/ai.mjs` – funcția care vorbește cu Claude API. Cheia ta API stă doar aici, pe server, niciodată în browser.
- `netlify.toml` – îi spune lui Netlify unde e site-ul și unde e funcția.

## Pasul 1. Cheia API Claude

1. Intră pe [platform.claude.com](https://platform.claude.com) și fă-ți cont.
2. La Billing adaugă credit (5–10 $ ajung mult timp pentru un grup de prieteni) și setează o limită lunară de cheltuieli. E plasa ta de siguranță.
3. La API keys apasă „Create key” și copiaz-o. O vezi o singură dată.

## Pasul 2. Alege un cod de acces

O parolă pe care o dai doar prietenilor, de exemplu `compass-arad-2026`. Fără cod, nimeni nu poate folosi AI-ul pe banii tăi.

## Pasul 3. Pune site-ul pe Netlify

Atenție: drag & drop (Netlify Drop) **nu** pornește funcțiile, deci AI-ul n-ar merge. Alege una dintre variante:

**Varianta A – GitHub (fără terminal)**

1. Pe github.com fă un repository nou (poate fi privat).
2. „Add file” → „Upload files” → trage tot conținutul acestui folder (`netlify.toml`, `public`, `netlify`, `README.md`) → „Commit changes”.
3. Pe app.netlify.com: „Add new project” (în unele conturi „Add new site”) → „Import an existing project” → GitHub → alegi repository-ul → „Deploy”. Netlify citește singur `netlify.toml`.

**Varianta B – Netlify CLI (dacă ai Node.js instalat)**

Deschide un terminal în acest folder și rulează:

```
npx netlify-cli login
npx netlify-cli deploy --prod
```

Când te întreabă, alege să creezi un proiect nou.

## Pasul 4. Pune cheia și codul în Netlify

În proiectul tău Netlify: „Project configuration” (sau „Site configuration”) → „Environment variables” → „Add a variable”:

| Nume | Valoare |
|---|---|
| `ANTHROPIC_API_KEY` | cheia de la pasul 1 |
| `ACCESS_CODE` | codul de la pasul 2 |

Opționale:

| Nume | Ce face | Implicit |
|---|---|---|
| `MODEL_QUICK` | modelul pentru logare rapidă și chat | `claude-haiku-5-5` |
| `MODEL_DEEP` | modelul pentru „Think deeper”, tipare și review săptămânal | `claude-sonnet-5-5` |
| `RATE_LIMIT_PER_HOUR` | câte cereri AI pe oră poate face un dispozitiv (aproximativ) | `60` |

Apoi „Deploys” → „Trigger deploy” → „Deploy site”, ca site-ul să ia valorile noi.

## Pasul 5. Folosește-l

1. Deschide linkul de la Netlify.
2. Fă-ți planul, apoi intră la Coach (sau Settings, rotița) și scrie codul de acces → „Unlock AI”.
3. Trimite prietenilor linkul și codul.

Pe telefon: deschide site-ul în browser → Share → „Add to Home Screen”. Se deschide ca o aplicație.

## Cât costă AI-ul

- Logare rapidă și chat cu Compass: Claude Haiku 5.5 (0,10 $ / 0,50 $ pe milion de tokeni). Un mesaj costă în jur de 0,06 cenți, adică peste 1.500 de mesaje la 1 $.
- „Think deeper”, „Explain my patterns” și review-ul cu AI: Claude Sonnet 5.5 (2 $ / 10 $ pe milion de tokeni), în jur de 1,5 cenți pe răspuns.

Sunt estimări. Consumul real îl vezi în platform.claude.com.

## Unde stau datele

- Fiecare om își ține datele în browserul lui, pe dispozitivul lui. Tu nu le vezi, ei nu le văd pe ale tale.
- Dacă cineva își șterge datele browserului sau schimbă telefonul, le pierde. Din Settings se poate descărca oricând un backup (.json) și se poate restaura.
- Când cineva folosește AI-ul, întrebarea lui și cifrele necesare trec prin funcția ta spre Claude API. Spune-le prietenilor asta.

## Siguranță

- Nu pune niciodată cheia API în `index.html` sau pe GitHub. Doar în „Environment variables”.
- Dacă codul ajunge la cine nu trebuie, schimbă `ACCESS_CODE` în Netlify și fă din nou deploy. Toți vor trebui să scrie codul nou.
- Limita de cheltuieli din platform.claude.com te apără dacă ceva scapă de sub control.

## Actualizări

Când primești o versiune nouă, înlocuiești fișierele în GitHub (Varianta A) și Netlify publică singur, sau rulezi din nou `npx netlify-cli deploy --prod` (Varianta B).
