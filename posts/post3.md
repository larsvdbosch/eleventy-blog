---
layout: home.njk
title: 11ty blog
date: 2024-10-20
---

**11ty blog voor documentatie**

Omdat ik deze periode gerust een “Javascript periode” mag noemen, heb ik natuurlijk ook meegedaan aan de coding sessies van Tjerk en Jop. Het leek mij ideaal om elke week vast wat inspiratie op te doen tijdens deze colleges. 

Tijdens de verschillende colleges heb ik uitleg gekregen over 11ty: Een static site generator die eenvoudig verschillende pagina’s kan maken met een vaste styling. Hierdoor heb ik mezelf niet steeds hoeven herhalen, wat ook vaker is terugkomen bij mijn verkregen feedback over het DRY-principe. Het leek mij een ideale kans om te leren werken met 11ty en een blog op te stellen voor documentatie. Hiermee toon ik aan dat ik niet alleen een blog kan programmeren, maar ook actief kan bijhouden voor documentatie en notities. Om dit gelijk te gebruiken voor het assessment, heb ik gekozen om mijn coding projecten hier ook op te documenteren. Alles is natuurlijk in een pdf document geplaatst, maar deze coding projecten heb ik dubbel uitgetypt op mijn persoonlijke blog.

**Het begin**

Ik ben begonnen met 11ty tijdens het “how-to-build-a-blog” college. Tjerk heeft in principe de basics van 11ty voorgedaan op het scherm zodat duidelijk werd hoe je de bestandsstructuur moet indelen, hoe je de terminal efficient kunt gebruiken en hoe je 11ty kunt runnen zodat er een local_host pagina wordt geladen die je live kunt bekijken. Er waren een aantal pagina’s in de projectmap die ik nog niet eerder heb gezien of nog niet eerder van had gehoord. Met 11ty gebruik je namelijk ook HTML & CSS, maar ook .md en .njk files. Ik had niet precies in de gaten waarom deze files in map werden geplaatst, maar tijdens het laden van de 11ty directory met de terminal worden al deze files automatisch al toegevoegd.

Markdown (.md) zorgt ervoor dat je eenvoudige content kunt schrijven met een vereenvoudigde syntax. Je bent dus nog minder tijd kwijt aan het schrijven van de html. Dit staat eerst nog los van de styling (CSS). Je bent dus in staat om het gehele proces eenvoudiger te maken waardoor je minder hoeft te herhalen en efficienter te werk gaat:

```md
---
layout: home.njk
title: Lars' Documentation
---

# Hi! My name is Lars. Welcome to my blog 👋

<h2>I made a personal blog to collect some documentation of my coding projects</h2>

<ul>
<li><a href="/posts/">Collection of my posts</a></li>
</ul>
```

Nunjucks (.njk) is een styling template die ervoor zorgt dat de HTML een vaste indeling heeft. Zo kan je alle content die je op een site wilt hebben, alvast op volgorde zetten. In mijn geval bij het maken van een blog, had ik navigatie, een titel van de blogpost en de inhoud van de blog nodig als vaste elementen voor een vooraf bepaalde layout.

Front-matter zorgt ervoor dat je simpele data kunt definieren zodat je die steeds kan herhalen op elke pagina van je blog. Voor een blog is dit vaak de titel, de datum van het schrijven van de post en een layout-file die ik dus al gemaakt had in de .njk file.
```md
---
layout: home.njk
title: Intro opdracht bibliotheek
date: 2024-10-19
---
```

De 3 streepjes boven en onder, geven aan dat de content hierbinnen de front-matter is.

**De code**

Naast het gebruiken van de 11ty files, heb ik nog een extra feature toegevoegd waardoor ik net zoals in Notion en Obsidian, kan verwijzen naar code in een mooi contentblok met een eigen gekozen VS Code thema. Ik heb gebruik gemaakt van Prism.js, een syntax highlighting library die ervoor zorgt dat je kan refereren naar allerlei soorten code. Ik heb dit als volgt gedaan:

Ik heb in de eleventy javascript file aangegeven dat de prism.js plugin moet worden ingeladen om syntax highlighting voor elkaar te krijgen op de blog. In de docs van eleventy stond een duidelijk stuk over syntax highlighting en hier werd ook uitgelegd welke code moest worden toegevoegd om de prism.js library in te laden: Ik heb dit vervolgens in mijn .eleventy.js file getypt:

```js
const syntaxHighlight = require("@11ty/eleventy-plugin-syntaxhighlight");

module.exports = function(eleventyConfig) {
  // toevoegen van prism.js
  eleventyConfig.addPlugin(syntaxHighlight);

  eleventyConfig.addPassthroughCopy("css");
  
  eleventyConfig.addCollection("posts", function(collection) {
    return collection.getFilteredByGlob("./posts/*.md").reverse();
  });

  return {
    dir: {
      input: ".",
      includes: "_includes",
      output: "_site"
    }
  };
};
```

Wat ik erg leuk vond was het personaliseren van de style van de syntax highlighting. Prism.js heeft de keuze om te kiezen uit bestaande VS Code thema’s die je kunt downloaden van hun website in een .css file. Het enige wat ik moest doen was het thema linken in de head van de HTML, als css file.

```html
<link rel="stylesheet" href="/css/prism-shades-of-purple.css">
```

**Conclusie**

Ik heb door het maken en bijhouden van deze blog, geleerd hoe ik efficient een statische website kan maken. Ik heb nu zelf ervaren hoe fijn het is om rekening te houden met het DRY-principe en snap nu ook waarom dit zo’n bekend principe is binnen ons vakgebied. 

Zodra je alle basics hebt opgesteld, zoals layouts en stylings, kun je gemakkelijk de pagina dupliceren om vervolgens nieuwe content te schrijven met dezelfde styling en layout. 

Dit is dus echt ideaal voor een blog of portfolio, maar is niet voor elke website handig om te gebruiken. Dit is echter de eerste keer voor mij dat ik heb gewerkt met “componenten en variabelen” op een website. In Figma kende ik dit principe al, maar met code had ik dit nog nooit gedaan.

