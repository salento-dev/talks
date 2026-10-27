# Contribuire

Le slide dei talk di [Salento.dev](https://salento.dev) sono aperte a tutta la community: puoi proporre un talk nuovo, correggere un refuso o migliorare lo stile.

## Prerequisiti

- Node.js LTS
- [pnpm](https://pnpm.io), la versione indicata in `packageManager` nel [package.json](package.json)

## Comandi

```sh
pnpm install                 # dalla radice del repo
pnpm --filter talk1 dev      # anteprima di un talk su http://localhost:3030
pnpm packages:build-base     # build di tutti i talk in dist/, come nel deploy
```

Ogni merge su `main` pubblica il sito su [talks.salento.dev](https://talks.salento.dev) con GitHub Pages.

## Come è fatto il repo

- `packages/talkN`: un pacchetto Slidev per ogni talk.
- `packages/addon-salento-dev`: lo stile condiviso. Il suo [README](packages/addon-salento-dev/README.md) è il catalogo dei pattern da usare nelle slide. Un pattern nuovo va nell'addon, così lo ritrova anche il talk successivo.
- `packages/index`: la pagina che elenca i talk.

Se usi Claude Code, la skill [talk-slide](.claude/skills/talk-slide/SKILL.md) guida la creazione, la modifica e la conversione di un talk, compresi i passi per aggiungerlo al README e alla pagina indice.

## Proporre una modifica

1. Crea un branch da `main`.
2. Fai le modifiche e controlla le slide in anteprima.
3. Apri una pull request verso `main` descrivendo cosa cambia.

I messaggi di commit seguono [Conventional Commits](https://www.conventionalcommits.org) in italiano, come nella storia del repo: `feat: …`, `fix: …`, `docs: …`, `chore: …`.

## Contenuti

- Testi in italiano.
- Usa solo immagini che hai il diritto di pubblicare: tue, del brand Salento.dev o con licenza compatibile.
- Niente dati personali di altri (numeri di telefono, mail, link di invito privati) senza il loro consenso.
