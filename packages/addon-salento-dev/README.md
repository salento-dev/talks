# slidev-addon-salento-dev

Lo stile **Night Console** di Salento.dev per le slide Slidev: fondo nero a puntini, cyan come unica luce, staffe d'angolo, font Outfit / Albert Sans / Roboto Mono.

L'addon porta stili, transizione `console`, la cornice animata (`global-top.vue`) e il componente `<Logo>`. Il tema sotto resta `default`.

## Uso

Nel `package.json` del talk:

```json
"dependencies": {
  "slidev-addon-salento-dev": "workspace:*"
}
```

Nell'headmatter di `slides.md`:

```yaml
theme: default
colorSchema: dark
addons:
  - salento-dev
transition: console
```

Le immagini del talk (screenshot, foto, loghi dei partner) restano nella `public/` del talk. I loghi di Salento.dev arrivano dall'addon tramite `<Logo>`.

## Regole visive

- **Una sola luce.** Etichette `.eyebrow` e link sono sempre cyan. Per il resto il cyan segna una sola idea per slide: la parola chiave del titolo (`<span class="cyan">`) e gli elementi che la sostengono (`.panel.on`, `.bar.on`, `.stat.cyan`). Se tutto è acceso, niente è acceso.
- **Ogni slide apre con un'etichetta** `.eyebrow` nel formato `NN · sezione` (`01 · eventi`). Copertina e chiusura usano `root@salento.dev · …`.
- **Layout.** Le slide senza `layout` usano `default`: contenuto in alto a sinistra, ed è normale che la parte bassa resti vuota. `layout: center` con `class: text-center` è per copertina, divisori di sezione, numeri grandi e chiusura.
- **Poco testo a schermo**: titolo breve, pannelli con una riga di testo. Il resto va nelle note (`<!-- … -->`).
- Solo scuro: niente sfondi chiari, salvo i riquadri bianchi per i loghi che lo richiedono.

## Catalogo

La tela è 980 × 552 px. Le classi di layout (`grid`, `gap-*`, `mt-*`, `text-sm`…) sono UnoCSS.

### Copertina e chiusura

```html
---
layout: center
class: text-center
---

<div class="eyebrow">root@salento.dev · talk #N</div>

<Logo class="h-44 mx-auto my-8" />

<h1 class="!text-4xl">Titolo, <span class="cyan">parola chiave</span></h1>

<p class="muted mono text-sm">Evento @ Comune · mese anno</p>
```

Per la chiusura: eyebrow `root@salento.dev · eof`, QR (`<img src="/qrcode.svg" class="w-[180px] mx-auto mt-8" />`) e contatti in `mono cyan`.

### Divisore di sezione

```html
---
layout: center
class: text-center
---

<div class="eyebrow">02 · whatsapp community</div>

# Dove succede <span class="cyan">tutto il resto</span>
```

### Pannelli

`.panel` è il blocco base, con bordo e staffe d'angolo. `.panel.on` accende le staffe di cyan. Dentro: `h3` per il titolo, `p` per una riga.

```html
<div class="grid grid-cols-2 gap-5 mt-8">
  <div class="panel"><h3>Titolo</h3><p>Una riga di spiegazione</p></div>
  <div class="panel on"><h3>Quello da ricordare</h3><p>Una riga di spiegazione</p></div>
</div>
```

Varianti già usate: `!py-2` / `!py-3` per pannelli bassi in elenco, `col-span-2` per un pannello largo, `.eyebrow !mb-2` come intestazione dentro il pannello. Un pannello può avere solo l'`h3`, per elenchi di parole chiave:

```html
<div class="grid grid-cols-4 gap-3 mt-8">
  <div class="panel !py-3"><h3>Web</h3></div>
  <div class="panel on !py-3"><h3>AI</h3></div>
</div>
```

### Numeri grandi

```html
<div class="grid grid-cols-4 gap-6 mt-12 max-w-4xl mx-auto">
  <div class="panel"><div class="stat">~18</div><p class="mt-2">eventi</p></div>
  <div class="panel on"><div class="stat cyan">~10</div><p class="mt-2">gruppi trasferta</p></div>
</div>
```

Accanto ad altro contenuto: `stat !text-4xl`.

### Pill (date, tag)

```html
<div class="panel !py-2"><span class="pill">nov 2025</span>&nbsp; <b>Meetup #0</b> · Taurisano</div>
<div class="panel on !py-2"><span class="pill on">ott 2026</span>&nbsp; <b>Lightning Night</b> · Taurisano <span class="cyan">← oggi</span></div>
```

### Timeline

```html
<div class="timeline mt-14 max-w-3xl">
  <div class="dot"></div>
  <div class="dot"></div>
  <div class="dot on"></div>
</div>

<div class="grid grid-cols-3 gap-6 mt-5 max-w-3xl">
  <div><p class="mono text-xs muted">12.11.2022</p><p class="text-sm mt-1">Primo passo</p></div>
  <div class="text-center"><p class="mono text-xs muted">13.11.2025</p><p class="text-sm mt-1">Secondo passo</p></div>
  <div class="text-right"><p class="mono text-xs cyan">oggi</p><p class="text-sm mt-1">Adesso</p></div>
</div>
```

### Barre orizzontali

Etichetta, barra, valore. La larghezza è in percentuale sul valore massimo.

```html
<div class="flex flex-col gap-4 mt-10 max-w-3xl">
  <div class="hbar"><span>2025</span><div class="bar" style="width:65.4%"></div><span class="val">~6.4K</span></div>
  <div class="hbar"><span>2026</span><div class="bar on" style="width:100%"></div><span class="val cyan">~9.7K</span></div>
</div>
```

Per confrontare due serie, due barre impilate nella stessa riga (`<div class="flex flex-col gap-[2px]">…</div>`) con la legenda `.key`.

### Colonne impilate

Una `.col` per periodo. Segmenti `.seg` dall'alto verso il basso, altezza in px rispetto all'altezza del grafico. `.tot` sopra la colonna (`&nbsp;` se vuoto), `.mo` sotto.

```html
<div class="flex gap-6 mt-2">
  <span class="key"><i class="s1"></i>Serie A</span>
  <span class="key"><i class="s2"></i>Serie B</span>
</div>

<div class="chart h-[215px] mb-8 mt-6">
  <div class="col"><div class="tot">&nbsp;</div><div class="seg s1" style="height:65px"></div><div class="mo">set<br><span>2025</span></div></div>
  <div class="col"><div class="tot">~1.5K</div><div class="seg s2" style="height:150px"></div><div class="seg s1" style="height:34px"></div><div class="mo">apr</div></div>
</div>
```

Colori delle serie: `s1` grigio, `s2` cyan, `s3` cyan chiaro.

### Screenshot

```html
<div class="grid grid-cols-2 gap-6 mt-8">
  <div>
    <img src="/screens/prima.png" class="shot" alt="…" />
    <p class="mono text-xs muted mt-3">didascalia · data</p>
  </div>
  <div>
    <img src="/screens/dopo.png" class="shot" alt="…" />
    <p class="mono text-xs cyan mt-3">didascalia · oggi</p>
  </div>
</div>
```

### Loghi dei partner

```html
<div class="grid grid-cols-7 gap-4 text-center">
  <div><img src="/partners/nome.png" class="partner-logo" alt="Nome" /><p class="partner-name">Nome</p></div>
  <div><div class="partner-logo partner-text">GDG<br>Lecce</div><p class="partner-name">GDG Lecce</p></div>
</div>
```

`partner-text` sostituisce un logo che manca. `!bg-white` per i loghi su fondo trasparente scuro.

### Due colonne

```html
---
layout: two-cols
layoutClass: gap-10
---

<div class="eyebrow">03 · sezione</div>

# Titolo

…

::right::

<div class="eyebrow">&nbsp;</div>
…
```

L'eyebrow vuoto a destra allinea le due colonne.

### Logo di Salento.dev

```html
<Logo class="h-16" />
<Logo variant="horizontal-cyan-on-dark" class="h-6" />
```

Varianti (`assets/logo/`):

- `stacked-symbol-white-on-dark` (predefinita): simbolo grande con "Salento Dev" su due righe accanto, per la copertina;
- `horizontal-white-on-dark`, `horizontal-cyan-on-dark`, `horizontal-dark-on-light` (su fondo bianco): su una riga, per spazi bassi;
- `compact-stacked-white-on-dark`: versione compatta;
- `pictogram-white-on-dark`: solo il simbolo.

## Variabili CSS

`--sd-cyan`, `--sd-dark`, `--sd-panel`, `--sd-bracket`, `--sd-muted`, `--sd-body`, `--sd-bright`: in [styles/index.css](styles/index.css).
