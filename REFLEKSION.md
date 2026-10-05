# Refleksion – Figma til kode

**Gruppemedlemmer:** Edyta Amanda Brzezinska og Richard Andersen Salcedo

## Eksempel 1: Arbejde med Astro 

Første benspænd ift. temaopgaven, var at arbejde ved brug af Astro til vores opgave.

Opstartsfasen for projektet var et benspænd for os, fordi vi ikke har haft brugt Astro eller noget frameworks før til denne opgave.
Vores udfordring lå i at forstå hvordan opsætning foregik, samt lokalisere elementer og medier, og få siderne til at linke til hinanden. Vi forstod at hver side kunne have været bygget op i sections, som vi kunne dele op i, under components.

Heldigvis, fik vi ressourcer og andre hjælpemidler gennem klassekammerater, der havde videoer til os der var bagud i forståelsen for Astro.
Det hjalp også forståelsen for det, jo mere vi dykkede ind i bruget og arbejde med opsætningen til hjemmesiden.

En del af forståelsen for Astro var også den måde man kunne tilgå forskellige undersider, istedet for bruget af den måde man er vant til. Normal vis hvis man skal til Kontaktsiden kunne man skrive feks. "pages/contact.html", men Astro har en anden tilgang til det. Til index skulle man så tilgå den med bare "/" og de andre respektive sider såsom "/taxes" osv.

Vores kodestykke til menuen:

```html 
    <div class="menu">
      <a href="/">Home</a>
      <a href="/taxes">Case Studies</a>
      <!-- filepath: src/components/header.astro -->
      <a href="/team">Team</a>
      <a href="/about">About</a>
    </div>
```

## Eksempel 2: Donut Chart

Dette benspænd er omfattet vores donut chart som vi har på index.
Vi havde basis for vores donut chart og koden tilhørende. Det var en nem opbygning da vi havde noget statisk vi kunne vise som basis, men udfordringen var at finde frem til opbygning af animation til vores donut chart, når vi scroller ned til det eller når det vises frem på skærmen. I første omgang havde vi en animation når man hover over vores elementer, men vi erstattede kodestykker for at få det til at fungere når vi scroller ned til sektionen.

Dette kodestykke fjernede vi:

```css
{
  transition: --progress 1s;
  
  &:hover {
    --progress: var(--value);
  }
}
```

Vi undersøgte her igennem: [animation-timeline](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation-timeline)

Med animation-timeline fandt vi frem til at view() var den funktion vi skulle bruge:
view(): [animation-timeline: view()](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation-timeline/view)

Key kodestykke der havde betydning for animationen:

```css
{
    animation: fillDonut 10s ease forwards;
    animation-timeline: view();
    animation-range: entry 40% entry 100%;
}
```

Donut Chart uden animation

```css
  figure {
    flex: 0 1 150px;
    min-inline-size: 0;
    text-align: center;
    margin-left: 10px;
    margin-right: 10px;

    --value: attr(data-value type(<number>));
    --value-string: attr(data-value);
    --value-percent: attr(data-value %);

    container: circle / inline-size;
    display: grid;
    grid: "stack";
    place-items: center;

    &::after {
      content: var(--value-string) "%";
      grid-area: stack;
      font-size: 25cqw;
      font-weight: 600;
    }
  }
```

Donut Chart med animation

```css
@property --progress {
    syntax: "<number>";
    inherits: true;
    initial-value: 0;
  }

  figure {
    flex: 0 1 150px;
    min-inline-size: 0;
    text-align: center;
    margin-left: 10px;
    margin-right: 10px;

    --value: attr(data-value type(<number>));
    --progress: 0;

    container: circle / inline-size;
    display: grid;
    grid: "stack";
    place-items: center;

    animation: fillDonut 10s ease forwards;
    animation-timeline: view();
    animation-range: entry 40% entry 100%;

    &::after {
      counter-reset: percentage round(var(--progress));
      content: counter(percentage) "%";

      grid-area: stack;
      font-size: 25cqw;
      font-weight: 600;
    }
  }

  @keyframes fillDonut {
    from {
      --progress: 0;
    }

    to {
      --progress: var(--value);
    }
  }
```

## Eksempel 3: Netlify

Da Netlify, branching og GitHub stadig er ret nyt for os, har vi haft nogle udfordringer med at få det hele til at fungere helt, som vi gerne ville. Vi har blandt andet oplevet, at nogle billeder og andre medier ikke bliver loadet eller vist på siden, når den ligger på Netlify. Vi har prøvet at gå vores stier igennem flere gange, men så vidt vi kan se, burde de være rigtige.

Vi har også haft problemer med vores donut chart, som virker fint, når vi kører siden lokalt på vores egne computere, men som ikke virker på Netlify. Vi har prøvet forskellige løsninger og kigget koden igennem flere gange, men vi har ikke rigtig kunne finde frem til, hvad problemet er, da selve koden ser ud til at være rigtig.

Vi har derfor brugt en del tid på at prøve at finde og rette fejlene, men til sidst måtte vi lidt acceptere, at vi ikke kunne finde en løsning på det. Det er helt klart noget, vi stadig skal blive bedre til og have mere erfaring med, især når det kommer til GitHub, branching og Netlify.

## Fallback og robusthed

Dette må gerne indgå i de tre eksempler ovenfor. Hvis det allerede er dækket dér, kan I slette dette afsnit.

- **Fallback/progressive enhancement:** Beskriv mindst ét konkret eksempel. Hvad oplever brugeren med og uden understøttelse? Link til dokumentation for den valgte feature, og angiv de browsere og versioner, I har testet.
- **Defensive CSS:** Vis et konkret eksempel på, hvordan løsningen håndterer fx lang tekst eller lidt plads.
- **Global CSS og komponent-CSS:** Forklar kort, hvad I har placeret hvor, og hvorfor.

## Brug af AI

Vi har undervejs i projektet brugt AI som en form for sparringspartner i vores kodearbejde. Det har især været, når vi er stødt på metoder, CSS eller andre dele af koden, som vi ikke helt har forstået.

Da der har været rigtig meget ny information og mange nye ting, vi skulle lære og forholde os til, har vi nogle gange haft brug for at få tingene forklaret på en anden måde. Her har vi brugt AI til at genforklare forskellige metoder og kodestykker, så vi bedre kunne forstå, hvad de gjorde, og hvordan de kunne bruges.

I nogle tilfælde har AI også givet eksempler på kode eller forslag til en løsning. Her har vi brugt det som hjælp til at komme videre og derefter arbejdet med koden selv. AI har altså mest været et værktøj til sparring og til at hjælpe os med de ting, vi havde svært ved at forstå.

