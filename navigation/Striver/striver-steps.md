--- 
layout: base
title: Striver About
search_exclude: true
permalink: /Striver/striver-steps
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
</div>
<style>
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
        margin-top: auto; 
    }
</style>
<div class="Steps-container">
    <h2>Steps Tracker</h2>

    <!-- Form to add steps -->
    <div class="step-form">
        <input type="number" id="steps-input" placeholder="Enter steps" />
        <button onclick="submitSteps()">Submit Steps</button>
    </div>

    <!-- Display the last recorded steps -->
    <div id="last-recorded-steps" class="qotd-container">
        <h2>Last Recorded Steps:</h2>
        <p id="steps-display">Loading...</p>
        <p id="motivation-message"></p>
    </div>
</div>

<style>
    .qotd-container {
        margin: 20px;
        padding: 20px;
        background-color: #f9f9f9;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        text-align: center;
    }
    .qotd-container h2 {
        margin-bottom: 10px;
        color: #333;
    }
    .qotd-container p {
        font-size: 18px;
        color: #555;
    }
    .step-form {
        margin-bottom: 20px;
    }
    #steps-input {
        padding: 10px;
        font-size: 16px;
        width: 150px;
    }
    button {
        padding: 10px 20px;
        background-color: #4CAF50;
        color: white;
        border: none;
        cursor: pointer;
    }
    button:hover {
        background-color: #45a049;
    }
</style>

<script>
    // Function to fetch the last recorded steps
    async function fetchLastSteps() {
        try {
            const response = await fetch('http://127.0.0.1:8887/api/steps', {
                method: 'GET',
                credentials: 'include',  // Ensure JWT cookie is sent with the request
            });

            if (response.ok) {
                const data = await response.json();
                const steps = data.steps;
                document.getElementById('steps-display').innerText = steps;
                displayMotivationMessage(steps);
            } else {
                document.getElementById('steps-display').innerText = 'Error fetching steps';
            }
        } catch (error) {
            document.getElementById('steps-display').innerText = 'Error fetching steps';
        }
    }

    // Function to display motivational message
    // Function to display motivational message
    function displayMotivationMessage(steps) {
        const messageElement = document.getElementById('motivation-message');
        if (steps >= 6000) {
            messageElement.innerText = 'Great Job!';
        } else if (steps >= 4000) {
            messageElement.innerText = 'Good job, chat!';
        } else {
            messageElement.innerText = 'Lock in!';
        }
    }


    // Function to submit the steps
    async function submitSteps() {
        const stepsInput = document.getElementById('steps-input');
        const steps = parseInt(stepsInput.value, 10);

        if (isNaN(steps) || steps <= 0) {
            alert('Please enter a valid number of steps');
            return;
        }

        try {
            const response = await fetch('http://127.0.0.1:8887/api/steps', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ steps }),
                credentials: 'include',  // Ensure JWT cookie is sent with the request
            });

            if (response.ok) {
                await fetchLastSteps();  // Fetch and display the updated steps after submission
            } else {
                alert('Error submitting steps');
            }
        } catch (error) {
            alert('Error submitting steps');
        }
    }

    // Fetch the last recorded steps on page load
    window.onload = fetchLastSteps;
</script>
