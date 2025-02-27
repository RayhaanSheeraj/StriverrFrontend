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
    <a href="/StriverrFrontend/Striver/striver-steps" class="sidebar-btn bottom-btn">Step tracker</a>
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-hobbies" class="sidebar-btn bottom-btn">Hobbies</a>
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
    <a href="/StriverrFrontend/Striver/striver-coolfacts" class="sidebar-btn bottom-btn">Cool Facts</a>
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

<div class="about-container">
    <h1>About Striver</h1>
    <p>Welcome to Striver, your ultimate companion for personal growth and achievement tracking. Our platform is designed to help you set, track, and achieve your goals in various aspects of life, from fitness to personal development.</p>
    
    <h2>Our Mission</h2>
    <p>At Striver, our mission is to empower individuals to reach their full potential by providing tools and resources that make goal-setting and achievement tracking simple and effective. We believe that everyone has the ability to achieve greatness, and our platform is here to support you every step of the way.</p>
    
    <h2>Features</h2>
    <ul>
        <li><strong>Achievements:</strong> Track your accomplishments and celebrate your successes.</li>
        <li><strong>Challenges:</strong> Take on new challenges to push your limits and grow.</li>
        <li><strong>AI Assistance:</strong> Get personalized recommendations and insights from our AI.</li>
        <li><strong>Step Tracker:</strong> Monitor your daily steps and stay active.</li>
        <li><strong>Bucket List:</strong> Create and manage your bucket list items.</li>
        <li><strong>Hobbies:</strong> Explore and track your hobbies and interests.</li>
        <li><strong>Quotes:</strong> Get inspired by motivational quotes.</li>
        <li><strong>Cool Facts:</strong> Learn interesting facts and trivia.</li>
    </ul>
    
    <h2>Meet the Team</h2>
    <div id="team-cards" style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center;"></div>
</div>

<script>
    async function fetchTeamInfo() {
        try {
            const responses = await Promise.all([
                fetch('http://127.0.0.1:8887/api/student/rayhaan'),
                fetch('http://127.0.0.1:8887/api/student/kush'),
                fetch('http://127.0.0.1:8887/api/student/neil'),
                fetch('http://127.0.0.1:8887/api/student/hithin'),
                fetch('http://127.0.0.1:8887/api/student/pradyun'),
                fetch('http://127.0.0.1:8887/api/student/zaid'),
                fetch('http://127.0.0.1:8887/api/student/nikith')
            ]);
    
            const data = await Promise.all(responses.map(response => response.json()));
    
            data.forEach(member => displayTeamInfo(member));
        } catch (error) {
            console.error('Error fetching team info:', error);
        }
    }

    function displayTeamInfo(member) {
        const container = document.getElementById('team-cards');
        
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

        container.appendChild(card);
    }

    fetchTeamInfo();
</script>

<style>
.about-container {
    max-width: 800px;
    margin: 50px auto;
    padding: 20px;
    background-color: #1A252F;
    border-radius: 10px;
    border: 1px solid #28cee8;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    color: #fff;
    text-align: center;
}

.about-container h1, .about-container h2 {
    color: #00d4ff;
}

.about-container ul {
    list-style-type: none;
    padding: 0;
}

.about-container ul li {
    background: #252535;
    margin: 10px 0;
    padding: 10px;
    border-radius: 5px;
}

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