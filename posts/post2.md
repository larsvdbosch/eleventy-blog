---
layout: home.njk
title: Boekwebsite
date: 2024-10-19
---

**Boeken website met javascript**

In de eerste 2 weken van dit semester ben ik begonnen met een accessibility opdracht die ik op verschillende moeilijkheden kon uitwerken. Ik heb gekozen om het design in Figma te programmeren aan de hand van HTML, CSS & Javascript, omdat ik vanaf dag 1 al wist dat ik de volle focus ging leggen op het programmeren met Javascript. Deze opdracht heeft veel overeenkomsten met het programmeren binnen een (semi)groot bedrijf. De meeste bedrijven die websites bouwen hebben verschillende afdelingen met elk hun eigen specialisatie. Als programmeur krijg je vaak een high fidelity prototype aangeleverd vanuit het UX/UI team. De taak is dan om het prototype om te zetten in code om er vervolgens een website mee te programmeren. In mijn geval heb ik dus een website geprogrammeerd aan de hand van een prototype in Figma. Tijdens het programmeren heb ik rekening gehouden met de accessibility van de website, responsive maken en de functionaliteit van buttons werkend maken met Javascript.

**Wat is er gedaan?**

Om te beginnen heb ik deze opdracht samen met Niels uitgevoerd. We hebben met elkaar samengewerkt, maar wel beide onze eigen website geprogrammeerd met uiteindelijk hetzelfde resultaat. Het is dus niet dat we de website op 1 laptop hebben gebouwd, want dan ga je snel meekijken i.p.v. dat je zelf de code gaat typen en begrijpen. Het voordeel is wel dat Niels al best veel ervaring had met Javascript. Hij heeft mij dus in zekere zin goed begeleid, maar wel op een lerende manier. Niels had wel in de gaten dat hij af en toe voorzetjes moest geven, maar niet de code zelf moest typen. Soms vond ik wel dat Niels iets te snel ging, dus dan vroeg ik aan hem wat we nou precies aan het doen waren en wat een bepaald stuk code inhield.

Voordat we begonnen met programmeren, hebben we naar het Figma design gekeken.

In dit design was al goed gewerkt met componenten en variabelen, zodat wij ook goed wisten wat er interactief gemaakt moest worden.

Om te beginnen heb ik geleerd hoe ik een button active kan maken, met als gevolg dat er bepaalde content onzichtbaar wordt gemaakt. Het is een filtersysteem waardoor je per categorie kan filter op boeken:

Ook bij dit project heb ik voor Javascript weer het “code ontleden gebruikt”. Ik wist namelijk welke functie ik wilde bereiken, alleen is de code best lastig. Ik heb dit eerst in stappen opgeschreven, als volgt:

- Als ik een button indruk, wordt er een active-state geactiveerd, waardoor je kunt zien dat de button ingedrukt is.
- Je kan de button ook deselecteren, zodat de keuze gereset wordt.
- Als ik een categorie aanklik, worden de sliders met boeken in deze categorie alleen zichtbaar. De boeken die niet aan deze categorie voldoen, worden onzichtbaar gemaakt.

Na dit stappen te hebben gemaakt, kon ik de code stap voor stap formuleren, als volgt:

```js
function clickButton(button) {
 
        if (button == "chill" && button1clicked == false) {
            chillButton.className = "catButton clicked";
            challengingButton.className = "catButton";
 
            romanceSlider.style.display = "block";
            designSlider.style.display = "block";
            horrorSlider.style.display = "none";
 
            button1clicked = true;
            button2clicked = false;
 
        } else if (button == "challenging" && button2clicked == false) {
            chillButton.className = "catButton";
            challengingButton.className = "catButton clicked";
 
            romanceSlider.style.display = "none";
            designSlider.style.display = "none";
            horrorSlider.style.display = "block";
 
            button1clicked = false;
            button2clicked = true;
 
        } else {
            chillButton.className = "catButton";
            challengingButton.className = "catButton";
 
            romanceSlider.style.display = "block";
            designSlider.style.display = "block";
            horrorSlider.style.display = "block";
 
            button1clicked = false;
            button2clicked = false;
        }
 
    }
```

Ook heb ik geleerd hoe ik een javascript library kan gebruiken om een bepaalde animatie te krijgen. Omdat we een boeken website hebben gemaakt, leek het me leuk om door de boekenkast heen te kunnen sliden, net als in het echt. Voor deze interactieve animatie hebben we dus een eenvoudige library gebruikt die ervoor zorgt dat je kunt sliden. Ik heb deze library in de HTML ingeladen, want anders werkt het niet. Hieronder kun je zien hoe ik de sliders werkend heb gemaakt:

```js
var splide = new Splide( '#splideromance', {
        type   : 'loop',
        drag: 'free',
        arrows: false,
        pagination: false,
        gap: 10,
    } );
 
    splide.mount();
 
    var splide = new Splide( '#splidedesign', {
        type   : 'loop',
        drag: 'free',
        arrows: false,
        pagination: false,
        gap: 10,
    } );
 
    splide.mount();
 
    var splide = new Splide( '#splidehorror', {
        type   : 'loop',
        drag: 'free',
        arrows: false,
        pagination: false,
        gap: 10,
    } );
 
    splide.mount();
```

Deze slider werkt alleen als we in de HTML de “boekenkast” hebben geprogrammeerd met een unieke id. In de Javascript konden we de desbetreffende div aanroepen door de juiste id te gebruiken:

```html
<div class="splide" id="splidehorror">
                <div class="splide__track">
                    <ul class="splide__list">
                        <li class="splide__slide"><a href="./book.html" aria-label="Boek Stand"><img src="img/skull.png" alt="Boek Stand"/></a></li>
                        <li class="splide__slide"><a href="./book.html" aria-label="Boek The killer poison"><img src="img/the hiller poison.png" alt="Boek The killer poison"/></a></li>
                        <li class="splide__slide"><a href="./book.html" aria-label="Boek Alone"><img src="img/yellow.png" alt="Boek Alone"/></a></li>
                        <li class="splide__slide"><a href="./book.html" aria-label="Boek Hide and seek"><img src="img/moon.png" alt="Boek Hide and seek"/></a></li>
                    </ul>
                </div>
            </div>
```

Ik heb ook nog een uitklap-container gemaakt die bepaalde tekst weergeeft zodra je er op klikt. De container moet dus geactiveerd worden, anders werkt het niet. Je kan de container ook weer dichtklappen, zodat het weer terug gaat naar de standaardwaarde. Ik ben dus weer bezig geweest met het begrijpen van if-statements: Als dit gebeurt, wordt dit op deze manier zichtbaar, en dat op die manier zichtbaar:

```js
function toggleBlock(block) {
 
        if (block == 1) {
 
            if (opened1 == false) {
                infoBlock1.style.height = textHeight + 40 + "px";
                blockIcon1.className = "blockIconOpen";
                opened1 = true;
 
            } else {
                infoBlock1.style.height = "10px";
                blockIcon1.className = "blockIconClosed";
                opened1 = false;
            }
 
        } else if (block == 2) {
            
            if (opened2 == false) {
                infoBlock2.style.height = textHeight + 40 + "px";
                blockIcon2.className = "blockIconOpen";
                opened2 = true;
 
            } else {
                infoBlock2.style.height = "10px";
                blockIcon2.className = "blockIconClosed";
                opened2 = false;
            }
 
        } else {
 
            if (opened3 == false) {
                infoBlock3.style.height = textHeight + 40 + "px";
                blockIcon3.className = "blockIconOpen";
                opened3 = true;
 
            } else {
                infoBlock3.style.height = "10px";
                blockIcon3.className = "blockIconClosed";
                opened3 = false;
            }
            
        }
    }
```

**Conclusie**

Ik heb aan een ander project gewerkt om nog meer te leren over javascript, in het specifiek de javascript statements. Hierdoor heb ik mijn kennis verbreed met Javascript en heb ik een design vertaald in code. Voor deze website heb ik iets meer gefocust op het visuele gedeelte. Mijn todo list is natuurlijk erg sober, maar voor deze boeken website is rekening gehouden met zowel design als functionaliteit.