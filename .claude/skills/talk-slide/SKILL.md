---
name: talk-slide
description: Crea, modifica o converte le slide Slidev dei talk Salento.dev nello stile Night Console. Usala per un nuovo talk in packages/, per cambiare le slide di un talk esistente, o per importare una presentazione esterna (pptx, pdf, Keynote, Google Slides, un altro Slidev).
---

# Slide dei talk

Ogni talk è un pacchetto `packages/talkN` che usa l'addon [slidev-addon-salento-dev](../../../packages/addon-salento-dev/README.md). Il README dell'addon è il catalogo: regole visive e uno snippet per ogni pattern. Leggilo prima di scrivere una slide.

## Il flusso

```
SCALETTA.md  →  BOZZE.md  →  slides.md
```

- **SCALETTA.md**: tutto il materiale (contenuti, dati, fonti), organizzato per sezione.
- **BOZZE.md**: una sezione per slide, con *a schermo*, *visual* e *note*. Qui si sceglie cosa entra nel tempo a disposizione.
- **slides.md**: si genera dalle bozze.

Formato dei due file di lavoro: [bozze.md](bozze.md). Sono appunti dello speaker: chiedigli se vuole versionarli.

## Nuovo talk e conversione

1. **Intervista lo speaker** finché ogni punto ha una risposta, o lo speaker ha detto che ancora non lo sa: titolo, evento (nome, comune, data), durata, pubblico e cosa sa già, il messaggio da portare a casa, materiale disponibile (dati, screenshot, foto, link).
2. Scrivi `SCALETTA.md`. Se converti una presentazione esistente, il materiale arriva da lì: [conversione.md](conversione.md). Fai approvare la scaletta.
3. Scrivi `BOZZE.md`: circa una slide per minuto di talk, quindi da una conversione si taglia e si unisce. Fai approvare le bozze.
4. Crea il pacchetto: [nuovo-talk.md](nuovo-talk.md), passi 1-4.
5. Genera `slides.md` dalle bozze (sotto).
6. Verifica (sotto) su tutte le slide e fai approvare le slide allo speaker.
7. Pubblica il talk nel repo: [nuovo-talk.md](nuovo-talk.md), passi 5-7.

## Modifica

1. Leggi `slides.md` e, se c'è, `BOZZE.md`.
2. Applica il cambio in `slides.md` con i pattern del catalogo. Se le bozze esistono, aggiornale nello stesso giro.
3. Verifica le slide toccate.

## Generare slides.md

- Una sezione delle bozze diventa una slide: *a schermo* è il testo visibile, *visual* sceglie il pattern del catalogo, *note* va in `<!-- … -->` in fondo alla slide.
- Componi con i pattern del catalogo. Se una slide ha bisogno di un pattern nuovo, aggiungilo all'addon (classe in `styles/index.css` e voce nel README): così il talk successivo lo trova già pronto.
- Numeri, date e fatti a schermo vengono dalla scaletta. Quelli segnati `?` restano domande per lo speaker.

## Verifica

Dalla cartella del talk:

```sh
pnpm build
npx slidev export --format png --output <cartella fuori dal repo>/png
```

Con `--range 3,5-7` esporti solo le slide toccate. Al primo export Playwright può chiedere il browser: `npx playwright-core install --only-shell chromium`.

Guarda ogni PNG. La verifica è completa quando nessuna slide ha testo tagliato o fuori tela, elementi sovrapposti, immagini mancanti, pannelli sbilanciati o cyan su elementi estranei all'idea della slide.
