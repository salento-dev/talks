# Formato di scaletta e bozze

## SCALETTA.md

Tutto il materiale del talk, organizzato per sezione: fatti, date, numeri con la loro fonte, link, immagini da raccogliere. Può essere lunga: qui non si decide cosa va a schermo.

```markdown
# Talk #N · Titolo

> Bozza di lavoro. Le slide (`slides.md`) si rigenerano da qui solo alla fine.
> Legenda: `TODO` = da completare · `?` = da verificare · `📷` = foto da inserire

**Evento:** Nome @ Comune · data · luogo
**Durata:** ~N min
**Pubblico:** chi c'è e cosa sa già

---

## 1. Sezione

- Fatto, con la fonte
- Numero: 25.000 messaggi (export chat al 25/10) ?

## Materiali da raccogliere

- 📷 screenshot del sito
```

## BOZZE.md

Una sezione per slide, numerate. Qui si decide cosa va a schermo (poco), cosa si mostra e cosa si dice.

```markdown
# Bozze slide · Talk #N

> Una sezione per slide: **a schermo** è il testo visibile (poco), **visual** è cosa mostrare, **note** è cosa dire.
> Fonte dei dati: `SCALETTA.md`. Le slide Slidev si generano da qui alla fine.
> Totale: N slide · circa N min

---

## 1 · Copertina

**A schermo**
- `root@salento.dev · talk #N`
- **Titolo**
- Evento @ Comune · mese anno

**Visual:** logo stacked white-on-dark, fondo a puntini.

**Note:** "La prima frase che dici."

---

## 2 · Titolo della slide

**A schermo**
- `01 · sezione`
- titolo con **una** parola in evidenza
- tre pannelli: …

**Visual:** pattern del catalogo (pannelli, timeline, barre, screenshot…).

**Note:** cosa dire, transizione verso la slide successiva.
```

Le slide che si possono saltare se si è lunghi coi tempi si segnano `(opzionale)` nel titolo della sezione.

In una conversione, ogni sezione indica da dove arriva (`**Origine:** slide 3 e 4`).

In fondo al file c'è sempre una sezione **Domande per lo speaker**: i `?` ancora aperti e le scelte da confermare. In una conversione aggiungi anche cosa è stato tagliato o unito rispetto all'originale.
