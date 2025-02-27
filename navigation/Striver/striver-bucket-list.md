---
layout: base
title: Striver Bucket List
search_exclude: true
permalink: /Striver/striver-bucket-list
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
    <a href="/StriverrFrontend/Striver/striver-coolfacts" class="sidebar-btn bottom-btn">Cool Facts</a>
</div>

<h1 style="color:cyan;">Bucket List</h1>
Explore and manage your bucket list!

<div class="container">
    <div class="form-container">
        <h2>Select Category</h2>
        <div>
            <label for="category">Category:</label>
            <select id="category">
                <option value="travel">Travel</option>
                <option value="adventure">Adventure</option>
                <option value="personal">Personal</option>
            </select>
        </div>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Bucket List</h2>
        <ul id="bucket-list"></ul>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Add Bucket List Item</h2>
        <label for="new-bucket-item">Item:</label>
        <input type="text" id="new-bucket-item" placeholder="Enter bucket list item" />
        <label for="new-bucket-desc">Description:</label>
        <input type="text" id="new-bucket-desc" placeholder="Enter description" />
        <label for="new-bucket-category">Category:</label>
        <select id="new-bucket-category">
            <option value="travel">Travel</option>
            <option value="adventure">Adventure</option>
            <option value="personal">Personal</option>
        </select>
        <button id="add-bucket-item-btn">Add Item</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Update Bucket List Item</h2>
        <label for="old-bucket-item">Old Item:</label>
        <input type="text" id="old-bucket-item" placeholder="Old item" />
        <label for="updated-bucket-item">New Item:</label>
        <input type="text" id="updated-bucket-item" placeholder="New item" />
        <label for="update-bucket-category">Category:</label>
        <select id="update-bucket-category">
            <option value="travel">Travel</option>
            <option value="adventure">Adventure</option>
            <option value="personal">Personal</option>
        </select>
        <button id="update-bucket-item-btn">Update Item</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Delete Bucket List Item</h2>
        <label for="delete-bucket-item">Item:</label>
        <input type="text" id="delete-bucket-item" placeholder="Item to delete" />
        <label for="delete-bucket-category">Category:</label>
        <select id="delete-bucket-category">
            <option value="travel">Travel</option>
            <option value="adventure">Adventure</option>
            <option value="personal">Personal</option>
        </select>
        <button id="delete-bucket-item-btn">Delete Item</button>
    </div>
</div>

<script type="module">

import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

window.fetchBucketList = async function fetchBucketList() {
    try {
        const category = document.getElementById('category').value;
        const response = await fetch(`${pythonURI}/api/bucketlist?category=${category}`, {
            ...fetchOptions,
            method: 'GET',
            headers: {
                'Content-Type': 'application/json'
            }
        });

        if (!response.ok) {
            throw new Error('Failed to fetch bucket list: ' + response.statusText);
        }

        const data = await response.json();
        console.log(data);
        const bucketList = document.getElementById('bucket-list');
        bucketList.innerHTML = "";

        data.forEach(item => {
            const titleItem = document.createElement('h3');
            titleItem.textContent = `${item['title']} (${item['category']})`;
            bucketList.appendChild(titleItem);

            const descItem = document.createElement('p');
            descItem.textContent = `${item['description']}`;
            bucketList.appendChild(descItem);

            const breakItem = document.createElement('br');
            bucketList.appendChild(breakItem);
        });
    } catch (error) {
        console.error('Error fetching bucket list:', error);
    }
}

window.addBucketListItem = async function addBucketListItem() {
    const item = document.getElementById('new-bucket-item').value;
    const desc = document.getElementById('new-bucket-desc').value;
    const category = document.getElementById('new-bucket-category').value;

    const title = item;
    const description = desc;

    try {
        const response = await fetch(`${pythonURI}/api/bucketlist`, {
            ...fetchOptions,
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ title, description, category })
        });

        if (!response.ok) {
            throw new Error('Failed to add bucket list item: ' + response.statusText);
        }

        alert('Bucket list item added successfully!');
        document.getElementById('new-bucket-item').value = ''; // Clear input
        document.getElementById('new-bucket-desc').value = '';
        document.getElementById('new-bucket-category').value = '';
        fetchBucketList(); // Refresh bucket list
    } catch (error) {
        console.error('Error adding bucket list item:', error);
        alert('Error adding bucket list item: ' + error.message);
    }
}

async function deleteBucketListItem() {
    const item = document.getElementById('delete-bucket-item').value.trim();
    const category = document.getElementById('delete-bucket-category').value.trim();

    if (!item || !category) {
        alert("Please enter both item and category.");
        return;
    }

    try {
        const response = await fetch(`${pythonURI}/api/bucketlist`, {
            ...fetchOptions,
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ title: item, category: category })
        });

        if (!response.ok) {
            throw new Error('Failed to delete bucket list item: ' + response.statusText);
        }

        alert('Bucket list item deleted successfully!');
        document.getElementById('delete-bucket-item').value = ''; // Clear input
        document.getElementById('delete-bucket-category').value = ''; 
        fetchBucketList(); // Refresh bucket list
    } catch (error) {
        console.error('Error deleting bucket list item:', error);
        alert('Error deleting bucket list item: ' + error.message);
    }
}

document.getElementById('category').addEventListener('change', fetchBucketList);
document.getElementById('add-bucket-item-btn').addEventListener('click', addBucketListItem);
document.getElementById('update-bucket-item-btn').addEventListener('click', putBucketListItem);
document.getElementById('delete-bucket-item-btn').addEventListener('click', deleteBucketListItem);
fetchBucketList();
</script>

<style>
/* General Styles */
body {
  font-family: Arial, sans-serif;
  background-color: #1A252F;
  color: #fff;
  margin: 0;
  padding: 0;
  border: 1px solid #28cee8;
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