---
layout: base
title: Striver Goals
search_exclude: true
permalink: /Striver/striver-goals
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

<h1 style="color:cyan;">GOALS 🥅 🥅 🥅</h1>
<h2 style="color:cyan;">Retrieve a random goal and update your progress!</h2>

<div class="container">
    <div class="form-container">
        <h2>Random Goal</h2>
        <button id="fetch-goal-btn">Generate Random Goal</button>
        <h2>Retrieve Specific Goal</h2>
        <label for="specific-goal-id">Goal ID:</label>
        <input type="text" id="specific-goal-id" placeholder="Enter goal ID" />
        <button id="fetch-specific-goal-btn">Retrieve Goal</button>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Goal Details</h2>
        <ul id="goal-list"></ul>
    </div>
</div>

<div class="container">
    <div class="form-container">
        <h2>Update Goal Progress</h2>
        <label for="goal-id">Goal ID:</label>
        <input type="text" id="goal-id" placeholder="Enter goal ID" />
        <label for="goal-progress">New Progress:</label>
        <input type="text" id="goal-progress" placeholder="Enter updated progress" />
        <button id="update-goal-btn">Update Progress</button>
    </div>
</div>

<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

// Fetch all goals from the backend, pick one at random, and display its details.
window.fetchRandomGoal = async function fetchRandomGoal() {
    try {
        const response = await fetch(`${pythonURI}/api/goals`, fetchOptions);
        if (!response.ok) {
            throw new Error('Failed to fetch goals: ' + response.statusText);
        }
        const goals = await response.json();
        if (!goals.length) {
            alert("No goals found.");
            return;
        }
        const randomIndex = Math.floor(Math.random() * goals.length);
        const goal = goals[randomIndex];
        displayGoal(goal);
    } catch (error) {
        console.error('Error fetching goal:', error);
    }
}

// Fetch a specific goal by ID from the backend and display its details.
window.fetchGoalById = async function fetchGoalById() {
    const goalId = document.getElementById('specific-goal-id').value.trim();
    if (!goalId) {
        alert("Please enter a goal ID");
        return;
    }
    try {
        // Fetch all goals
        const response = await fetch(`${pythonURI}/api/goals`, fetchOptions);
        if (!response.ok) {
            throw new Error('Failed to fetch goals: ' + response.statusText);
        }
        const goals = await response.json();
        // Filter for the goal with the matching ID (using loose equality to handle type conversion)
        const goal = goals.find(g => g.id == goalId);
        if (!goal) {
            alert("No goal found with that ID.");
            return;
        }
        displayGoal(goal);
    } catch (error) {
        console.error("Error fetching specific goal:", error);
        alert("Error fetching specific goal: " + error.message);
    }
}



// Update the displayed goal details in the page.
function displayGoal(goal) {
    const goalList = document.getElementById('goal-list');
    goalList.innerHTML = '';

    const idElem = document.createElement('p');
    idElem.textContent = `ID: ${goal.id}`;
    goalList.appendChild(idElem);

    const outputElem = document.createElement('p');
    outputElem.textContent = `Goal: ${goal.goaloutput}`;
    goalList.appendChild(outputElem);

    const progressElem = document.createElement('p');
    progressElem.textContent = `Progress: ${goal.progress || 'N/A'}`;
    goalList.appendChild(progressElem);
}

// Update a goal's progress using its ID.
window.updateGoalProgress = async function updateGoalProgress() {
    const goalId = document.getElementById('goal-id').value;
    const newProgress = document.getElementById('goal-progress').value;
    if (!goalId || !newProgress) {
        alert("Please enter both Goal ID and new progress.");
        return;
    }
    const putData = { id: goalId, progress: newProgress };

    try {
        const response = await fetch(`${pythonURI}/api/goals`, {
            method: 'PUT',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(putData)
        });
        if (!response.ok) {
            throw new Error(`Failed to update goal: ${response.statusText}`);
        }
        const data = await response.json();
        console.log('Update response:', data);
        alert('Goal progress updated successfully!');
        fetchRandomGoal(); // Refresh the displayed goal
    } catch (error) {
        console.error("Error updating goal:", error);
        alert("Error updating goal: " + error.message);
    }
}

document.getElementById('fetch-goal-btn').addEventListener('click', fetchRandomGoal);
document.getElementById('fetch-specific-goal-btn').addEventListener('click', fetchGoalById);
document.getElementById('update-goal-btn').addEventListener('click', updateGoalProgress);

// Automatically load a random goal on page load.
fetchRandomGoal();
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
.form-container label, 
.form-container input, 
.form-container textarea, 
.form-container select, 
.form-container button {
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
  margin-top: auto;
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
