---
layout: base
title: Striver Hobbies
search_exclude: true
permalink: /Striver/striver-hobbies
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
</div>

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
</div>

<h1 style="color:cyan;">Hobbies</h1>
Explore and manage your hobbies!

<div class="container">
    <div class="form-container">
        <h2>Select Category</h2>
        <div>
            <label for="category">Category:</label>
            <select id="category">
                <option value="general">General</option>
                <option value="sports">Sports</option>
                <option value="arts">Arts</option>
            </select>
            <button onclick="fetchHobbies()">Get Hobbies</button>
        </div>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Hobbies List</h2>
        <ul id="hobbies-list"></ul>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Add Hobby</h2>
        <input type="text" id="new-hobby-name" placeholder="Enter hobby name" />
        <button onclick="addHobby()">Add Hobby</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Update Hobby</h2>
        <input type="text" id="old-hobby-name" placeholder="Old hobby name" />
        <input type="text" id="updated-hobby-name" placeholder="New hobby name" />
        <button onclick="updateHobby()">Update Hobby</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Delete Hobby</h2>
        <input type="text" id="delete-hobby-name" placeholder="Hobby name to delete" />
        <button onclick="deleteHobby()">Delete Hobby</button>
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
    const apiUrl = 'http://127.0.0.1:8887/api/hobby';
function fetchHobbies() {
    // Fetch hobbies based on the selected category
    const category = document.getElementById('category').value;
    // Example: Fetch hobbies from a server or local storage
    console.log(`Fetching hobbies for category: ${category}`);
}

function addHobby() {
    const hobbyName = document.getElementById('new-hobby-name').value;
    if (hobbyName) {
        const hobbiesList = document.getElementById('hobbies-list');
        const listItem = document.createElement('li');
        listItem.textContent = hobbyName;
        hobbiesList.appendChild(listItem);
        console.log(`Added hobby: ${hobbyName}`);
    }
}

function updateHobby() {
    const oldHobbyName = document.getElementById('old-hobby-name').value;
    const updatedHobbyName = document.getElementById('updated-hobby-name').value;
    const hobbiesList = document.getElementById('hobbies-list').children;
    for (let i = 0; i < hobbiesList.length; i++) {
        if (hobbiesList[i].textContent === oldHobbyName) {
            hobbiesList[i].textContent = updatedHobbyName;
            console.log(`Updated hobby: ${oldHobbyName} to ${updatedHobbyName}`);
            break;
        }
    }
}

function deleteHobby() {
    const hobbyName = document.getElementById('delete-hobby-name').value;
    const hobbiesList = document.getElementById('hobbies-list').children;
    for (let i = 0; i < hobbiesList.length; i++) {
        if (hobbiesList[i].textContent === hobbyName) {
            hobbiesList[i].remove();
            console.log(`Deleted hobby: ${hobbyName}`);
            break;
        }
    }
}
</script>

<style>
/* General Styles */
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

.sidebar-btn:hover {
  background-color: #1e1e1e;
  transform: scale(1.05);
}

.sidebar-btn.active {
  background-color: #333;
  font-weight: bold;
}
</style>