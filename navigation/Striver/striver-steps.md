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
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-hobbies" class="sidebar-btn bottom-btn">Hobbies</a>
    <a href="/StriverrFrontend/Striver/striver-coolfacts" class="sidebar-btn bottom-btn">Cool Facts</a>
    <a href="/StriverrFrontend/Striver/striver-goals" class="sidebar-btn bottom-btn">🥅 Goals</a>
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
<div class="steps-container">
    <h2>Steps Tracker</h2>
    <div class="step-form">
        <input type="number" id="steps-input" placeholder="Enter steps" />
        <button onclick="submitSteps()">Submit Steps</button>
        <button onclick="updateSteps()">Update</button>
        <button onclick="deleteSteps()">Delete</button>
    </div>
    <div id="last-recorded-steps" class="qotd-container">
        <h3>Last Recorded Steps:</h3>
        <p id="steps-display">Error fetching steps</p>
        <p id="motivation-message"></p>
    </div>
</div>

<style>
    /* General Layout */
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #1e1e2f;
        color: #fff;
    }

    .steps-container {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        background-color: #1A252F;
        border-radius: 10px;
        border: 1px solid #28cee8;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        text-align: center;
    }

    h2 {
        font-size: 24px;
        margin-bottom: 20px;
    }

    h3 {
        font-size: 20px;
        margin-top: 30px;
    }

    /* Form Styling */
    .step-form {
        margin-bottom: 20px;
        display: flex;
        justify-content: center;
        gap: 10px;
    }

    #steps-input {
        padding: 10px;
        font-size: 16px;
        width: 200px;
        border: 1px solid #28cee8;
        border-radius: 5px;
        background-color: #1A252F;
        color: white;
    }

    #steps-input::placeholder {
        color: #aaa;
    }

    button {
        padding: 10px 20px;
        font-size: 16px;
        background-color: #4CAF50;
        color: white;
        border: 1px solid #28cee8;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #45a049;
    }

    /* Display Section */
    #last-recorded-steps {
        margin-top: 20px;
        padding: 15px;
        background-color: #1A252F;
        border-radius: 5px;
        border: 1px solid #28cee8;
    }

    p {
        font-size: 16px;
        margin: 5px 0;
    }
</style>

<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

// Function to fetch the last recorded steps
window.fetchLastSteps = async function fetchLastSteps() {
    try {
        const response = await fetch(`${pythonURI}/api/steps`, {
            method: 'GET',
            credentials: 'include', // Ensure JWT cookie is sent with the request
        });

        if (response.ok) {
            const data = await response.json();
            const stepCount = data.steps.steps; // Accessing the steps property in the nested object
            document.getElementById('steps-display').innerText = stepCount;
            displayMotivationMessage(stepCount);
        } else {
            document.getElementById('steps-display').innerText = 'Error fetching steps';
        }
    } catch (error) {
        document.getElementById('steps-display').innerText = 'Error fetching steps';
    }
}

// Function to display motivational message
function displayMotivationMessage(steps) {
    const messageElement = document.getElementById('motivation-message');
    if (steps >= 6000) {
        messageElement.innerText = 'Great Job!';
    } else if (steps >= 4000) {
        messageElement.innerText = 'Good job!';
    } else {
        messageElement.innerText = 'Lock in!';
    }
}

// Function to submit the steps
window.submitSteps = async function submitSteps() {
    const stepsInput = document.getElementById('steps-input');
    const steps = parseInt(stepsInput.value, 10);

    if (isNaN(steps) || steps <= 0) {
        alert('Please enter a valid number of steps');
        return;
    }

    try {
        const response = await fetch(`${pythonURI}/api/steps`, {
            ...fetchOptions,
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

// Function to update the steps
window.updateSteps = async function updateSteps() {
    const steps = parseInt(prompt('Please enter the new number of steps:'), 10);

    if (isNaN(steps) || steps <= 0) {
        alert('Please enter a valid number of steps');
        return;
    }

    try {
        const response = await fetch(`${pythonURI}/api/steps`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ steps }),
            credentials: 'include',  // Ensure JWT cookie is sent with the request
        });

        if (response.ok) {
            await fetchLastSteps();  // Fetch and display the updated steps after submission
        } else {
            alert('Error updating steps');
        }
    } catch (error) {
        alert('Error updating steps');
    }
}

// Function to delete the steps
window.deleteSteps = async function deleteSteps() {
    try {
        const response = await fetch(`${pythonURI}/api/steps`, {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            },
            credentials: 'include', // Ensure JWT cookie is sent with the request
        });

        if (response.ok) {
            document.getElementById('steps-display').innerText = 'No steps recorded';
        } else {
            const errorData = await response.json();
            alert('Error deleting steps: ' + errorData.message);
        }
    } catch (error) {
        console.error('Error deleting steps:', error);
        alert('Error deleting steps: ' + error.message);
    }
}

// Fetch the last recorded steps on page load
document.addEventListener('DOMContentLoaded', fetchLastSteps);

</script>