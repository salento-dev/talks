# CLAUDE.md

Slide dei talk di Salento Dev, fatte con [Slidev](https://sli.dev). Monorepo pnpm: ogni talk è un pacchetto in `packages/` (`talk0`, `talk1`, …), `packages/index` è la pagina di atterraggio. Per la descrizione della community e l'elenco dei talk vedi il [README](README.md).

## Comandi

- `pnpm install` dalla radice
- `pnpm --filter talk1 dev`: anteprima di un talk
- `pnpm packages:build-base`: build di tutti i pacchetti in `dist/` (la stessa usata per il deploy)

Ogni push su `main` pubblica il sito con GitHub Pages ([.github/workflows/deploy.yaml](.github/workflows/deploy.yaml)).

## Regole del codice

- Formattazione da [.editorconfig](.editorconfig): 2 spazi, LF, newline finale.
- Un nuovo talk è un nuovo pacchetto `packages/talkN` con gli script `build-base` (output in `../../dist/talkN`, base `/talkN/`), più la voce nel README e nella pagina indice.
- Contenuti in italiano.

## Git

- Commit e push solo su richiesta esplicita.
- Nessuna riga di attribuzione nei commit: niente `Co-authored-by` per Claude o altri assistenti. Nelle PR niente "Generated with Claude Code" né diciture simili.
- Messaggi in stile Conventional Commits, in italiano, come nella storia esistente (`feat: …`, `fix: …`, `chore: …`); corpo facoltativo per spiegare il perché.
- Lavora su un branch e apri una PR verso `main`. Se `main` è protetto, il push diretto non è un'opzione.
