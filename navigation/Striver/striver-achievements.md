---
layout: base
title: Striver Home Page
search_exclude: true
permalink: /Striver/striver-achievements
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<div class="sidebar">
    <a href="/StriverrFrontend/Striver/striver-achievements" class="sidebar-btn">⭐️ Achievements</a>
    <a href="/StriverrFrontend/Striver/striver-challenges" class="sidebar-btn">📉 Challenges</a>
    <a href="/StriverrFrontend/Striver/striver-ai" class="sidebar-btn">🤖 AI</a>
    <a href="/StriverrFrontend/Striver/striver-about" class="sidebar-btn">❓ About</a>
    <a href="/StriverrFrontend/Striver/striverr-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
    <a href="/StriverrFrontend/Striver/striver-steps" class="sidebar-btn bottom-btn">Step tracker</a>
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-hobbies" class="sidebar-btn bottom-btn">Hobbies</a>
    <a href="/StriverrFrontend/Striver/striver-coolfacts" class="sidebar-btn bottom-btn">Cool Facts</a>
    <a href="/StriverrFrontend/Striver/striver-goals" class="sidebar-btn bottom-btn">🥅 Goals</a>
</div>

<h1 style="color:cyan;">Achievements</h1>
Share your achievements with others!
<br>
<br>

<style>
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
        color:rgb(0, 0, 0);
    }
    .form-container label {
        margin-bottom: 5px;
    }
    .form-container input, .form-container textarea, .form-container select {
        margin-bottom: 10px;
        padding: 10px;
        border-radius: 5px;
        border: none;
        width: 100%;
    }
    .form-container button {
        padding: 10px;
        border-radius: 5px;
        border: none;
        background-color: #1A252F;
        color: #2C3E50;
        cursor: pointer;
    }
</style>

<div class="container">
    <div class="form-container">
        <h2 style="color:#28cee8;">Select Group and Channel</h2>
        <form id="selectionForm">
            <label style="color:#28cee8;" for="group_id">Group:</label>
            <select id="group_id" name="group_id" required>
                <option value="">Select a group</option>
            </select>
            <label style="color:#28cee8;" for="channel_id">Channel:</label>
            <select id="channel_id" name="channel_id" required>
                <option value="">Select a channel</option>
            </select>
            <button type="submit">Select</button>
        </form>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2 style="color:#28cee8;">Add New Post</h2>
        <form id="postForm">
            <label style="color:#28cee8;" for="title">Title:</label>
            <input type="text" id="title" name="title" required>
            <label style="color:#28cee8;" for="comment">Comment:</label>
            <textarea id="comment" name="comment" required></textarea>
            <button type="submit">Add Post</button>
        </form>
    </div>
</div>

<div class="container">
    <div id="data" class="data">
        <div class="left-side">
            <p id="count"></p>
        </div>
        <div class="details" id="details">
        </div>
    </div>
</div>

<script type="module">
    // Import server URI and standard fetch options
    import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

    /**
     * Fetch groups for dropdown selection
     * User picks from dropdown
     */
    async function fetchGroups() {
        try {
            const response = await fetch(`${pythonURI}/api/groups/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ section_name: "Home Page" }) // Adjust the section name as needed
            });
            if (!response.ok) {
                throw new Error('Failed to fetch groups: ' + response.statusText);
            }
            const groups = await response.json();
            const groupSelect = document.getElementById('group_id');
            groups.forEach(group => {
                const option = document.createElement('option');
                option.value = group.name; // Use group name for payload
                option.textContent = group.name;
                groupSelect.appendChild(option);
            });
        } catch (error) {
            console.error('Error fetching groups:', error);
        }
    }

    /**
     * Fetch channels based on selected group
     * User picks from dropdown
     */
    async function fetchChannels(groupName) {
        try {
            const response = await fetch(`${pythonURI}/api/channels/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ group_name: groupName })
            });
            if (!response.ok) {
                throw new Error('Failed to fetch channels: ' + response.statusText);
            }
            const channels = await response.json();
            const channelSelect = document.getElementById('channel_id');
            channelSelect.innerHTML = '<option value="">Select a channel</option>'; // Reset channels
            channels.forEach(channel => {
                const option = document.createElement('option');
                option.value = channel.id;
                option.textContent = channel.name;
                channelSelect.appendChild(option);
            });
        } catch (error) {
            console.error('Error fetching channels:', error);
        }
    }

    /**
      * Handle group selection change
      * Channel Dropdown refresh to match group_id change
      */
    document.getElementById('group_id').addEventListener('change', function() {
        const groupName = this.value;
        if (groupName) {
            fetchChannels(groupName);
        } else {
            document.getElementById('channel_id').innerHTML = '<option value="">Select a channel</option>'; // Reset channels
        }
    });

    /**
     * Handle form submission for selection
     * Select Button: Computer fetches and displays posts
     */
    document.getElementById('selectionForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const groupId = document.getElementById('group_id').value;
        const channelId = document.getElementById('channel_id').value;
        if (groupId && channelId) {
            fetchData(channelId);
        } else {
            alert('Please select both group and channel.');
        }
    });

    /**
     * Handle form submission for adding a post
     * Add Form Button: Computer handles form submission with request
     */
    document.getElementById('postForm').addEventListener('submit', async function(event) {
        event.preventDefault();

        // Extract data from form
        const title = document.getElementById('title').value;
        const comment = document.getElementById('comment').value;
        const channelId = document.getElementById('channel_id').value;

        // Create API payload
        const postData = {
            title: title,
            comment: comment,
            channel_id: channelId
        };

        // Trap errors
        try {
            // Send POST request to backend, purpose is to write to database
            const response = await fetch(`${pythonURI}/api/post`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(postData)
            });

            if (!response.ok) {
                throw new Error('Failed to add post: ' + response.statusText);
            }

            // Successful post
            const result = await response.json();
            alert('Post added successfully!');
            document.getElementById('postForm').reset();
            fetchData(channelId);
        } catch (error) {
            // Present alert on error from backend
            console.error('Error adding post:', error);
            alert('Error adding post: ' + error.message);
        }
    });

    /**
     * Fetch posts based on selected channel
     * Handle response: Fetch and display posts
     */
    async function fetchData(channelId) {
        try {
            const response = await fetch(`${pythonURI}/api/posts/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ channel_id: channelId })
            });
            if (!response.ok) {
                throw new Error('Failed to fetch posts: ' + response.statusText);
            }

            // Parse the JSON data
            const postData = await response.json();

            // Extract posts count
            const postCount = postData.length || 0;

            // Update the HTML elements with the data
            document.getElementById('count').innerHTML = `<h2>Count ${postCount}</h2>`;

            // Get the details div
            const detailsDiv = document.getElementById('details');
            detailsDiv.innerHTML = ''; // Clear previous posts

            // Iterate over the postData and create HTML elements for each item
            postData.forEach(postItem => {
                const postElement = document.createElement('div');
                postElement.className = 'post-item';
                postElement.innerHTML = `
                    <h3>${postItem.title}</h3>
                    <p><strong>Channel:</strong> ${postItem.channel_name}</p>
                    <p><strong>User:</strong> ${postItem.user_name}</p>
                    <p>${postItem.comment}</p>
                `;
                detailsDiv.appendChild(postElement);
            });
            
        } catch (error) {
            console.error('Error fetching data:', error);
        }
    }

    // Fetch groups when the page loads
    fetchGroups(); 
</script>

<style>
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
    .main {
        display: flex;
    }
    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        /* padding-left: 180px; */
    }

    .friends-container {
        display: flex;
        overflow-x: auto; /* horizontal scrolling */
        padding: 10px;
        margin-bottom: 10px;
        margin-top: 20px;
        gap: 10px; 
        scrollbar-width: thin;
        scrollbar-color: #ccc transparent; /* Color for scrollbar */
        width: 750px;
    }

    .friend {
        display: flex;
        flex-direction: column;
        align-items: center;
        position: relative;
        width: 80px; /* Set a width for each profile card */
        text-align: center;
        font-family: Arial, sans-serif;
    }

    .profile-pic {
        width: 60px;
        height: 60px;
        border-radius: 50%; /* Makes the image round */
        overflow: hidden;
        border: 2px solid #ddd;
    }

    .profile-pic img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .friend p {
        margin: 5px 0 0;
        font-size: 14px;
        color: #333;
    }

    .live-badge {
        position: absolute;
        top: -5px;
        left: 15px;
        background-color: #000;
        color: #fff;
        font-size: 12px;
        padding: 2px 6px;
        border-radius: 12px;
        font-weight: bold;
    }

    /* Form Styling */
    .form-container {
        padding: 20px;
        background-color: #1A252F;;
        border-radius: 12px;
        border: 1px solid #28cee8;
        width: calc(100% - 400px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        font-family: Arial, sans-serif;
    }

    .form-inputs {
        display: flex;
        gap: 10px;
        align-items: center;
    }

    #title {
        flex: 1;
        padding: 12px;
        border-radius: 8px;
        font-size: 16px;
    }

    .file-button {
        padding: 10px;
        background-color: #333;
        color: white;
        border: 1px solid #28cee8;
        border-radius: 50%;
        font-size: 18px;
        cursor: pointer;
        width: 40px;
        height: 40px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    #textArea {
        width: 100%;
        padding: 12px;
        border-radius: 8px;
        border: 1px solid #28cee8;
        font-size: 16px;
        margin-top: 10px;
        resize: none;
        height: 100px;
    }

    button[type="submit"] {
        align-self: flex-start;
        padding: 10px 20px;
        background-color:rgb(34, 59, 75);
        color: white;
        border: 1px solid #28cee8;
        border-radius: 8px;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        margin-top: 10px;
        transition: background-color 0.2s ease;
    }

    button[type="submit"]:hover {
        background-color:rgb(3, 54, 85);
    }

    /* Channels Container */
    #channels {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        padding-top: 20px;
        border: 1px solid #28cee8;
    }

    /* Post Cards Styling */
    .card {
        width: calc(50% - 20px);
        min-width: 300px;
        padding: 20px;
        background-color: #2C3E50;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
        text-align: left;
        border: 1px solid #28cee8;
    }

    .card-title {
        font-size: 1.2em;
        font-weight: bold;
        color: #28cee8;
    }

    .card-description {
        color: #28cee8;
        font-size: 1em;
        margin-top: 10px;
    }

    .delete-button, .comment-button {
        background-color: #ff4d4d;
        color: white;
        border: none;
        padding: 8px 12px;
        border-radius: 4px;
        border: 1px solid #28cee8;
        cursor: pointer;
        font-size: 0.9em;
        margin-top: 15px;
        transition: background-color 0.3s ease;
        margin-right: 5px;
    }

    .delete-button:hover, .comment-button:hover {
        background-color: #ff1a1a;
    }
</style>




<script type="module">
    // this is for the images
    // import { pythonURI, fetchOptions } from '../assets/js/api/config.js';
    // const fileInput = document.getElementById('fileInput');
    // const file = fileInput.files[0];
    // if (file) {
    //     const reader = new FileReader();
    //     reader.onload = function() {
    //         const imageTest = document.getElementById('imageTest');
    //         imageTest.innerHTML = `<img src="${reader.result}" alt="Profile Picture">`;
    //     };
    //     reader.readAsDataURL(file);
    // }




    // async function sendProfilePicture(base64String) {
    // const URL = pythonURI + "/api/id/pfp";

    // const options = {
    //     URL,
    //     body: { pfp: base64String },
    //     message: 'profile-message',
    //     callback: () => {
    //         console.log('Profile picture uploaded successfully!');
    //     }
    // };

    // try {
    //     await putUpdate(options);
    // } catch (error) {
    //     console.error('Error uploading profile picture:', error.message);
    //     document.getElementById('profile-message').textContent = 'Error uploading profile picture: ' + error.message;
    // }
    // }

    // async function convertToBase64(file) {
    //     return new Promise((resolve, reject) => {
    //         const reader = new FileReader();
    //         reader.onload = () => resolve(reader.result.split(',')[1]); // Remove the prefix part of the result
    //         reader.onerror = error => reject(error);
    //         reader.readAsDataURL(file);
    //     });
    // }
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
<style>
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
</style>






