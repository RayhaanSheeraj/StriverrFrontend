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
    <a href="/StriverrFrontend/Striver/striver-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
</div>

<h1 style="color:cyan;">Achievements</h1>
Share your achievements with others!
<br>
<br>

<div class="main">
    <div id="sidebar"></div>
    <div class="content">
        <div class="form-container">
            <form id="channelForm">
                <div class="form-inputs">
                    <input type="text" id="title" name="title" placeholder="Enter Title Here" required>
                    <input type="file" id="fileInput" name="fileInput" style="display: none;">
                    <button type="button" onclick="document.getElementById('fileInput').click()" class="file-button">➕</button>
                </div>
                <textarea id="textArea" name="textArea" placeholder="Post Here" required></textarea>
                <button type="submit">Post</button>
            </form>
        </div>
        <div id="channels"></div>
    <div>
</div>
<div id="imageTest"></div>

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
        background-color: #f4f4f4;
        border-radius: 12px;
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
        border: 1px solid #ddd;
        font-size: 16px;
    }

    .file-button {
        padding: 10px;
        background-color: #333;
        color: white;
        border: none;
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
        border: 1px solid #ddd;
        font-size: 16px;
        margin-top: 10px;
        resize: none;
        height: 100px;
    }

    button[type="submit"] {
        align-self: flex-start;
        padding: 10px 20px;
        background-color: #1da1f2;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        margin-top: 10px;
        transition: background-color 0.2s ease;
    }

    button[type="submit"]:hover {
        background-color: #1a91da;
    }

    /* Channels Container */
    #channels {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        padding-top: 20px;
    }

    /* Post Cards Styling */
    .card {
        width: calc(50% - 20px);
        min-width: 300px;
        padding: 20px;
        background-color: #ffffff;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
        text-align: left;
    }

    .card-title {
        font-size: 1.2em;
        font-weight: bold;
        color: #333;
    }

    .card-description {
        color: #555;
        font-size: 1em;
        margin-top: 10px;
    }

    .delete-button, .comment-button {
        background-color: #ff4d4d;
        color: white;
        border: none;
        padding: 8px 12px;
        border-radius: 4px;
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
</script>

<script type="module">
    import { pythonURI, fetchOptions } from '../assets/js/api/config.js';
    const container = document.getElementById("channels");

    function openChatRoom(button) {
        const channelId = button.getAttribute("id");
        window.location.href = `{{site.baseurl}}/Striver/striver-achievements?channelId=${channelId}`;
    }

    async function fetchUser() {
        const response = await fetch(`${pythonURI}/api/user`, fetchOptions);
        const user = await response.json();
        console.log(user);
        return user;
    }

    const user = fetchUser();

    async function fetchChannels() {
        try {
            const groupName = 'Striver';
            const responseData = {
                group_name: groupName,
            };
            // add filter to get only messages from this channel
            const response = await fetch(`${pythonURI}/api/channels/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(responseData)
            });

            if (!response.ok) {
                throw new Error('Failed to fetch channels: ' + response.statusText);
            }
            const channels = await response.json();
            container.innerHTML = "";

            channels.forEach(channel => {
                const card = document.createElement("div");
                card.classList.add("card");

                const title = document.createElement("h3");
                title.classList.add("card-title");
                title.textContent = channel.name;

                // const imageBox = document.createElement("div");
                // title.classList.add("image-box");

                const description = document.createElement("p");
                description.classList.add("card-description");
                description.textContent = channel.attributes["content"];

                const deleteButton = document.createElement("button");
                deleteButton.classList.add("delete-button");
                deleteButton.textContent = "Delete";

                const commentButton = document.createElement("button");
                commentButton.classList.add("comment-button");
                commentButton.textContent = "Comment";
                commentButton.setAttribute("id", channel.id);

                commentButton.onclick = function () {
                    openChatRoom(commentButton);
                };

                card.appendChild(title);
                card.appendChild(description);
                card.appendChild(deleteButton);
                card.appendChild(commentButton);

                container.appendChild(card);
            });
        } catch (error) {
            console.error('Error fetching channels:', error);
        }
    }

    document.getElementById('channelForm').addEventListener('submit', async function(event) {
        event.preventDefault();

        const title = document.getElementById('title').value;
        const content = document.getElementById('textArea').value;
        const group_id = 9;

        const channelData = {
            name: title,
            group_id: group_id,
            attributes: {"content": content}
        };

        try {
            const response = await fetch(`${pythonURI}/api/channels`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(channelData)
            });

            if (!response.ok) {
                throw new Error('Failed to add channel: ' + response.statusText);
            }

            fetchChannels();
            document.getElementById('channelForm').reset();
        } catch (error) {
            console.error('Error adding channel:', error);
            alert('Error adding channel: ' + error.message);
        }
    });

    fetchChannels();
</script>
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