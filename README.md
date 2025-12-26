# Romaanimainen LaTeX-pohja (book, 130×198 mm)

Tämä LaTeX-pohja on tehty **pienikokoiseen romaanimaiseen proosataittoon** (trade paperback -henkinen), kaksipuolisena ja niin, että luvut alkavat oikealta sivulta. Lisäksi mukana on valmiit määritykset kirjan alkuun: **nimiösivu**, **kolofoni/tietosivu** sekä **sisällysluettelo ilman sivunumeroiden näyttöä**.

## Sisältö

- [Tavoite ja käyttötarkoitus](#tavoite-ja-käyttötarkoitus)
- [Kääntäminen](#kääntäminen)
- [Preamblen pääpiirteet](#preamblen-pääpiirteet)
  - [Dokumenttiluokka](#dokumenttiluokka)
  - [Kieli](#kieli)
  - [Fontit ja merkistöt](#fontit-ja-merkistöt)
  - [Sivukoko ja marginaalit](#sivukoko-ja-marginaalit)
  - [Sisällysluettelon asettelu](#sisällysluettelon-asettelu)
  - [Proosatypografia](#proosatypografia)
  - [Matematiikka](#matematiikka)
  - [Linkit](#linkit)
  - [Luvun otsikot](#luvun-otsikot)
  - [Sivunumerot ja alatunnisteet](#sivunumerot-ja-alatunnisteet)
  - [Tyhjät välisivut](#tyhjät-välisivut)
  - [Lainaus-/nostoblokki](#lainaus-nostoblokki)
- [Kirjan alku: nimiösivu, kolofoni ja sisällys](#kirjan-alku-nimiösivu-kolofoni-ja-sisällys)
  - [Nimiösivu + kolofoni titlepage-ympäristössä](#nimiösivu--kolofoni-titlepage-ympäristössä)
  - [Sisällysluettelo ilman sivunumeroita](#sisällysluettelo-ilman-sivunumeroita)
  - [Huomio: kappaleasetusten palautus](#huomio-kappaleasetusten-palautus)
- [Muokkausvinkkejä](#muokkausvinkkejä)
- [Tunnetut sudenkuopat](#tunnetut-sudenkuopat)

---

## Tavoite ja käyttötarkoitus

Pohja on tarkoitettu tilanteisiin, joissa halutaan:

- **pieni sivukoko**: 130×198 mm
- **kaksipuolinen taitto** (sisä-/ulkoreunamarginaalit)
- **romaanityyli**: kappaleet sisennetään, eikä käytetä kappalevälejä
- **hillitty ulkoasu**: sivunumerot ulkoreunoille, ei otsakeviivoja, linkit ilman värilaatikoita
- **hallittu sisällys**: pienempi fontti ja vähemmän ilmaa sisällysluettelossa
- **valmis etuosa**: nimiösivu + kolofoni + sisällys ilman sivunumeroita

---

## Kääntäminen

Pohja on tehty toimimaan pdfLaTeXilla.

- Suositus:
  - `pdflatex` → `pdflatex` (kahdesti, jotta sisällys päivittyy)
- Jos käytät viitteitä/indeksejä, tarvitset lisäksi `bibtex/biber` tai `makeindex`, mutta perusromaani ei yleensä tarvitse.

---

## Preamblen pääpiirteet

### Dokumenttiluokka

```tex
\documentclass[11pt,twoside,openright]{book}
```

- `11pt`: hieman ilmavampi leipäteksti.
- `twoside`: peilaa sivut (sisämarginaali/sidonta vs. ulkomarginaali).
- `openright`: luvut alkavat oikealta (parittomalta) sivulta.

### Kieli

```tex
\usepackage[finnish]{babel}
```

- Suomen kielen tavutus ja typografiset käytännöt.

### Fontit ja merkistöt

```tex
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc} % pdfLaTeX; LuaLaTeXissa ei tarvita
\usepackage{libertinus}
```

- `T1` + `utf8`: hyvä suomelle pdfLaTeXilla.
- `libertinus`: asettaa Libertinus-fontit.

### Sivukoko ja marginaalit

```tex
\usepackage[
  paperwidth=130mm,
  paperheight=198mm,
  inner=18mm,
  outer=15mm,
  top=18mm,
  bottom=22mm,
  headheight=14pt,
  headsep=8pt,
  footskip=10mm
]{geometry}
```

- Sivukoko trade paperback -tyyliin.
- Sisämarginaali hieman suurempi sidoksen takia.
- `headheight/headsep/footskip`: varmistavat, että alatunnisteet/otsakealueet mahtuvat ilman varoituksia.

### Sisällysluettelon asettelu

```tex
\usepackage{tocloft}
\setlength{\cftbeforechapskip}{2pt}
\renewcommand{\cftchapfont}{\small}
...
```

- Vähentää chapter-rivien väliä sisällyksessä.
- Pienentää sisällysluettelon fonttia (otsikot + sivunumerot) chapter/section/subsection -tasoille.

### Proosatypografia

```tex
\usepackage{microtype}
\usepackage{setspace}
\setstretch{1.05}
\setlength{\parindent}{1.5em}
\setlength{\parskip}{0pt}
```

- `microtype`: tasaisempi ladonta ja vähemmän ylitäyttöjä.
- Kevyt rivivälin lisäys (1.05).
- Romaanityyli: sisennys päällä, kappaleväli pois.

Lisäksi:

```tex
\clubpenalty=10000
\widowpenalty=10000
\displaywidowpenalty=10000
\emergencystretch=2em
```

- Estää leski-/orpo-rivejä ja helpottaa vaikeita rivinvaihtotilanteita.

### Matematiikka

```tex
\usepackage{amsmath, amssymb, amsthm}
\usepackage{mathtools}
```

- Mukana “varalta” – ei pakota käyttämään, mutta mahdollistaa siistin matematiikan, jos tarpeen.

### Linkit

```tex
\usepackage[hidelinks]{hyperref}
```

- Klikattavat viittaukset ilman värillisiä laatikoita.

### Luvun otsikot

```tex
\usepackage{titlesec}
\newcommand{\NoHyphens}{...}
\titleformat{\chapter}[display]{...}{\thechapter}{8pt}{...}
```

- Chapter-otsikoissa näkyy **vain lukunumero**, ei sanaa “Luku”.
- `\NoHyphens` estää otsikoiden tavutuksen (pitkät otsikot putoavat mieluummin seuraavalle riville sanaväleistä).

### Sivunumerot ja alatunnisteet

```tex
\usepackage{fancyhdr}
\fancypagestyle{plain}{ ... \fancyfoot[LE,RO]{\thepage} }
\pagestyle{fancy}
\fancyfoot[LE,RO]{\thepage}
```

- Sivunumero tulee **ulkoreunaan**:
  - parillisilla vasempaan alakulmaan (LE)
  - parittomilla oikeaan alakulmaan (RO)
- Ei otsakeviivaa (`headrulewidth=0pt`).

### Tyhjät välisivut

```tex
\usepackage{emptypage}
```

- `openright` voi tuottaa tyhjiä välisivuja. Tämä varmistaa, että ne ovat oikeasti tyhjiä (ei sivunumeroa).

### Lainaus-/nostoblokki

```tex
\usepackage[most]{tcolorbox}

\newtcolorbox{romaanilainaus}[1][]{
  breakable,
  frame hidden,
  borderline west={0.6pt}{0pt}{black!40},
  colback=white,
  left=12pt,
  ...
  fontupper=\itshape,
  #1
}
```

Käyttö:

```tex
\begin{romaanilainaus}
Tämä on romaanimainen lainaus tai nosto, jossa on vain vasen viiva.
\end{romaanilainaus}
```

---

## Kirjan alku: nimiösivu, kolofoni ja sisällys

Tässä osiossa kuvataan kirjan alkuun tulevat sivut ja miksi niissä tehdään tietyt määritykset.

### Nimiösivu + kolofoni titlepage-ympäristössä

Alla oleva rakenne tekee kaksi ensimmäistä sivua:

1) Nimiösivu (ei sivunumeroa)  
2) Kolofoni/tietosivu (ei sivunumeroa, pienempi fontti, ei sisennystä)

```tex
\begin{titlepage}
  \thispagestyle{empty}
  \centering

  \vspace*{0.18\textheight}

  {\fontsize{30}{36}\selectfont\bfseries
  Kirjan nimi\par}

  \vspace{0.6cm}

  {\Large\itshape
  Alaotsikko\par}

  \vspace{1.8cm}

  {\Large
  Kirjailija\par}

  \vfill

  {\small
  Kustantaja / Helsinki\par}

\newpage

% --- KOLOFONI / TIETOSIVU (kakkossivu) ---

  \thispagestyle{empty}
  \footnotesize
  \setlength{\parindent}{0pt}

  \vspace*{\fill}

  \textcopyright\ Kirjailija ja Kustantaja \the\year\ \par
  Kaikki oikeudet pidätetään.\par

  \vspace{1em}

  n:s painos 2025\par
  Painettu X:ssä\par
  Kustantaja\par
  ISBN XXX-XXX-XXXX-XX-X\par

  \vspace{1em}

  %Kannen suunnittelu: [nimi]\par
  %Taitto: [nimi]\par

  \vspace{1em}

  %\textit{[Mahdollinen motto / sitaatti / lyhyt huomautus]}\par

  \vspace*{1cm}
\end{titlepage}
```

**Miksi nämä määritykset:**
- `\thispagestyle{empty}`: poistaa sivunumeron ja ylätunnisteet kyseiseltä sivulta (nimiösivu/kolofoni).
- `\centering`: keskittää nimiösivun typografian.
- `\fontsize{30}{36}\selectfont`: otsikko kontrolloidulla koossa (30pt fontti, 36pt riviväli).
- Kolofonissa:
  - `\footnotesize`: pienempi tekstikoko
  - `\setlength{\parindent}{0pt}`: kolofoni on usein “luettelomainen”, ilman kappalesisennystä
  - `\vspace*{\fill}`: työntää kolofonin tekstiblokin sivun alaosaan “kirjamaisesti”.

### Sisällysluettelo ilman sivunumeroita

Seuraava ryhmä tekee sisällyksen ja varmistaa, ettei sisällyssivuilla näy sivunumeroa (myöskään ensimmäisellä, joka on usein `plain`-tyyliä).

```tex
% sislu, sivunumeroa ei näytetä
\begingroup
  \pagestyle{empty} % myös mahdolliset seuraavat TOC-sivut tyhjiksi

  \makeatletter
  \let\ps@plain\ps@empty % TOC:n eka sivu (plain) => empty
  \makeatother

  \tableofcontents
  \cleardoublepage
\endgroup
```

**Miksi näin:**
- `\pagestyle{empty}`: asettaa ryhmän sisällä sivutyylin tyhjäksi.
- `\let\ps@plain\ps@empty`: “huijaa” `plain`-sivutyylin (jota LaTeX käyttää usein TOC:n ekalla sivulla) käyttäytymään kuten `empty`.
- `\begingroup...\endgroup`: varmistaa, että muutos koskee vain sisällystä, eikä sotke muun dokumentin sivutyylejä.

### Huomio: kappaleasetusten palautus

Kolofonissa asetetaan:

```tex
\setlength{\parindent}{0pt}
```

Koska kolofoni on `titlepage`-ympäristön sisällä, tämä saattaa vaikuttaa myös sen jälkeen tulevaan tekstiin, jos arvo jää voimaan.

**Turvallinen käytäntö:** palauta proosa-asetukset heti etuosan jälkeen ennen varsinaista tekstiä:

```tex
\setlength{\parindent}{1.5em}
\setlength{\parskip}{0pt}
```

Jos käytät myöhemmin erillisiä etuosasivuja (esim. omistuskirjoitus, esipuhe), voi olla fiksua tehdä niille omat ryhmäykset (`\begingroup...\endgroup`) tai omat tyylikomennot.

---

## Muokkausvinkkejä

- **Sivukoko / marginaalit:** säädä `geometry`-paketin arvoja.
- **Riviväli:** `\setstretch{1.0}` tiukemmaksi tai `1.1` ilmavammaksi.
- **Sisällyksen fonttikoko:** vaihda `\small` → `\footnotesize`, jos haluat vielä pienemmän.
- **Chapter-otsikon koko:** `\Huge` → `\LARGE` tai muuta `\titlespacing*`-arvoja.
- **Lainausblokki:** poista kursiivi poistamalla `fontupper=\itshape`.

---

## Tunnetut sudenkuopat

1) **pdfLaTeX vs LuaLaTeX**
- `\usepackage[utf8]{inputenc}` on pdfLaTeXille; LuaLaTeXissa sitä ei yleensä tarvita.
- Jos vaihdat moottoria, fonttiasetukset kannattaa arvioida uudelleen.

2) **Kolofonin kappaleasetukset**
- Jos huomaat, että leipätekstin sisennys katoaa titlepage-osion jälkeen, palauta `\parindent` ja `\parskip` heti sisällyksen jälkeen.

3) **Sisällyksen sivutyylit**
- `\let\ps@plain\ps@empty` on tarkoituksella ryhmän sisällä; älä nosta sitä globaaliksi, ellei tavoite ole poistaa `plain`-sivutyyli koko dokumentista.

---

## Esimerkkirunko (minimaalinen)

```tex
\begin{document}

% --- Titlepage + kolofoni ---
% (liitä titlepage-blokki tähän)

% --- Sisällys ilman sivunumeroita ---
% (liitä begingroup...endgroup -blokki tähän)

% Palauta proosa-asetus tarvittaessa
\setlength{\parindent}{1.5em}
\setlength{\parskip}{0pt}

\chapter{Ensimmäinen luku}
Tässä alkaa varsinainen teksti...

\end{document}
```
