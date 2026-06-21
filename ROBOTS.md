# Robots.txt Analysis — Yardi Romania (Breezy.hr)

Sursa: https://yardiromania.breezy.hr/robots.txt

## Reguli

```
User-agent: *
Disallow: /
```

## Interpretare

| Cale | Accesibil? | Ce conține |
|---|---|---|
| `/` | ❌ **Disallowed** | Pagina principală cu listări de job-uri |
| `/p/*` | ❌ **Disallowed** | Paginile individuale de job |
| `/json` | ❌ **Disallowed** | API-ul JSON de la care scraper-ul extrage datele |

## Recomandare

robots.txt NU este legal binding, dar reprezintă intenția proprietarului site-ului.

- API-ul `/json` e **disallowed** de robots.txt. În practică, serverul nu blochează cererile (răspunde cu 200 OK).
- Paginile individuale de job (`/p/...`) sunt și ele disallowed. Noi nu le scraper-uim direct — doar le verificăm accesibilitatea (HEAD request) în E2E tests.
- Scraperul curent face o singură cerere GET către `/json` pentru a obține toate job-urile — comportament rezonabil, nu agresiv.

**Concluzie**: Risc minim. API-ul e public, răspunde fără autentificare, iar scraperul e politicos (User-Agent standard, o singură cerere simultană).
