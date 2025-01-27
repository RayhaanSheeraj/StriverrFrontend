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
    <a href="/StriverrFrontend/Striver/striver-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
    <a href="/StriverrFrontend/Striver/striver-steps" class="sidebar-btn bottom-btn">Step tracker</a>
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-hobbies" class="sidebar-btn bottom-btn">Hobbies</a>
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
</div>

<h1 style="color:cyan;">Quotes</h1>
Explore quotes!

<div class="container">
    <div class="form-container">
        <h2>Select Category</h2>
        <div>
            <label for="category">Category:</label>
            <select id="category">
                <option value="">All</option>
                <option value="common">Common</option>
                <option value="sports">Sports</option>
                <option value="motivational">Motivation</option>
            </select>
            <button onclick="fetchQuotes()">Find Quotes</button>
        </div>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Quotes List</h2>
        <ul id="quotes-list"></ul>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Add Quote</h2>
        <input type="text" id="new-quote" placeholder="Enter Quote" />
        <button onclick="addQuote()">Add Quote</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Update Quote</h2>
        <input type="text" id="old-quote" placeholder="Old Quote" />
        <input type="text" id="updated-quote" placeholder="New Quote" />
        <button onclick="updateQuote()">Update Quote</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Delete Quote</h2>
        <input type="text" id="delete-quote" placeholder="Desired quote to delete" />
        <button onclick="deleteQuote()">Delete Quote</button>
    </div>
</div>

<div class="members-section">
    <h3 style="color:cyan;">Members</h3>
    <ul>
        <li>⚪ John</li>
        <li>⚪ Mary</li>
        <li>⚪ Jack</li>
        <li>⚪ Bob</li>
        <li>⚪ Matt</li>
        <li>⚪ Mark</li>
        <li>⚪ Juan</li>
        <li>⚪ Travis</li>
    </ul>
</div>

<script>
    const apiUrl = 'http://127.0.0.1:8887/api/quotes';

    // Static quotes dataset (fallback if API is unavailable)
    const quotesDataset = [
        { text: "The only way to do great work is to love what you do.", category: "motivational" },
        { text: "Don't watch the clock; do what it does. Keep going.", category: "motivational" },
        { text: "Winning isn’t everything, but wanting to win is.", category: "sports" },
        { text: "Champions keep playing until they get it right.", category: "sports" },
        { text: "Hard work beats talent when talent doesn’t work hard.", category: "sports" },
        { text: "Success is not the key to happiness. Happiness is the key to success.", category: "common" },
        { text: "Happiness is not by chance, but by choice.", category: "common" },
        { text: "Success is not final, failure is not fatal: It is the courage to continue that counts.", category: "common" },
        { text: "Believe you can, and you're halfway there.", category: "common" },
        { text: "In the middle of every difficulty lies opportunity.", category: "common" },
        { text: "Never give up on something you can’t go a day without thinking about.", category: "motivational" },
        { text: "It’s not the will to win that matters—everyone has that. It’s the will to prepare to win that matters.", category: "sports" }
    ];

    async function fetchQuotes() {
        const category = document.getElementById('category').value;
        const quotesList = document.getElementById('quotes-list');
        quotesList.innerHTML = '';

        try {
            const response = await fetch(apiUrl + '/quote');
            if (response.ok) {
                const quotes = await response.json();
                let filteredQuotes = quotes;

                if (category) {
                    filteredQuotes = quotes.filter(q => q.category === category);
                }

                filteredQuotes.forEach((quote) => {
                    const listItem = document.createElement('li');
                    listItem.textContent = quote.text;
                    quotesList.appendChild(listItem);
                });
            } else {
                throw new Error('API unavailable, falling back to local dataset');
            }
        } catch {
            let filteredQuotes = quotesDataset;
            if (category) {
                filteredQuotes = quotesDataset.filter(q => q.category === category);
            }

            filteredQuotes.forEach((quote) => {
                const listItem = document.createElement('li');
                listItem.textContent = quote.text;
                quotesList.appendChild(listItem);
            });
        }
    }

    async function addQuote() {
        const newQuote = document.getElementById('new-quote').value;
        if (!newQuote) return alert('Please enter a quote to add.');

        try {
            const response = await fetch(`${apiUrl}/quotes`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ text: newQuote, category: "general" })
            });

            if (response.ok) {
                alert('Quote added successfully!');
            } else {
                throw new Error('API request failed');
            }
        } catch {
            quotesDataset.push({ text: newQuote, category: "general" });
            alert('Quote added!');
        }
        fetchQuotes();
    }

    async function updateQuote() {
        const oldQuote = document.getElementById('old-quote').value;
        const updatedQuote = document.getElementById('updated-quote').value;

        if (!oldQuote || !updatedQuote) return alert('Please enter both the old and new quotes.');

        try {
            const response = await fetch(`${apiUrl}/quotes`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ oldQuote, updatedQuote })
            });

            if (response.ok) {
                alert('Quote updated successfully!');
            } else {
                throw new Error('API request failed');
            }
        } catch {
            const quoteIndex = quotesDataset.findIndex(q => q.text === oldQuote);
            if (quoteIndex !== -1) {
                quotesDataset[quoteIndex].text = updatedQuote;
                alert('Quote updated!');
            } else {
                alert('Quote not found in local dataset!');
            }
        }
        fetchQuotes();
    }

    async function deleteQuote() {
        const deleteQuote = document.getElementById('delete-quote').value;
        if (!deleteQuote) return alert('Please enter a quote to delete.');

        try {
            const response = await fetch(`${apiUrl}/quotes`, {
                method: 'DELETE',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ text: deleteQuote })
            });

            if (response.ok) {
                alert('Quote deleted successfully!');
            } else {
                throw new Error('API request failed');
            }
        } catch {
            const quoteIndex = quotesDataset.findIndex(q => q.text === deleteQuote);
            if (quoteIndex !== -1) {
                quotesDataset.splice(quoteIndex, 1);
                alert('Quote deleted!');
            } else {
                alert('Quote not found in local dataset!');
            }
        }
        fetchQuotes();
    }
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #121212;
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
  background-color: #2C3E50;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  color: #ECF0F1;
}

.form-container label, .form-container input, .form-container textarea, .form-container select, .form-container button {
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  border: none;
  width: 100%;
}

.form-container button {
  background-color: #34495E;
  color: #ECF0F1;
  cursor: pointer;
}

.form-container button:hover {
  background-color: #1A252F;
}

/* Members Section */
.members-section {
  background-color: #111;
  color: white;
  width: 200px; /* Set width for the sidebar */
  position: fixed; /* Fix it to the side */
  right: 0;
  top: 0;
  bottom: 0; /* Stretch it vertically */
  padding-top: 20px; /* Add padding from top */
  text-align: left; /* Align text to the left */
  z-index: 10; /* Ensure it stays above other elements */
}

.members-section h3 {
  text-align: center;
  margin-bottom: 20px;
}

.members-section ul {
  list-style-type: none;
  padding: 0;
}

.members-section li {
  margin: 10px 0;
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
</style>
