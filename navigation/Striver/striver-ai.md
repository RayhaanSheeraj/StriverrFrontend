---
layout: base
title: Striver AI
search_exclude: true
permalink: /Striver/striver-ai
author: Hithin
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

<style>
    body {
        background-image: url("../../images/background9674.png");
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        background-attachment: fixed;
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

<div id="main-content">
    <div id="chatPanel">
        <h3>Chat Room</h3>
        <div id="outputDiv"></div>
        <form>
            <button class="plus-button" onclick="triggerFileUpload()">+</button>
            <input type="file" id="file-input" onchange="handleFileUpload(event)">
            <input placeholder="Enter message to send:" type="text" id="messageBox" name="message">
        </form>
    </div>
    <!-- Instructions Frame with Buttons Below -->
    <div class="instructions-frame">
        <div class="instructions-box">
            <h3>Striver is here to assist you</h3>
            <p>Welcome, I am an AI therapist that can give ideas on achievments as well. </p>
            <ul>
                <li>Use the chat to interact with the AI and I will respond with positive reinforcement and feedback.</li>
                <li>Explain your achievments</li>
                <li>This chat bot is powered by Gemini AI</li>
                <li>Continue sharing achievements or ask for guidance on specific topics.</li>
            </ul>
            <span style="color: cyan;">It is an honor to get to hear about you</span>
        </div>
    </div>

        
  

</div>

<style>
    table, th, td {
        border: 1px solid black;
        border-collapse: collapse;
    }
    th, td {
        padding: 5px;
        text-align: left;
    }
    .small {
        font-size: 8px;
    }
    h3 {
        margin-bottom: 10px;
    }
    #main-content {
        display: flex;
        align-content: space-between;
    }
    #userPanel {
        margin-left: auto;
        width: 30%;
    }
    #chatPanel {
        position: relative;
        width: 700px;
        height: 500px;
    }
    #messageBox {
        width: 85%;
        height: 40px;
        padding: 15px 20px;
        font-size: 16px;
        border: 1px solid #ddd;
        outline: none;
        background-color: #f3f3f3;
        border-radius: 30px;
        box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
        color: #333;
    }
    #outputDiv {
        flex-grow: 1;
        overflow-y: auto;
        max-height: calc(100% - 135px);
    }
    form {
        position: absolute;
        bottom: 0;
        width: 100%;
        padding: 10px 0;
    }
    .message-bubble {
        background-color: #218aff;
        padding: 10px;
        border-radius: 10px;
        margin: 5px 0;
        max-width: 80%;
        word-wrap: break-word;
    }
    .ai-bubble {
        background-color: #e0e0e0;
        padding: 10px;
        border-radius: 10px;
        margin: 5px 0;
        max-width: 80%;
        word-wrap: break-word;
        color: #333;
    }
    .cell {
        display: flex;
    }
    .cell-content {
        margin-left: 10px;
    }
    .profile-photo {
        border-radius: 30px;
    }
    .plus-button {
        width: 40px;
        height: 40px;
        color: white;
        border: none;
        border-radius: 50%;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        font-size: 24px;
        outline: none;
    }
    input[type="file"] {
        display: none;
    }
    /* Instructions Box */
    .instructions-box {
        width: 250px;
        padding: 20px;
        background-color: black;
        border: 3px solid cyan; /* Added cyan border */
        border-radius: 8px;
        color: white;
        height: 430px; /* Adjust this value as needed */
        display: flex;
        flex-direction: column;
        /* justify-content: space-between; */
    }

    .instructions-box h3 {
        margin-top: 0;
        font-size: 1.2em;
        font-weight: bold;
        color: #007bff;
    }

    .instructions-box p, .instructions-box ul {
        font-size: 0.9em;
        color: white;
    }
    
    .instructions-box ul {
        padding-left: 20px;
    }

    .guess-options {
        display: flex;
        gap: 0;
        margin-top: 10px;
        padding-top: 10px;
        width: 100%; 
    }

    .guess-button {
        flex: 1;
        padding: 8px 0;
        background-color: #007bff !important;
        color: white !important;
        border: none;
        border-radius: 10;
        font-size: 0.9em;
        cursor: pointer;
        transition: background-color 0.3s ease !important;
    }

    .guess-button:hover {
        background-color: #0056b3 !important;
    }

    .guess-button:active {
        background-color: #003f7f !important;
    }
</style>

<style>
    @keyframes screenFlash {
        0% {
            background-color: white;
        }
        50% {
            background-color: #8B0000;
        }
        100% {
            background-color: white;
        }
    }

    .flash {
        animation: screenFlash 2.5s ease-out;
        height: 100vh;
        width: 100vw;
    }

    #guessPrompt {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: #fff;
        border: 1px solid #ccc;
        padding: 20px;
        text-align: center;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        z-index: 10;
        color: black;
        border-radius: 20px;
    }
    .timestamp {
        font-size: 0.75em;
        color: #666;
        margin-left: 10px;
    }
    .typing-indicator {
        font-style: italic;
        color: #888;
        margin: 5px;
    }
</style>

<script>
    const names = ["Striver"];
    const states = ["Iowa", "California", "New York", "Texas", "Florida", "Nevada", "Ohio", "Michigan"];

    function getRandomItem(array) {
        return array[Math.floor(Math.random() * array.length)];
    }

    const randomName = getRandomItem(names);
    const randomState = getRandomItem(states);
    function displayTrickyMessage() {
        const message = `Loading... You connected to Striver, feel free to share anything!`;

        const outputDiv = document.getElementById('outputDiv');
        const messageElement = document.createElement('div');
        messageElement.classList.add('message-bubble');
        messageElement.textContent = message;

        outputDiv.appendChild(messageElement);
    }

    window.onload = displayTrickyMessage;

async function sendToGeminiAPI(userMessage) {
    const apiKey = "YOUR_SECURE_API_KEY"; // Replace with a securely stored API key
    const modelVersion = 'gemini-1.5-flash-latest';
    const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${modelVersion}:generateContent?key=${apiKey}`;

    try {
        const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                contents: [{
                    parts: [{ 
                        text: `You are Striver, an AI designed to listen to users' challenges, achievements, goals, and struggles, and respond like a supportive best friend or therapist. ${userMessage}` 
                    }]
                }]
            })
        });

        if (!response.ok) {
            throw new Error(`HTTP Error: ${response.status}`);
        }

        const data = await response.json();
        const reply = data?.candidates?.[0]?.content?.parts?.[0]?.text;

        if (!reply) {
            throw new Error('Unexpected API response structure');
        }

        return reply;
    } catch (error) {
        console.error('Error communicating with Gemini API:', error);
        return `An error occurred: ${error.message}. Please try again.`;
    }
}


    let messageCount = 0;
    function incrementMessageCount() {
        messageCount += 1;
        if (messageCount === 5) {
            showGuessPrompt();
        }
    }

    let score = 0;
    const scoreText = document.getElementById('score')
    function submitGuess(answer) {
        if (answer === 'ai') {
            score += 1
            scoreText.innerHTML = `Score: ${score}`
            hideGuessPrompt();
            messageCount = 0;
            document.getElementById('outputDiv').innerHTML = ' ';
        } else {
            score -= 1
            scoreText.innerHTML = `Score: ${score}`
            hideGuessPrompt();
            messageCount = 0;
            document.getElementById('outputDiv').innerHTML = ' ';
        }
    }

    function showGuessPrompt() {
        document.getElementById('guessPrompt').style.display = 'block';
    }

    function hideGuessPrompt() {
        document.getElementById('guessPrompt').style.display = 'none';
    }

    function getCurrentTime() {
        const now = new Date();
        return now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
    }

    function addMessageToChat(message, isAI = false) {
        const messageElement = document.createElement('p');
        messageElement.classList.add(isAI ? 'ai-bubble' : 'message-bubble');
        messageElement.innerHTML = `${message} <span class="timestamp">${getCurrentTime()}</span>`;
        document.getElementById('outputDiv').appendChild(messageElement);
    }

    const storedMessage = localStorage.getItem("storedMessage");
    if(storedMessage) {
        console.log("I tried", storedMessage);

        const aiMessageElement = document.createElement('p');
        aiMessageElement.classList.add('ai-bubble');
        aiMessageElement.textContent = storedMessage;
        document.getElementById('outputDiv').appendChild(aiMessageElement);
        incrementMessageCount();
        
        const messagesDiv = document.getElementById('outputDiv');
        messagesDiv.scrollTop = messagesDiv.scrollHeight;
    }

    // Chat functionality
    document.getElementById('messageBox').addEventListener('keypress', async function(event) {
    if (event.key === 'Enter') {
        event.preventDefault();
        const userMessage = event.target.value;

        addMessageToChat(userMessage);
        event.target.value = '';
        incrementMessageCount();

        const typingIndicator = document.createElement('div');
        typingIndicator.classList.add('typing-indicator');
        typingIndicator.textContent = `${randomName} is typing...`;
        document.getElementById('outputDiv').appendChild(typingIndicator);

        // TODO: Add response delay.
        setTimeout(async () => {
            const aiResponse = await sendToGeminiAPI(userMessage);

            localStorage.setItem("storedMessage", aiResponse);
            console.log(aiResponse);

            const aiMessageElement = document.createElement('p');
            aiMessageElement.classList.add('ai-bubble');
            aiMessageElement.textContent = aiResponse;
            document.getElementById('outputDiv').appendChild(aiMessageElement);
            incrementMessageCount();

            const messagesDiv = document.getElementById('outputDiv');
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }, 1500);
    }
    });

    function triggerFileUpload() {
        event.preventDefault();
        document.getElementById('file-input').click();
    }

    function handleFileUpload(event) {
        const file = event.target.files[0];
        messageContent = document.getElementById('messageBox').text;
        if (file) {
            console.log(`Selected file: ${file.name}`);
            displayFileMessage(file, messageContent);
        }
    }

    function displayFileMessage(file, message='') {
        const outputDiv = document.getElementById('outputDiv');

        const messageElement = document.createElement('div');
        messageElement.classList.add('message-bubble');

        if (message) {
            const textElement = document.createElement('p');
            textElement.innerHTML = `${message} <span class="timestamp">${getCurrentTime()}</span>`;
            messageElement.appendChild(textElement);
        }

        if (file.type.startsWith("image/")) {
            const img = document.createElement('img');
            img.src = URL.createObjectURL(file);
            img.alt = file.name;
            img.style.maxWidth = '200px';
            img.style.maxHeight = '200px';
            messageElement.appendChild(img);
        } else {
            const fileLink = document.createElement('a');
            fileLink.href = URL.createObjectURL(file);
            fileLink.download = file.name;
            fileLink.textContent = `Uploaded File: ${file.name}`;
            messageElement.appendChild(fileLink);
        }

        const timestamp = document.createElement('span');
        timestamp.classList.add('timestamp');
        timestamp.textContent = getCurrentTime(); 
        messageElement.appendChild(timestamp);

        outputDiv.appendChild(messageElement);
    }

    function toggleRedirect() {
    const checkbox = document.getElementById('toggle-switch');
    if (checkbox.checked) {
        window.location.href = '{{site.baseurl}}/create_and_compete/realityroom';
    }
    }

</script>

<div class="customization-panel">
    <h4>Customize Appearance</h4>
    <label for="bgColorSlider">Box Background Color:</label>
    <input type="color" id="bgColorPicker" value="#ffffff" />
    <label for="fontColorPicker">Font Color:</label>
    <input type="color" id="fontColorPicker" value="#ffffff" />
</div>

<style>
    .customization-panel {
        margin-top: 20px;
        background-color: black;
        padding: 10px;
        border: 2px solid cyan; /* Added cyan border */
        border-radius: 8px;
        width: fit-content;
        color: white;
    }
</style>

<script>
    const boxElement = document.querySelector(".instructions-box");
    const bgColorPicker = document.getElementById("bgColorPicker");
    const fontColorPicker = document.getElementById("fontColorPicker");

    bgColorPicker.addEventListener("input", () => {
        boxElement.style.backgroundColor = bgColorPicker.value;
    });

    fontColorPicker.addEventListener("input", () => {
        boxElement.style.color = fontColorPicker.value;
    });

body {
    background: linear-gradient(135deg, #ff7eb3, #ff758c, #ff9a76, #ffcd77, #fff59e, #b0f4e6, #80bfff, #9d74ff, #d96cff);
    background-size: 150% 150%;
    animation: gradientShift 10s ease infinite;
    color: #fff;
}

/* Keyframes for animated gradient background */
@keyframes gradientShift {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}


</script>



