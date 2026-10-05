# Refleksion – Figma til kode

**Gruppemedlemmer:** Edyta Amanda Brzezinska og Richard Andersen Salcedo

## Sådan bruger I filen

Skriv jeres fælles refleksion direkte i denne fil. Erstat hjælpeteksterne med jeres egne erfaringer, og slet Markdown-guiden og demoen inden aflevering. Skriv kort og konkret, og brug eksempler fra jeres egen kode.

Åbn forhåndsvisningen i VS Code med **Cmd + Shift + V** (Mac) eller **Ctrl + Shift + V** (Windows). Så ser I, hvordan Markdown bliver vist. På GitHub vises formateringen automatisk, når I åbner filen.

### Mini-guide til Markdown

- `# Titel` er dokumentets hovedoverskrift. Brug kun én.
- `## Afsnit` og `### Underafsnit` giver overskrifter i flere niveauer.
- `**vigtig tekst**` bliver til **vigtig tekst**.
- En bindestreg efterfulgt af et mellemrum laver en punktopstilling som denne.
- Skriv kode inde i en sætning mellem enkelte backticks, fx `getTeamMembers()`.
- Links skrives sådan: `[Astros dokumentation](https://docs.astro.build/)`.
- Lav et nyt afsnit med en tom linje. Brug også en tom linje før og efter lister og kodeblokke.

En kodeblok starter og slutter med tre backticks. Skriv sproget efter de første, fx `js`, `css`, `html` eller `astro`. Se et eksempel i filens kildekode nedenfor.

### Kort demo – sådan kan tekst, kode og link kombineres

> Dette er et opdigtet eksempel på formen, ikke en færdig refleksion eller et ekstra krav.

Vi flyttede datahentningen til en fælles funktion, så endpointet kun skal vedligeholdes ét sted.

```js
export function getServices() {
  return apiFetch("https://ftk-api.pages.dev/services");
}
```

I komponenten kalder vi `getServices()`. Vi kontrollerede, at de samme servicetitler blev vist før og efter ændringen. Næste skridt er at undersøge, hvad der sker, hvis API'et returnerer en fejl.

Reference: [Datahentning i Astro](https://docs.astro.build/en/guides/data-fetching/).

---

## Eksempel 1: Skriv navnet på et valgt benspænd

### Hvor og hvorfor?

Hvor i løsningen bruger I teknikken, og hvilket konkret problem løser den? Henvis gerne til en fil, fx `src/components/MinKomponent.astro`.

### Relevant kode

Indsæt en kort kodeblok fra jeres løsning. Vælg det passende sprog, og forklar den del, der er vigtig for jeres valg.

### Afprøvning og ændringer

## Eksempel 1: Arbejde med Astro 

Første benspænd ift. temaopgaven, var at arbejde ved brug af Astro til vores opgave.

Opstartsfasen for projektet var et benspænd for os, fordi vi ikke har haft brugt Astro eller noget frameworks før til denne opgave.
Vores udfordring lå i at forstå hvordan opsætning foregik, samt lokalisere elementer og medier, og få siderne til at linke til hinanden. Vi forstod at hver side kunne have været bygget op i sections, som vi kunne dele op i, under components.

Heldigvis, fik vi ressourcer og andre hjælpemidler gennem klassekammerater, der havde videoer til os der var bagud i forståelsen for Astro.
Det hjalp også forståelsen for det, jo mere vi dykkede ind i bruget og arbejde med opsætningen til hjemmesiden.


- **Vi testede:** Beskriv situationen, fx en smal skærm, lang tekst eller tastaturbetjening.
- **Vi observerede:** Hvad skete der konkret?
- **Vi ændrede eller mangler:** Hvad rettede I, eller hvad vil være næste skridt?

## Eksempel 2: Donut Chart

Dette benspænd er omfattet vores donut chart som vi har på index.
Vi havde basis for vores donut chart og koden tilhørende. Det var en nem opbygning da vi havde noget statisk vi kunne vise som basis, men udfordringen var at finde frem til opbygning af animation til vores donut chart, når vi scroller ned til det eller når det vises frem på skærmen.

Vi undersøgte her igennem: [animation-timeline](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation-timeline)

Med animation-timeline fandt vi frem til at view() var den funktion vi skulle bruge:
view(): [animation-timeline: view()](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation-timeline/view)

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

## Eksempel 3: Skriv navnet på et valgt benspænd

Brug samme struktur som i eksempel 1: Hvor og hvorfor? Relevant kode. Afprøvning og ændringer.

## Fallback og robusthed

Dette må gerne indgå i de tre eksempler ovenfor. Hvis det allerede er dækket dér, kan I slette dette afsnit.

- **Fallback/progressive enhancement:** Beskriv mindst ét konkret eksempel. Hvad oplever brugeren med og uden understøttelse? Link til dokumentation for den valgte feature, og angiv de browsere og versioner, I har testet.
- **Defensive CSS:** Vis et konkret eksempel på, hvordan løsningen håndterer fx lang tekst eller lidt plads.
- **Global CSS og komponent-CSS:** Forklar kort, hvad I har placeret hvor, og hvorfor.

## Brug af AI

Hvis I har brugt AI til en væsentlig del af løsningen, så beskriv kort:

- Hvad brugte I den til?
- Hvad ændrede eller fravalgte I i svaret?
- Hvad lærte I, og hvordan kontrollerede I løsningen?

Hvis I ikke har brugt AI, kan I blot skrive det. I skal ikke indsætte en komplet chatlog.
