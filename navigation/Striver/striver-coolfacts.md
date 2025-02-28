--- 
layout: base
title: Striver About
search_exclude: true
permalink: /Striver/striver-coolfacts
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
<h1 style="color:cyan;">Cool Facts</h1>
<h2 id="changing-text" style="color:#28cee8">This page is dedicated to you posting the factual events or things of those you look up too</h2>
<h3 style="color:#28cee8">The way this works is that you input a fact about someone you look up to, and then add after how long that fact will relate to you as well</h3>
<br>
<h3 style="color:#28cee8">For example ...</h3>
<div class="container">
    <div class="form-container">
        <h2>Cool Facts List</h2>
        <ul id="coolfacts-list"></ul>
    </div>
</div>
<div class="container">
    <div class="form-container">
        <h2>Add Cool Fact</h2>
        <label for="new-fact-age">Age:</label>
        <input type="text" id="new-fact-age" placeholder="Enter age" />
        <label for="new-fact-text">Cool Fact:</label>
        <input type="text" id="new-fact-text" placeholder="Enter cool fact" />
        <button id="add-fact-btn">Add Cool Fact</button>
    </div>
</div>
<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';
async function fetchCoolFacts() {
    try {
        const response = await fetch(`${pythonURI}/api/coolfacts`, {
            ...fetchOptions,
            method: 'GET'
        });
        if (!response.ok) {
            throw new Error('Failed to fetch cool facts: ' + response.statusText);
        }
        const data = await response.json();
        const coolFactsList = document.getElementById('coolfacts-list');
        coolFactsList.innerHTML = "";
        data.forEach(fact => {
            const listItem = document.createElement('li');
            listItem.style.display = 'flex';
            listItem.style.alignItems = 'center';
            listItem.style.justifyContent = 'space-between';
            const factText = document.createElement('span');
            factText.textContent = `${fact.age}: ${fact.coolfacts}`;
            const updateButton = document.createElement('button');
            updateButton.textContent = 'Update';
            updateButton.style.marginLeft = '10px';
            updateButton.style.padding = '2px 5px';
            updateButton.onclick = () => promptUpdateCoolFact(fact.id, fact.age, fact.coolfacts);
            const deleteButton = document.createElement('button');
            deleteButton.textContent = 'Delete';
            deleteButton.style.marginLeft = '10px';
            deleteButton.style.padding = '2px 5px';
            deleteButton.onclick = () => deleteCoolFact(fact.id);
            listItem.appendChild(factText);
            listItem.appendChild(updateButton);
            listItem.appendChild(deleteButton);
            coolFactsList.appendChild(listItem);
        });
    } catch (error) {
        console.error('Error fetching cool facts:', error);
    }
}
async function addCoolFact() {
    const age = document.getElementById('new-fact-age').value;
    const coolfacts = document.getElementById('new-fact-text').value;
    try {
        const response = await fetch(`${pythonURI}/api/coolfacts`, {
            ...fetchOptions,
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ age, coolfacts })
        });
        if (!response.ok) {
            throw new Error('Failed to add cool fact: ' + response.statusText);
        }
        alert('Cool fact added successfully!');
        document.getElementById('new-fact-age').value = ''; // Clear input
        document.getElementById('new-fact-text').value = ''; // Clear input
        fetchCoolFacts(); // Refresh cool facts list
    } catch (error) {
        console.error('Error adding cool fact:', error);
        alert('Error adding cool fact: ' + error.message);
    }
}
async function promptUpdateCoolFact(id, age, coolfacts) {
    const updatedAge = prompt('Enter new age:', age);
    const updatedCoolFact = prompt('Enter new cool fact:', coolfacts);
    if (updatedAge && updatedCoolFact) {
        try {
            const response = await fetch(`${pythonURI}/api/coolfacts`, {
                ...fetchOptions,
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ 
                    coolfacts, 
                    age, 
                    new_coolfacts: updatedCoolFact, 
                    new_age: updatedAge 
                })
            });
            if (!response.ok) {
                throw new Error('Failed to update cool fact: ' + response.statusText);
            }
            alert('Cool fact updated successfully!');
            fetchCoolFacts(); // Refresh cool facts list
        } catch (error) {
            console.error('Error updating cool fact:', error);
            alert('Error updating cool fact: ' + error.message);
        }
    }
}
async function deleteCoolFact(id) {
    try {
        const response = await fetch(`${pythonURI}/api/coolfacts`, {
            ...fetchOptions,
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ id })
        });
        if (!response.ok) {
            throw new Error('Failed to delete cool fact: ' + response.statusText);
        }
        alert('Cool fact deleted successfully!');
        fetchCoolFacts(); // Refresh cool facts list
    } catch (error) {
        console.error('Error deleting cool fact:', error);
        alert('Error deleting cool fact: ' + error.message);
    }
}
document.getElementById('add-fact-btn').addEventListener('click', addCoolFact);
fetchCoolFacts();
function changeTextColor() {
    const getRandomHexColor = () => {
    return `#${Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0')}`;
    };
    const element = document.getElementById('changing-text');
    if (element) {
        element.style.color = getRandomHexColor();
    }
}
setInterval(changeTextColor, 500);
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
#coolfacts-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #1A252F;
  padding: 10px;
  margin-bottom: 5px;
  border-radius: 5px;
  border: 1px solid #28cee8;
}
#coolfacts-list button {
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
#coolfacts-list button.update-btn {
  background-color: #1A252F;
  margin-left: 10px; /* Add some space between buttons */
  border: 1px solid #28cee8;
}
#coolfacts-list button.update-btn:hover {
  background-color: #2980B9;
}
#coolfacts-list span {
  flex-grow: 1; /* Ensure the text takes up available space */
}
#coolfacts-list button:hover {
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