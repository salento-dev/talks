# CLAUDE.md

Slide dei talk di Salento.dev, fatte con [Slidev](https://sli.dev). Monorepo pnpm: ogni talk è un pacchetto in `packages/` (`talk0`, `talk1`, …), `packages/index` è la pagina di atterraggio, `packages/addon-salento-dev` è lo stile condiviso. Per la community e l'elenco dei talk vedi il [README](README.md); per prerequisiti, comandi e flusso delle PR vedi [CONTRIBUTING](CONTRIBUTING.md).

## Regole del codice

- Formattazione da [.editorconfig](.editorconfig): 2 spazi, LF, newline finale.
- Per creare, modificare o convertire slide usa la skill [talk-slide](.claude/skills/talk-slide/SKILL.md). Lo stile e i pattern sono nel [catalogo dell'addon](packages/addon-salento-dev/README.md): un pattern nuovo va nell'addon, non nel singolo talk.
- Contenuti in italiano.

## Git

- Commit e push solo su richiesta esplicita.
- Nessuna riga di attribuzione nei commit: niente `Co-authored-by` per Claude o altri assistenti. Nelle PR niente "Generated with Claude Code" né diciture simili.
- Messaggi in stile Conventional Commits, in italiano, come nella storia esistente (`feat: …`, `fix: …`, `chore: …`); corpo facoltativo per spiegare il perché.
- Lavora su un branch e apri una PR verso `main`. Se `main` è protetto, il push diretto non è un'opzione.
