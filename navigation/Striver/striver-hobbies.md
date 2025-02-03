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
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
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

<script type="module">

import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

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
                listItem.style.display = 'flex';
                listItem.style.alignItems = 'center';
                listItem.style.justifyContent = 'space-between';

                const hobbyText = document.createElement('span');
                hobbyText.textContent = hobby;

                const updateButton = document.createElement('button');
                updateButton.textContent = 'Update';
                updateButton.style.marginLeft = '10px'; // Add some space between buttons
                updateButton.style.padding = '2px 5px';
                updateButton.style.fontSize = '12px'; // Make the button smaller
                updateButton.style.width = '60px'; // Make the button smaller horizontally
                updateButton.classList.add('update-btn');
                updateButton.onclick = () => promptUpdateHobby(hobby, category);

                const deleteButton = document.createElement('button');
                deleteButton.textContent = 'Delete';
                deleteButton.style.marginLeft = '10px'; // Add some space between buttons
                deleteButton.style.padding = '2px 5px';
                deleteButton.style.fontSize = '12px'; // Make the button smaller
                deleteButton.style.width = '60px'; // Make the button smaller horizontally
                deleteButton.onclick = () => deleteHobby(hobby, category);

                listItem.appendChild(hobbyText);
                listItem.appendChild(updateButton);
                listItem.appendChild(deleteButton);
                hobbiesList.appendChild(listItem);
            });
        } catch (error) {
            console.error('Error fetching hobbies:', error);
        }
    }

    async function addHobby() {
        const hobbyName = document.getElementById('new-hobby-name').value;
        const category = document.getElementById('new-hobby-category').value;
        const allHobbiesResponse = await fetch(`${pythonURI}/api/hobby`, {
            ...fetchOptions,
            method: 'GET'
        });

        if (!allHobbiesResponse.ok) {
            alert('Failed to fetch all hobbies');
            return;
        }

        const allHobbiesData = await allHobbiesResponse.json();
        const allHobbiesList = allHobbiesData.hobbies.flatMap(hobby => hobby);

        if (allHobbiesList.includes(hobbyName)) {
            alert('Hobby already exists!');
            return;
        }

        try {
            const response = await fetch(`${pythonURI}/api/hobby`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
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

    async function promptUpdateHobby(hobbyName, category) {
        const updatedHobbyName = prompt('Enter new hobby name:', hobbyName);
        const allHobbiesResponse = await fetch(`${pythonURI}/api/hobby`, {
            ...fetchOptions,
            method: 'GET'
        });

        if (!allHobbiesResponse.ok) {
            alert('Failed to fetch all hobbies');
            return;
        }

        const allHobbiesData = await allHobbiesResponse.json();
        const allHobbiesList = allHobbiesData.hobbies.flatMap(hobby => hobby);

        if (allHobbiesList.includes(updatedHobbyName)) {
            alert('Hobby already exists!');
            return;
        }

        if (updatedHobbyName) {
            try {
                const response = await fetch(`${pythonURI}/api/hobby`, {
                    ...fetchOptions,
                    method: 'PUT',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({ old_name: hobbyName, name: updatedHobbyName, category: category })
                });

                if (!response.ok) {
                    throw new Error('Failed to update hobby: ' + response.statusText);
                }

                alert('Hobby updated successfully!');
                fetchHobbies(); // Refresh hobbies list
            } catch (error) {
                console.error('Error updating hobby:', error);
                alert('Error updating hobby: ' + error.message);
            }
        }
    }

    async function deleteHobby(hobbyName, category) {
        try {
            const response = await fetch(`${pythonURI}/api/hobby`, {
                ...fetchOptions,
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ name: hobbyName, category: category })
            });

            if (!response.ok) {
                throw new Error('Failed to delete hobby: ' + response.statusText);
            }

            alert('Hobby deleted successfully!');
            fetchHobbies(); // Refresh hobbies list
        } catch (error) {
            console.error('Error deleting hobby:', error);
            alert('Error deleting hobby: ' + error.message);
        }
    }

    document.getElementById('category').addEventListener('change', fetchHobbies);
    document.getElementById('add-hobby-btn').addEventListener('click', addHobby);
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

#hobbies-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #34495E;
  padding: 10px;
  margin-bottom: 5px;
  border-radius: 5px;
}

#hobbies-list button {
  background-color: #E74C3C;
  color: #ECF0F1;
  border: none;
  padding: 2px 5px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px; /* Make the button smaller */
  width: 60px; /* Make the button smaller horizontally */
  margin-left: 0; /* Move the button closer */
}

#hobbies-list button.update-btn {
  background-color: #3498DB;
  margin-left: 10px; /* Add some space between buttons */
}

#hobbies-list button.update-btn:hover {
  background-color: #2980B9;
}

#hobbies-list span {
  flex-grow: 1; /* Ensure the text takes up available space */
}

#hobbies-list button:hover {
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
  background-color: #1e1e1e;
  transform: scale(1.05);
}

.sidebar-btn.active {
  background-color: #333;
  font-weight: bold;
}
</style>