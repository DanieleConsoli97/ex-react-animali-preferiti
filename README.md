# 🐾 Trasformare una Pagina HTML Statica in un'App React Interattiva

## Introduzione

Un collega, distratto da un animale domestico, ha pubblicato una pagina HTML statica invece di usare React. Ora tocca a te convertire quella pagina in un'app interattiva **senza riscrivere da zero**, montando React direttamente all'interno del documento HTML, come mostrato in questo esempio:

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I miei animali Preferiti</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
      <h1>I miei animali Preferiti</h1>
    </header>
    <main>
        <figure>
            <img src="https://picsum.photos/400/300" alt="Immagine Casuale">
        </figure>
        <div class="lista-animali"></div>
    </main>
    <footer>
      <p>Creato con amore da... un collega sbadato! 🐾</p>
    </footer>
</body>
</html>
```

E questo è il relativo CSS:

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
header {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 1rem;
}
main {
    padding: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
}
footer {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 1rem;
}
form{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
}
img{
    max-width: 100%;
}
.lista-animali{
    width: 100%;
}
```

---

## ✅ Obiettivi e Milestone

### 📌 Milestone 1: Inserire un Componente React

**Obiettivo:** Mostrare una lista statica di animali all'interno di un `<details>`.

**Requisiti:**

* Monta un componente React nell'elemento con classe `.lista-animali`.
* Il componente include:

  * `<details>` con titolo "Animali".
  * Una `<ul>` generata da un array statico `const animals = ["Cane", "Gatto", "Pappagallo"]`.

### 📌 Milestone 2: Aggiungere Animali Casuali

**Obiettivo:** Permettere l'aggiunta dinamica di animali alla lista.

**Requisiti:**

* Inizializza lo stato `animals` con `useState([])`.
* Crea un bottone "Aggiungi Animale".
* Alla pressione del bottone, scegli casualmente da:

```js
const animalsChoices = ["Cane", "Gatto", "Pappagallo", "Cavallo", "Panda"];
```

* Aggiungi l'animale selezionato alla lista `<ul>`.

### 📌 Milestone 3: Usare una Modale per Aggiungere Animali

**Obiettivo:** Consentire l'inserimento manuale di un nome animale tramite modale.

**Requisiti:**

* Espandi il componente `Modal`:

  * La prop `content` accetta anche componenti React.
  * Aggiungi i bottoni "Annulla" e "Conferma".
  * Una prop `onConfirm` gestisce la conferma.
* Al click su "Aggiungi Animale":

  * Mostra la modale con input di testo.
  * Conferma aggiunge l'animale alla lista.

```js
function Modal({ title, content, show = false, onClose = () => {}, onConfirm = () => {} }) {
  return show && ReactDOM.createPortal(
    <div className="modal-container">
      <div className="modal">
        <h2>{title}</h2>
        {content}
        <div>
          <button onClick={onClose}>Annulla</button>
          <button onClick={onConfirm}>Conferma</button>
        </div>
      </div>
    </div>,
    document.body
  );
}
```

### 🎯 Bonus: Utilizzare l'API per Creare Card

**Obiettivo:** Migliorare l'inserimento usando una API per ottenere info sugli animali.

**Requisiti:**

* Endpoint API:

```
https://boolean-spec-frontend.vercel.app/freetestapi/animals?search=[animalName]
```

* Durante la ricerca:

  * Mostra "Caricamento..." mentre si attende la risposta.
  * Gestisci errori (nessun risultato, rete assente).

**Dati richiesti dal primo risultato disponibile:**

* `name`
* `description` ("Descrizione non disponibile" se mancante)
* `image` (default se mancante)

**Visualizzazione in una card:**

* Titolo con nome dell'animale.
* Immagine.
* Descrizione.

---

## 🧠 Suggerimenti Tecnici

* Usa `ReactDOM.createRoot(document.querySelector(".lista-animali"))` per montare l'app.
* Ogni animale può essere visualizzato come:

```jsx
<div className="animal-card">
  <h3>{animal.name}</h3>
  <img src={animal.image} alt={animal.name} />
  <p>{animal.description}</p>
</div>
```

* Gestisci key univoche per ogni animale (`index` o `uuid`).

---

## 🎉 Conclusione

Un errore iniziale è diventato un'opportunità per creare una splendida app interattiva con React, direttamente in una pagina HTML esistente. Hai dimostrato creatività, adattabilità e padronanza di React!

Buon lavoro e... 🐶🐱🐦 React con amore!
