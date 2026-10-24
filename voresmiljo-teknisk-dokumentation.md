# Vores Miljø (voresmiljo.dk) — Teknisk Dokumentation & Kildekodeoverblik

Dette dokument er et komplet teknisk øjebliksbillede af kildekoden, arkitekturen, filstrukturen og designsystemet for webprojektet **Vores Miljø** (`voresmiljo/voresmiljo.github.io`). Dokumentet er struktureret til brug som videnskilde i AI-systemer og analyseredskaber (f.eks. NotebookLM).

---

## 1. Hovedfakta & Teknisk Arkitektur

* **Website-navn:** Vores Miljø
* **Domæne:** [https://voresmiljo.dk](https://voresmiljo.dk)
* **Kildekode-lager (Git Repository):** `voresmiljo/voresmiljo.github.io`
* **Arkitekturtype:** 100 % statisk website (Static Site).
* **Hosting:** GitHub Pages med custom domain (`CNAME: voresmiljo.dk`).
* **Sprog & Tegnsæt:** Dansk (`lang="da"`), UTF-8 encoding.
* **Build-værktøjer / Dependencies:** Ingen node.js, npm, bundlers, compilers eller eksterne frameworks. Alle filer leveres som ren, semantisk HTML5, CSS3 og vanilla JavaScript direkte til browseren.

---

## 2. Designsystem, CSS & Typografi

### 2.1 CSS-arkitektur: Intet CSS-framework (Ingen Tailwind)
Der anvendes **ikke Tailwind CSS**, Bootstrap eller andre CSS-frameworks. Sitet benytter et specialbygget, modulært designsystem baseret på CSS Custom Properties (variabler), primært defineret i `site.css`.

### 2.2 Farvepalette (CSS Variabler)
Paletten er dæmpet, naturinspireret og professionel med fokus på høj kontrast og god læsbarhed:
```css
:root {
  --earth: #2C3E2D; /* Dyb skovgrøn — anvendes til primær tekst, mørke baggrunde og footers */
  --moss:  #4A6741; /* Mellemgrøn / mos — anvendes til links, sektionsetiketter og fremhævelser */
  --stone: #8B9E7F; /* Lys mos-sten — anvendes til sekundære etiketter, rammer og knaphover */
  --sand:  #E8E0D0; /* Varm sand — kontrastfarve til tekst på mørk baggrund og lette borderlinjer */
  --cream: #F4F0E8; /* Sand-creme — anvendes til highlight-bokse, infopaneler og relaterede links */
  --light: #FAFAF7; /* Brækket hvid — primær baggrundsfarve for hele websitet */
}
```

### 2.3 Typografi
Fontene indlæses via Google Fonts (`fonts.googleapis.com`):
* **Overskrifter og logo (`h1`, `h2`, `h3`, `.logo`):** `'Playfair Display', serif`
* **Brødtekst (`body`, `p`, `li`):** `'Source Serif 4', Georgia, serif` (basisstørrelse: 18px, linjehøjde: 1.75–1.8).
* **Juridiske skabeloner & kodefelter:** `Georgia, serif` med faste linjehøjder (`line-height: 1.6`) og mørk kontrast (`#111111`) for at sikre, at tekst let kan markeres og kopieres fejlfrit.

### 2.4 Centrale UI-komponenter og CSS-klasser i `site.css`
* `.wrap` & `.wrap-narrow`: Centrale layouts med henholdsvis `max-width: 1200px` og `max-width: 850px`.
* `.site-header`: Standard mørk header (`background: var(--earth)`).
* `.site-header.hero`: Udvidet forsidehero (`min-height: 78vh`) med grid-layout (`grid-template-rows: auto 1fr`).
* `.hero-label` & `.section-label`: Små, spærrede overskrifter i versaler (`font-size: 0.75rem`, `letter-spacing: 0.2em`, `text-transform: uppercase`).
* `.btn`, `.btn-outline`, `.btn-copy`: Standardknapper og interaktive kopieringsknapper.
* `.fold-list` & `details.fold`: Tilpassede HTML `<details>` elementer med subtile rammer, etiketter og statusnoter.
* `.template-panel`: Tekstpaneler til rå juridiske tekstskabeloner.
* `.breadcrumb`: Brødkrummenavigation.
* `.grid-2` & `.card`: Responsivt 2-kolonners gitter til sektioner og sagsarkiver.

---

## 3. Komplet Fil- og Mappeoversigt

Nedenfor er samtlige filer i projektet grupperet efter funktion:

### 3.1 Rod- og konfigurationsfiler
* `CNAME`: Indeholder linjen `voresmiljo.dk`, som dirigerer GitHub Pages til det officielle domæne.
* `robots.txt`: Aktuel konfiguration blokerer generelle søgemaskiner (Google, Bing) med `Disallow: /`, men tillader AI-crawlere (GPTBot, ClaudeBot, PerplexityBot m.fl.) adgang.
* `sitemap.xml`: Midlertidigt tom URL-liste under udvikling/pre-launch.
* `sitemap.ready.xml`: Færdiggjort XML sitemap med alle aktive URL'er, klar til at erstatte `sitemap.xml` ved officiel lancering.
* `llms.txt`: Struktureret dokumentation i ren tekst designet specifikt til LLM-agenter, som opsummerer sitets formål, nøglesider og retningslinjer.
* `google384694f52337980b.html`: Verifikationsfil til Google Search Console.

### 3.2 Hovedsider (Moderne layout baseret på `site.css`)
* `index.html`: Forsiden. Indeholder en præsentation af projektet, 2×2 sektionsgrid til værktøjskassen, genveje til processen, seneste sagsbelysninger og direkte links til kontakt.
* `vaerktoejskasse.html`: Værktøjskassen med 4 udfoldelige sektioner og integrerede tekstskabeloner til download/kopi:
  1. Anmodning om aktindsigt
  2. Struktureret høringssvar
  3. Formelt klageskrift
  4. Tjekliste til Bilag 6-screeninger
* `vejviser.html`: Den samlede procesguide ("Processen"), som gennemgår miljøvurderingslovens faser (screening, offentlighedsfase/høring og klageproces).
* `sagsarkiv.html`: Samlet arkiv og sagsportal over konkrete miljøsager og klageafgørelser.
* `om.html`: Information om personerne/fagligheden bag projektet, præcisering af at der ydes frivillig hjælp og ikke kommerciel rådgivning, samt kontaktformular/indsendelse af sagsakter (`kontakt@voresmiljo.dk`).

### 3.3 Sagsanalyser (Konkrete cases)
* `sag-sanderoedgaard.html`: Dybdegående analyse af Sanderødgård Grusgrav (screening, grundvandsbeskyttelse, PFAS, manglende kumulation og retlig belysning).
* `sag-falkenberg.html`: Sagsanalyse af lokalplan 4.47 og kommuneplantillæg for Falkenberg Jorde (idrætsanlæg, naturpåvirkning, støj og processuelle fejl).
* `sag-koppers.html`: Principiel afgørelse om Koppers-grunden i Nyborg (udledning til Nyborg Fjord, blandingszoner og krav til tilstrækkeligt vidensgrundlag).
* `sag-skaerbaekvaerket.html`: Analyse af Miljø- og Fødevareklagenævnets hjemvisning af Skærbækværkets udledningstilladelse til Kolding Fjord.

### 3.4 Fagguides (Legacy-dokumenter med intern `<style>`-blok)
* `vvm-screening.html`: Teknisk og juridisk fagguide om VVM-screening, screeningskriterier og krav til anmelder.
* `miljoegodkendelser.html`: Gennemgang af godkendelsespligtige virksomheder (listevirksomheder), BAT-konklusioner og vilkår.
* `spildevandstilladelser.html`: Retningslinjer for spildevandsudledning, recipientforhold og vandrammedirektivet.
* `raastoftilladelser.html`: Regler for råstofindvinding, grave- og efterbehandlingsplaner samt grundvandshensyn.
* `hoeringssvar.html`: Detaljeret faglig guide til borgeres og foreningers udarbejdelse af saglige høringssvar.
* `faq.html`: Ofte stillede spørgsmål om gratis hjælp, kapacitet og projektets rammer.

### 3.5 Omdirigeringssider (Redirects)
Disse sider indeholder `meta http-equiv="refresh"` samt kanoniske tags for at håndtere ældre URL-strukturer:
* `kontakt.html` → omdirigerer til `om.html`
* `afgørelser.html` → omdirigerer til `sagsarkiv.html`
* `miljoevurderinger.html` → omdirigerer til `vejviser.html`
* `sagsarkiv-sanderoedgaard.html` → omdirigerer via JavaScript og link til `sag-sanderoedgaard.html`

### 3.6 Mappen `assets/`
* `assets/dokumenter/`:
  * `README.md`: Fortegnelse over tilknyttede sagsakter.
  * `miljoegodkendelse.pdf`: Konkret miljøgodkendelsesakt.
  * `sanderoedgaard-forureningsundersoegelse.pdf`: Forureningsundersøgelse vedr. Sanderødgård.
  * `falkenberg/klage-lokalplan-447-falkenberg-jorde-kommuneplantillaeg-24-13aug2026.pdf`: Klageskrift indgivet til Planklagenævnet.
* `assets/skabeloner/`:
  * `README.md`: Dokumentation for planlagte `.docx`-skabeloner (`anmodning-om-aktindsigt.docx`, `struktureret-hoeringssvar.docx`, `formelt-klageskrift.docx`).

---

## 4. Klient-side JavaScript & Interaktive Funktioner

Al interaktivitet er skrevet i ren vanilla JavaScript uden eksterne biblioteker:

### 4.1 Kopiering af skabeloner (`vaerktoejskasse.html`)
Lytter på klik på `.btn-copy` knapper:
```javascript
document.querySelectorAll('.btn-copy').forEach(function (btn) {
  btn.addEventListener('click', async function (e) {
    e.preventDefault();
    e.stopPropagation();
    var target = document.getElementById(btn.getAttribute('data-target'));
    if (!target) return;
    var copyText = ('value' in target) ? target.value : (target.innerText || target.textContent);
    try {
      await navigator.clipboard.writeText(copyText);
      var original = btn.textContent;
      btn.textContent = 'Kopieret';
      btn.classList.add('is-copied');
      setTimeout(function () {
        btn.textContent = original;
        btn.classList.remove('is-copied');
      }, 2000);
    } catch (err) {
      if (target.select) { target.focus(); target.select(); }
      btn.textContent = 'Markér teksten og kopiér (Ctrl/Cmd+C)';
    }
  });
});
```

### 4.2 Harmonika / Accordion Logik (`vaerktoejskasse.html`)
Sikrer at:
1. Alle folder (`details.fold`) lukkes eksplicit ved start, selv hvis browseren har cachet åben status.
2. Når én fold åbnes (`toggle`-event), lukkes alle øvrige folder automatisk, så brugeren kun præsenteres for ét aktivt værktøj ad gangen.
3. Elementer med `[data-exclusive]` holdes gensidigt udelukkende.

---

## 5. Strukturerede Data & SEO-standarder (JSON-LD)

Projektet implementerer Schema.org specifikationen via `<script type="application/ld+json">` på alle primære sider. Typiske objekter omfatter:

1. **Organization (`Schema.org/Organization`):**
   * Navn: `Vores Miljø`
   * URL: `https://voresmiljo.dk/`
   * E-mail: `kontakt@voresmiljo.dk`
   * Beskrivelse: Uafhængigt, frivilligt og ikke-kommercielt fagligt projekt om miljøvurderinger, VVM, høringssvar og sagsbelysning.
   * `knowsAbout`: `["miljøvurdering", "VVM-screening", "høringssvar", "miljøklage", "Bilag IV-arter", "drikkevandsbeskyttelse"]`.

2. **WebSite (`Schema.org/WebSite`):**
   * Angiver overordnet site-definition med sprogangivelse `da-DK`.

3. **WebPage (`Schema.org/WebPage`):**
   * Specificerer sidens individuelle kanoniske URL, titel og beskrivelse.

---

## 6. Nuværende Status & Klargøring til Offentliggørelse

Websitet er i øjeblikket i en **pre-launch fase**:
1. **Robots & Indeksering:**
   * HTML-hovederne indeholder `<meta name="robots" content="noindex, nofollow">`.
   * `robots.txt` har `Disallow: /` for de fleste søgemaskiner.
   * `sitemap.xml` er midlertidigt tom.
2. **Klargøringstrin ved officiel lancering:**
   * Erstat `noindex, nofollow` med `index, follow` i HTML-filerne.
   * Åbn `robots.txt` for almindelig indeksering.
   * Kopiér indholdet fra `sitemap.ready.xml` til `sitemap.xml`.
   * Ensret de ældre fagguides (`vvm-screening.html`, `miljoegodkendelser.html`, `spildevandstilladelser.html`, `raastoftilladelser.html`, `faq.html`) til at bruge `site.css` i stedet for inline `<style>`.
