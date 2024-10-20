---
layout: home.njk
title: Todo list
date: 2024-10-18
---

**Todo list maken met javascript**

Vanaf het moment dat ik in de hoofdfase zit, heb ik een passie ontwikkeld voor programmeren. Op dit moment is dit nog op front-end niveau, want dit is echt wat ik nu leuk vind en wat een logische stap is om als beginner mee te starten. Mijn kennis van HTML en CSS is erg goed op dit moment, maar Javascript is nog steeds een puntje van aandacht. Ik heb in mijn 3e studiejaar wel al eens projecten gedaan met Javascript, maar snapte er eigenlijk niet veel van. Mijn manier van werken was eigenlijk heel simpel: ChatGPT en copy-paste code. Dit is voor mij en ik denk voor niemand niet een goede manier om programmeertalen te gaan begrijpen. Ik ben daarom deze periode in principe opnieuw begonnen met het onder de knie krijgen van javascript, waardoor ik me heb bezig gehouden met een laagdrempelig project zoals een todo-list maken, maar dan door zelf de code te schrijven.

**Het avontuur**

Ik moet eerlijk zeggen dat ik Javascript nog steeds erg lastig vindt. Hoewel HTML en CSS mij erg makkelijk afgaat, is Javascript toch een stuk moeilijker. Ik vind het wiskundige gedeelte van Javascript nog wel lastig, maar ook wel weer leuk. Ik heb op school het vak Wiskunde altijd leuk gevonden en dit merk ik terug tijdens het gebruiken van Javascript. 

De structuur van Javascript is wel een stuk anders opgebouwd. De welbekende var, const en let is natuurlijk allemaal nieuw en dit heeft best even geduurd voordat ik precies in de gaten kreeg waarom bepaalde code zo in elkaar zat. 

Wat ik zelf erg fijn vond om te doen, om voor het schrijven van code, een soort van stappenplan te schrijven. Dit werkt vooral goed als ik een function wilde gebruiken. 

Toelichting:

De code die ik hier heb geschreven is voor het afvuren van confetti, mits de task afgevinkt is door middel van een checkbox. Toen ik deze regels met code voor het eerst zag, zag het er echt uit als wartaal.

```js
function toggleTodo(index) {
            todos[index].completed = !todos[index].completed;
            saveTodos();
            displayTodos();
            if (todos[index].completed) {
                triggerConfetti();
            }
        }
```

Voordat ik dus een functie wilde aanroepen heb ik in stappen opgeschreven wat ik met deze functie wilde bereiken. Dit ging als volgt:

- Ik wil dat de checkbox aangeklikt kan worden om een taak te “completen” of door een taak juist weer te “unchecken”.
- Als de checkbox aangeklikt wordt, wil ik een animatie om visueel weer te geven dat er een goede prestatie is geleverd. Dit mag alleen gebeuren bij het afvinken en niet andersom bij het ongedaan maken van het afvinken.
- Ik wil dat de status opgeslagen wordt in localstorage zodat de data bewaard blijft als ik de website ga refreshen.

Na dit stappenplan, kan je de code per stap gaan opschrijven.

- Ik wil dat de checkbox aangeklikt kan worden om een taak te “completen” of door een taak juist weer te “unchecken”.

```js
function toggleTodo(index) {
            todos[index].completed = !todos[index].completed;
            saveTodos();
            displayTodos();
            if (todos[index].completed) {
                triggerConfetti();
            }
        }
```

```js
function toggleTodo(index) {
            todos[index].completed = !todos[index].completed;}
```

- Als de checkbox aangeklikt wordt, wil ik een animatie om visueel weer te geven dat er een goede prestatie is geleverd. Dit mag alleen gebeuren bij het afvinken en niet andersom bij het ongedaan maken van het afvinken.

```js
if (todos[index].completed) {
                triggerConfetti();
            }
```

- Ik wil dat de status opgeslagen wordt in localstorage zodat de data bewaard blijft als ik de website ga refreshen.

```js
saveTodos();
displayTodos();
```

Dit heeft mij echt geholpen om de code te gaan begrijpen. Ik noem deze methode “Het ontleden van code”.

**De code**

Tijdens het todo project heb ik actief om feedback gevraagd aan Tjerk en klasgenoten die al meer kennis hebben van Javascript. Ik merk aan mezelf dat ik de feedback beter in mezelf opneem als ik persoonlijk en fysiek met iemand ga zitten. Tutorials op youtube lijken toegankelijk, maar sluiten niet aan op mijn persoonlijke snelheid en kennis van Javascript. Ik heb YouTube enkel gebruikt om inspiratie of uitleg te krijgen.

Voordat ik ben begonnen met de todolist, heb ik van Tjerk een aantal handelingen gekregen die op de todo-list gedaan konden worden. Dit is voor mij echt een richtlijn geweest wat wel en niet moest gaan gebeuren. De focus lag dit keer niet op de styling (css) van de website, maar puur de functionaliteit en het onder de knie krijgen van Javascript.

Tjerk heeft mijn code beoordeeld en comments geplaats waar nodig. Hieronder de raw comments inclusief typfouten ;-)

```js
// query selector all inputs
// foreach loopen
// aan al die checkboxes een eventlisten hangen en dan je checken of die checked.
// dan kan je confetti afvuren 


// de JSON laden en alle todo's renderen
// laten zien in de html

// hou je de todos bij in de HTML of hou je het bij in een array met todo.
// remove from html
// array remove of array push

// zet in een array en render de array met todos
// functie nodig die heet render die krijgt een array met todo's en die poept ze uit in de html

// add, remove functie aanroept
// opnieuw render

// let todos = ["asdasdasd", "asdasdsa", "asdasd"];
```

Handig om te benoemen is dat ik eerst de todo’s in een unordered list in de HTML bijhield. Doordat ik localstorage wilde toevoegen, heb ik het bijhouden van de todo’s veranderd van de HTML naar een array die geëxporteerd kan worden als JSON.

Code ging van:

```js
function saveData(){
    localStorage.setItem("data", list.innerHTML);
}
function showTask(){
    const savedData = localStorage.getItem("data");
    if(savedData){
        list.innerHTML = savedData;
    }
}
```

Naar:

```js
let todos = [];
function saveTodos() {
    localStorage.setItem('todos', JSON.stringify(todos));
}
window.onload = function() {
    const storedTodos = localStorage.getItem('todos');
    if (storedTodos) {
        todos = JSON.parse(storedTodos);
        displayTodos();
    }
}
function displayTodos() {
    const todoList = document.getElementById('itemList');
    todoList.innerHTML = '';

    for (let i = 0; i < todos.length; i++) {
        const li = document.createElement('li');
        li.innerHTML = `
            <input type="checkbox" onchange="toggleTodo(${i})" ${todos[i].completed ? 'checked' : ''}>
            <span class="${todos[i].completed ? 'completed' : ''}">${todos[i].text}</span>
            <span class="delete-btn" onclick="deleteTodo(${i})">❌</span>
        `;
        todoList.appendChild(li);
    }
}
```

Door de code te veranderen heb ik nu een button toegevoegd die de JSON kan exporteren, waardoor je een JSON file kan exporteren met daarin de todo’s weergegeven in een array.

**Conclusie**

Ik heb veel geleerd van de projecten die ik heb gedaan met Javascript. Vooral ook omdat ik voordat ik begon erg weinig kennis had van javascript. Het is dus in principe allemaal nieuw voor mij geweest deze periode. Hoewel ik nu de structuur van javascript begrijp, vind ik het nog steeds lastig om de code wel helemaal zelf te schrijven. Ik ben natuurlijk actief geweest op MDN docs en stackoverflow, maar vaak is de uitleg erg algemeen en moet je code zo vormen dat het passend is voor je project. Ik heb dus best wat moeite gehad om de code echt werkend te krijgen en hier heeft ook best wat tijd ingezeten. Soms kon ik minuten lang staren naar 1 regel met code om te achterhalen waarom er een error werd weergegeven. Ik weet dus 100% zeker dat ik de volgende periode weer met Javascript bezig ga. Ik vind het desondanks erg leuk en houd ervan om opnieuw uitgedaagd te worden met nieuw coding-languages. Ik laat eerst nog even de frameworks zoals NEXT.js en React achterwegen, want dit kan ik beter oppakken als ik nog meer geoefend heb met javascript. Ik heb zelf een schema waarbij meerdere projecten m.b.v. javascript staan opgedeeld per niveau.



