# Convertire una presentazione esistente

Obiettivo: portare tutto il **contenuto** dell'originale in `SCALETTA.md` (testo, dati, note, immagini), una sezione per slide originale. Il layout non si traduce: si rifà con il catalogo dell'addon. Cosa tenere nel tempo del talk si decide dopo, nelle bozze.

Il passo è completo quando ogni slide dell'originale ha la sua sezione in scaletta, note comprese, e ogni immagine da riusare è in `public/`.

Lavora sui file estratti in una cartella fuori dal repo. In `public/` del talk copia solo le immagini che userai, con nomi descrittivi e in sottocartelle (`screens/`, `partners/`, `photos/`…).

## Per formato

**Keynote**: File › Esporta in › PowerPoint, poi come pptx.

**Google Slides**: File › Scarica › Microsoft PowerPoint (.pptx), poi come pptx.

**pptx**: se hai una skill per i pptx, usala. Altrimenti:

- testo e note: `python3 -m markitdown file.pptx` (pacchetto `markitdown`) oppure `python-pptx` (`slide.shapes` per il testo, `slide.notes_slide` per le note);
- immagini: il pptx è uno zip, `unzip -o file.pptx 'ppt/media/*' -d <cartella>`;
- per vedere com'era ogni slide: esporta in PDF e usa `pdftoppm` come sotto.

**pdf**: le note di solito non ci sono; chiedile allo speaker.

- testo: `pdftotext -layout file.pdf -`
- immagini incorporate: `pdfimages -png file.pdf <cartella>/img`
- una PNG per pagina, da guardare: `pdftoppm -png -r 80 file.pdf <cartella>/pag`

**Slidev**: parti da `slides.md` e segui le slide incluse con `src:`. Altri file `.md` nella cartella (per esempio `pages/`) possono essere bozze o contenuti mai inclusi: chiedi allo speaker se fanno parte del talk. I file che iniziano con `_` di solito sono template. I componenti e i layout del tema originale qui non esistono: si sostituiscono con i pattern del catalogo.

## Note dello speaker

Se l'originale non ha note (succede con pdf e spesso con Slidev), ricavale dal testo delle slide e segnale `?` in scaletta: lo speaker le rivede.

## Cosa portare in scaletta

- Testo e dati di ogni slide, con l'origine (`da: slide 4` o `da: pages/principi.md`).
- Grafici e tabelle: i dati, non la forma. Il pattern (barre, colonne, numeri grandi) si sceglie in bozza.
- Immagini: riusale solo se lo speaker ha il diritto di farlo (proprie, del brand, con licenza). Altrimenti segnale `📷` da sostituire.
- Link, QR e date: segnali `?`, perché nell'originale possono essere scaduti.
