---
layout: base
title: Striver Hobbies
search_exclude: true
permalink: /Striver/striver-hobbies
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaiddf
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
        <label for="new-hobby-name">Hobby Name:</label>
        <input type="text" id="new-hobby-name" placeholder="Enter hobby name" />
        <label for="new-hobby-category">Category:</label>
        <select id="new-hobby-category">
            <option value="general">General</option>
            <option value="sports">Sports</option>
            <option value="arts">Arts</option>
        </select>
        <button id="add-hobby-btn">Add Hobby</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Update Hobby</h2>
        <label for="old-hobby-name">Old Hobby Name:</label>
        <input type="text" id="old-hobby-name" placeholder="Old hobby name" />
        <label for="updated-hobby-name">New Hobby Name:</label>
        <input type="text" id="updated-hobby-name" placeholder="New hobby name" />
        <label for="update-hobby-category">Category:</label>
        <select id="update-hobby-category">
            <option value="general">General</option>
            <option value="sports">Sports</option>
            <option value="arts">Arts</option>
        </select>
        <button id="update-hobby-btn">Update Hobby</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Delete Hobby</h2>
        <label for="delete-hobby-name">Hobby Name:</label>
        <input type="text" id="delete-hobby-name" placeholder="Hobby name to delete" />
        <label for="delete-hobby-category">Category:</label>
        <select id="delete-hobby-category">
            <option value="general">General</option>
            <option value="sports">Sports</option>
            <option value="arts">Arts</option>
        </select>
        <button id="delete-hobby-btn">Delete Hobby</button>
    </div>
</div>

<script type="module">
    const pythonURI = 'http://127.0.0.1:8887';
    const fetchOptions = {
        headers: {
            'Content-Type': 'application/json'
        }
    };

    async function fetchHobbies() {
        try {
            const category = document.getElementById('category').value;
            const response = await fetch(`${pythonURI}/api/hobby?category=${category}`, {
                ...fetchOptions,
                method: 'GET'
            });

            if (!response.ok) {
                throw new Error('Failed to fetch hobbies: ' + response.statusText);
            }
            const data = await response.json();
            const hobbiesList = document.getElementById('hobbies-list');
            hobbiesList.innerHTML = "";

            data.hobbies.forEach(hobby => {
                const listItem = document.createElement('li');
                listItem.textContent = hobby;
                hobbiesList.appendChild(listItem);
            });
        } catch (error) {
            console.error('Error fetching hobbies:', error);
        }
    }

    async function addHobby() {
        const hobbyName = document.getElementById('new-hobby-name').value;
        const category = document.getElementById('new-hobby-category').value;
        try {
            const response = await fetch(`${pythonURI}/api/hobby`, {
                ...fetchOptions,
                method: 'POST',
                body: JSON.stringify({ name: hobbyName, category: category })
            });

            if (!response.ok) {
                throw new Error('Failed to add hobby: ' + response.statusText);
            }

            alert('Hobby added successfully!');
            document.getElementById('new-hobby-name').value = ''; // Clear input
            fetchHobbies(); // Refresh hobbies list
        } catch (error) {
            console.error('Error adding hobby:', error);
            alert('Error adding hobby: ' + error.message);
        }
    }

    async function updateHobby() {
        const oldHobbyName = document.getElementById('old-hobby-name').value;
        const updatedHobbyName = document.getElementById('updated-hobby-name').value;
        const category = document.getElementById('update-hobby-category').value;
        try {
            const response = await fetch(`${pythonURI}/api/hobby`, {
                ...fetchOptions,
                method: 'PUT',
                body: JSON.stringify({ old_name: oldHobbyName, name: updatedHobbyName, category: category })
            });

            if (!response.ok) {
                throw new Error('Failed to update hobby: ' + response.statusText);
            }

            alert('Hobby updated successfully!');
            document.getElementById('old-hobby-name').value = ''; // Clear input
            document.getElementById('updated-hobby-name').value = ''; // Clear input
            fetchHobbies(); // Refresh hobbies list
        } catch (error) {
            console.error('Error updating hobby:', error);
            alert('Error updating hobby: ' + error.message);
        }
    }

    async function deleteHobby() {
        const hobbyName = document.getElementById('delete-hobby-name').value;
        const category = document.getElementById('delete-hobby-category').value;
        try {
            const response = await fetch(`${pythonURI}/api/hobby`, {
                ...fetchOptions,
                method: 'DELETE',
                body: JSON.stringify({ name: hobbyName, category: category })
            });

            if (!response.ok) {
                throw new Error('Failed to delete hobby: ' + response.statusText);
            }

            alert('Hobby deleted successfully!');
            document.getElementById('delete-hobby-name').value = ''; // Clear input
            fetchHobbies(); // Refresh hobbies list
        } catch (error) {
            console.error('Error deleting hobby:', error);
            alert('Error deleting hobby: ' + error.message);
        }
    }

    document.getElementById('category').addEventListener('change', fetchHobbies);
    document.getElementById('add-hobby-btn').addEventListener('click', addHobby);
    document.getElementById('update-hobby-btn').addEventListener('click', updateHobby);
    document.getElementById('delete-hobby-btn').addEventListener('click', deleteHobby);
    fetchHobbies();
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