# Pizzichino — regole del progetto

Sito **pizzichino.it**: pagina unica "Regala un sito web comico" (99 €, 72 ore) + privacy.
Statico, Eleventy 2, stesso schema di deploy di clickbari.it. Il negozio vero (repo
`sito-regalo`, Netlify + Stripe) è un progetto separato e futuro: qui niente pagamenti.

## Struttura
- `src/index.html` — la pagina (CSS inline, prefisso `rg-`; header/footer `pz-`).
  Nata dalla vecchia `clickbari.it/sito-regalo/` (ottobre 2026).
- `src/privacy.html` — informativa (niente cookie, niente analytics, contatti via WhatsApp).
- Font self-hosted in `src/fonts/` (Bebas Neue, DM Sans, Shantell Sans). Niente Google Fonts.
- Immagini: `src/img/regalo/<slug>.webp` (600×1298, anteprime delle 3 demo), `src/img/og.png`
  (anteprima social 1200×630), favicon `src/favicon.svg` + png.
- Le 3 demo (Kir fa tutto, Nonna a Noleggio, Mimmo il Parcheggiatore) restano su Netlify,
  repo separati.
- JSON-LD `FAQPage` + `Service/Offer` (99 EUR) in `index.html`: se cambiano prezzo o FAQ,
  aggiorna anche il JSON-LD.
- Nessun riferimento al brand ClickBari sulla pagina (scelta voluta).

## Deploy
push su `main` → GitHub Action (`.github/workflows/build.yml`) → `npm run build` →
pubblica `_site/` sul branch `dist` (mai `force_orphan`) → OVH (Multisito, dominio
pizzichino.it collegato via Git al branch `dist`, webhook GitHub → OVH).
Push diretto su `main` dopo ogni modifica concordata.
