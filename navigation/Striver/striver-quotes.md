---
layout: base
title: Striver Quotes
search_exclude: true
permalink: /Striver/striver-quotes
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<div class="sidebar">
    <a href="/StriverrFrontend/Striver/striver-achievements" class="sidebar-btn">⭐️ Achievements</a>
    <a href="/StriverrFrontend/Striver/striver-challenges" class="sidebar-btn">📉 Challenges</a>
    <a href="/StriverrFrontend/Striver/striver-ai" class="sidebar-btn">🤖 AI</a>
    <a href="/StriverrFrontend/Striver/striver-about" class="sidebar-btn">❓ About</a>
    <a href="/StriverrFrontend/Striver/striverr-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
    <a href="/StriverrFrontend/Striver/striver-steps" class="sidebar-btn bottom-btn">Step Tracker</a>
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
    <a href="/StriverrFrontend/Striver/striver-hobbies" class="sidebar-btn bottom-btn">Hobbies</a>
    <a href="/StriverrFrontend/Striver/striver-coolfacts" class="sidebar-btn bottom-btn">Cool Facts</a>
    <a href="/StriverrFrontend/Striver/striver-goals" class="sidebar-btn bottom-btn">🥅 Goals</a>
</div>

<h1 style="color:cyan;">Quotes</h1>
<p style="color:#28cee8">This page is dedicated to you posting your favorite quotes.</p>

<div class="container">
    <div class="form-container">
        <h2>Quotes List</h2>
        <ul id="quotes-list"></ul>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Add Quote</h2>
        <label for="new-quote-name">Quote:</label>
        <input type="text" id="new-quote-name" placeholder="Enter quote" />
        <label for="new-quote-category">Category:</label>
        <input type="text" id="new-quote-category" placeholder="Enter category" />
        <button id="add-quote-btn">Add Quote</button>
    </div>
</div>

<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

async function fetchQuotes() {
    try {
        const response = await fetch(`${pythonURI}/api/quotes`, {
            ...fetchOptions,
            method: 'GET'
        });
        if (!response.ok) {
            throw new Error('Failed to fetch quotes: ' + response.statusText);
        }
        const data = await response.json();
        const quotesList = document.getElementById('quotes-list');
        quotesList.innerHTML = "";

        data.forEach(quote => {
            const listItem = document.createElement('li');
            listItem.style.display = 'flex';
            listItem.style.alignItems = 'center';
            listItem.style.justifyContent = 'space-between';

            const quoteText = document.createElement('span');
            quoteText.textContent = `${quote.category}: ${quote.name}`;

            const updateButton = document.createElement('button');
            updateButton.textContent = 'Update';
            updateButton.style.marginLeft = '10px';
            updateButton.style.padding = '2px 5px';
            updateButton.onclick = () => promptUpdateQuote(quote.name, quote.category);

            const deleteButton = document.createElement('button');
            deleteButton.textContent = 'Delete';
            deleteButton.style.marginLeft = '10px';
            deleteButton.style.padding = '2px 5px';
            deleteButton.onclick = () => deleteQuote(quote.name, quote.category);

            listItem.appendChild(quoteText);
            listItem.appendChild(updateButton);
            listItem.appendChild(deleteButton);
            quotesList.appendChild(listItem);
        });
    } catch (error) {
        console.error('Error fetching quotes:', error);
    }
}

async function addQuote() {
    const name = document.getElementById('new-quote-name').value;
    const category = document.getElementById('new-quote-category').value;
    try {
        const response = await fetch(`${pythonURI}/api/quotes`, {
            ...fetchOptions,
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ name, category })
        });
        if (!response.ok) {
            throw new Error('Failed to add quote: ' + response.statusText);
        }
        alert('Quote added successfully!');
        document.getElementById('new-quote-name').value = ''; // Clear input
        document.getElementById('new-quote-category').value = ''; // Clear input
        fetchQuotes(); // Refresh quotes list
    } catch (error) {
        console.error('Error adding quote:', error);
        alert('Error adding quote: ' + error.message);
    }
}

async function promptUpdateQuote(name, category) {
    const updatedName = prompt('Enter new quote:', name);
    const updatedCategory = prompt('Enter new category:', category);
    if (updatedName && updatedCategory) {
        try {
            const response = await fetch(`${pythonURI}/api/quotes`, {
                ...fetchOptions,
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ old_name: name, name: updatedName, category: updatedCategory })
            });
            if (!response.ok) {
                throw new Error('Failed to update quote: ' + response.statusText);
            }
            alert('Quote updated successfully!');
            fetchQuotes(); // Refresh quotes list
        } catch (error) {
            console.error('Error updating quote:', error);
            alert('Error updating quote: ' + error.message);
        }
    }
}

async function deleteQuote(name, category) {
    try {
        const response = await fetch(`${pythonURI}/api/quotes`, {
            ...fetchOptions,
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ name, category })
        });
        if (!response.ok) {
            throw new Error('Failed to delete quote: ' + response.statusText);
        }
        alert('Quote deleted successfully!');
        fetchQuotes(); // Refresh quotes list
    } catch (error) {
        console.error('Error deleting quote:', error);
        alert('Error deleting quote: ' + error.message);
    }
}

document.getElementById('add-quote-btn').addEventListener('click', addQuote);
fetchQuotes();
</script>

<style>
/* General Styles */
body {
  font-family: Arial, sans-serif;
  background-color: #1A252F;
  color: #fff;
  margin: 0;
  padding: 0;
}

h1, h2 {
  text-align: center;
}

.container {
  display: flex;
  justify-content: center;
  width: 100%;
  max-width: 1200px;
  padding: 20px;
  box-sizing: border-box;
}

.form-container {
  display: flex;
  flex-direction: column;
  max-width: 800px;
  width: 100%;
  background-color: #1A252F;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  color: #ECF0F1;
  border: 1px solid #28cee8;
}

.form-container label, .form-container input, .form-container textarea, .form-container select, .form-container button {
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  border: none;
  width: 100%;
}

.form-container button {
  background-color: #1A252F;
  color: #ECF0F1;
  cursor: pointer;
  border: 1px solid #28cee8;
}

.form-container button:hover {
  background-color: #1A252F;
}

#quotes-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #1A252F;
  padding: 10px;
  margin-bottom: 5px;
  border-radius: 5px;
  border: 1px solid #28cee8;
}

#quotes-list button {
  background-color: #E74C3C;
  color: #ECF0F1;
  border: none;
  padding: 2px 5px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px; /* Make the button smaller */
  width: 60px; /* Make the button smaller horizontally */
  margin-left: 0; /* Move the button closer */
  border: 1px solid #28cee8;
}

#quotes-list button.update-btn {
  background-color: #1A252F;
  margin-left: 10px; /* Add some space between buttons */
  border: 1px solid #28cee8;
}

#quotes-list button.update-btn:hover {
  background-color: #2980B9;
}

#quotes-list span {
  flex-grow: 1; /* Ensure the text takes up available space */
}

#quotes-list button:hover {
  background-color: #C0392B;
}

/* Sidebar */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 180px;
  height: 100%;
  background-color: #121212 !important;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
  color: white;
  border-right: 1px solid gray;
}

.sidebar-btn {
  background-color: #121212;
  color: white !important;
  border: 2px solid cyan;
  margin: 10px 0;
  padding: 10px;
  border-radius: 8px;
  font-size: 16px;
  width: 160px;
  text-align: center;
  cursor: pointer;
  text-decoration: none;
}

.bottom-btn {
  margin-top: auto; /* Pushes the Terms button to the bottom */
}

.sidebar-btn:hover {
  background-color: #1E1E1E;
  transform: scale(1.05);
}

.sidebar-btn.active {
  background-color: #333;
  font-weight: bold;
}
</style>