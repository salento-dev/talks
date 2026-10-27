# Creare il pacchetto di un nuovo talk

`N` è il numero successivo all'ultimo `packages/talkN`. Usa `packages/talk1` come modello. Il deploy passa da GitHub Pages: i `netlify.toml` dei talk esistenti non servono.

## Pacchetto (prima di generare le slide)

1. `packages/talkN/package.json`: copia quello di talk1 e cambia `name` in `talkN` e i percorsi di `build-base` in `../../dist/talkN` e `/talkN/`.
2. `packages/talkN/public/`: copia `favicon.svg` e `qrcode.svg` da talk1 (il QR punta a salento.dev; se lo speaker vuole un altro link, va generato nuovo).
3. `packages/talkN/slides.md` con questo headmatter, adattando `title`, `info` e `duration` alle risposte dell'intervista:

   ```yaml
   ---
   theme: default
   colorSchema: dark
   addons:
     - salento-dev
   transition: console
   favicon: /favicon.svg
   title: Salento.dev - Talk \#N · Titolo
   info: |
     Una riga sul talk.
     Evento @ Comune, mese anno.
   duration: 20min
   drawings:
     persist: false
   mdc: true
   routerMode: hash
   layout: center
   class: text-center
   ---
   ```

4. `pnpm install` dalla radice del repo.

## Pubblicazione (dopo l'approvazione delle slide)

5. Copertina: esporta la prima slide (`npx slidev export --format png --range 1 --output <cartella fuori dal repo>`), portala a 1280 × 720 come le altre copertine e salvala in `packages/talkN/public/cover.png`.
6. Aggiungi il talk al [README](../../../README.md), sezione "Talk": `### AAAA/MM/GG - Titolo`, la copertina con link a `https://talks.salento.dev/talkN/` e una riga di descrizione.
7. Aggiungi una `<article class="talk-card">` in [packages/index/index.html](../../../packages/index/index.html), prima del commento "Placeholder per future presentazioni", con titolo `Talk #N`, la stessa descrizione del README e la durata.

Il talk è pubblicabile quando `pnpm packages:build-base` dalla radice produce `dist/talkN/`.
