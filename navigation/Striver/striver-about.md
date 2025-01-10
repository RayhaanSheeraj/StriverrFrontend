---
layout: base
title: Striver About
search_exclude: true
permalink: /Striver/striver-about
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<div class="sidebar">
    <a href="/StriverrFrontend/Striver/striver-achievements" class="sidebar-btn">⭐️ Achievements</a>
    <a href="/StriverrFrontend/Striver/striver-challenges" class="sidebar-btn">📉 Challenges</a>
    <a href="/StriverrFrontend/Striver/striver-ai" class="sidebar-btn">🤖 AI</a>
    <a href="/StriverrFrontend/Striver/striver-about" class="sidebar-btn">❓ About</a>
    <a href="/StriverrFrontend/Striver/striver-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
    <a href="/StriverrFrontend/Striver/striver-qotd" class="sidebar-btn bottom-btn">QOTD</a>
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
<div id="team-cards" style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center;"></div>

<script>
    async function fetchTeamInfo() {
        try {
            // Fetch data from multiple endpoints (e.g., /api/derek, /api/john, /api/sarah)
            const responses = await Promise.all([
                fetch('http://127.0.0.1:8887/api/student/rayhaan'),
                fetch('http://127.0.0.1:8887/api/student/kush'),
                fetch('http://127.0.0.1:8887/api/student/neil'),
                fetch('http://127.0.0.1:8887/api/student/hithin'),
                fetch('http://127.0.0.1:8887/api/student/pradyun'),
                fetch('http://127.0.0.1:8887/api/student/zaid'),
                fetch('http://127.0.0.1:8887/api/student/nikith')
            ]);
    
            // Convert all the responses to JSON
            const data = await Promise.all(responses.map(response => response.json()));
    
            // Display team info using the data returned by the backend
            data.forEach(member => displayTeamInfo(member)); // Display each member's info
        } catch (error) {
            console.error('Error fetching team info:', error);
        }
    }

function displayTeamInfo(member) {
    const container = document.getElementById('team-cards');
    
    // Create the team card with the data
    const card = document.createElement('div');
    card.className = 'team-card';

    const name = document.createElement('h3');
    name.textContent = member.name;
    card.appendChild(name);

    const age = document.createElement('p');
    age.textContent = `Age: ${member.age}`;
    card.appendChild(age);

    const favoriteSubject = document.createElement('p');
    favoriteSubject.textContent = `Favorite Subject: ${member.favorite_subject}`;
    card.appendChild(favoriteSubject);

    const favoriteColor = document.createElement('p');
    favoriteColor.textContent = `Favorite Color: ${member.favorite_color}`;
    card.appendChild(favoriteColor);

    // Add the card to the container
    container.appendChild(card);
}

fetchTeamInfo();
</script>

<style>
#team-cards {
    font-family: 'Arial', sans-serif;
    margin: 20px auto;
}

.team-card {
    background: linear-gradient(145deg, #1e1e2f, #252535);
    border-radius: 10px;
    color: #fff;
    padding: 20px;
    width: 300px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    text-align: center;
    transition: transform 0.3s;
}

.team-card:hover {
    transform: scale(1.05);
}

.team-card h3 {
    margin-bottom: 10px;
    font-size: 1.5em;
    color: #00d4ff;
}

.team-card p {
    margin: 5px 0;
    font-size: 1em;
}

.team-card a {
    color: #00d4ff;
    text-decoration: none;
}

.team-card a:hover {
    text-decoration: underline;
}
</style>