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
</div>

<style>
    body {
        background-image: url("../../images/background9674.png");
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        background-attachment: fixed;
        font-family: 'Arial', sans-serif;
        line-height: 1.6;
        color: #fff;
    }

    /* Sidebar */
    .sidebar {
        position: fixed;
        top: 0;
        left: 0;
        width: 180px;
        height: 100%;
        background-color: #121212;
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
        transition: background 0.3s, transform 0.3s;
    }

    .bottom-btn {
        margin-top: auto; /* Pushes the Profile button to the bottom */
    }

    .sidebar-btn:hover {
        background-color: #1e1e1e;
        transform: scale(1.05);
    }

    .sidebar-btn.active {
        background-color: #333;
        font-weight: bold;
    }

    /* Main Content */
    .content {
        margin-left: 200px;
        padding: 40px;
    }

    h2 {
        font-size: 36px;
        margin-bottom: 20px;
        text-align: center;
    }

    p {
        font-size: 18px;
        margin-bottom: 20px;
        text-align: justify;
    }

    .about-grid {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
    }

    .card {
        background-color: rgba(0, 0, 0, 0.7);
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .card h3 {
        font-size: 24px;
        margin-bottom: 10px;
    }

    .card p {
        font-size: 16px;
    }

    .join-btn {
        display: block;
        margin: 30px auto;
        background-color: #04AA6D;
        color: white;
        border: none;
        padding: 15px 30px;
        font-size: 18px;
        border-radius: 8px;
        cursor: pointer;
        text-align: center;
        transition: background-color 0.3s ease;
    }

    .join-btn:hover {
        background-color: #037a54;
    }

    /* Customization Styles */
    .customization-container {
        margin-top: 30px;
    }
    .customization-container label {
        font-size: 16px;
        margin-right: 10px;
    }
    .customization-container select, .customization-container input {
        padding: 8px;
        font-size: 14px;
    }
    .btn {
        margin-top: 20px;
        padding: 10px 15px;
        background-color: #00796b;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    .btn:hover {
        background-color: #004d40;
    }
    .reset-btn {
        background-color: #ff5722;
        margin-left: 10px;
    }
</style>

<div class="content">
    <h2>About Striver</h2>

    <p>
        Welcome to <strong>Striver</strong>, a platform designed to celebrate personal achievements and provide support during challenges. Whether you're aiming for growth, reflecting on milestones, or seeking a community, Striver is here for you.
    </p>

    <div class="about-grid">
        <div class="card">
            <h3>🌟 Empowerment</h3>
            <p>We help individuals share their milestones, connect with others, and celebrate every step forward, no matter how small.</p>
        </div>

        <div class="card">
            <h3>💬 Connection</h3>
            <p>Engage in open and supportive conversations through our anonymous chat system, fostering empathy and understanding.</p>
        </div>

        <div class="card">
            <h3>🤖 AI Companion</h3>
            <p>Meet Gemini, our AI-powered assistant, offering personalized guidance and encouragement throughout your journey.</p>
        </div>

        <div class="card">
            <h3>📈 Growth</h3>
            <p>Explore stories of triumph and progress on the home page, inspiring growth in yourself and others.</p>
        </div>
    </div>

    <p>
        Striver isn't just a platform; it's a community where achievements are celebrated, challenges are met with encouragement, and every story inspires growth. Together, let's create a world where progress is shared and celebrated.
    </p>

    <a href="/Sprint-4-CSP-Project-Frontend---Neil-Rayhaan-Hithin-Nikith-Zaid-Pradyun/Striver/striver-achievements" class="join-btn">Join Us Today</a>

    <!-- Customization Section -->
    <div class="customization-container">
        <h3>Customize Your Experience</h3>
        <div>
            <label for="bg-color">Background Color:</label>
            <input type="color" id="bg-color" onchange="customizePage()">
        </div>
        <div>
            <label for="text-color">Text Color:</label>
            <input type="color" id="text-color" onchange="customizePage()">
        </div>
        <div>
            <label for="font-size">Font Size:</label>
            <select id="font-size" onchange="customizePage()">
                <option value="14px">Small</option>
                <option value="18px">Medium</option>
                <option value="22px">Large</option>
            </select>
        </div>
        <button class="btn" onclick="applyCustomizations()">Apply Customizations</button>
        <button class="btn reset-btn" onclick="resetCustomizations()">Reset to Default</button>
    </div>
</div>

<script>
    // Function to customize the page's background, text color, and font size
    function customizePage() {
        let bgColor = document.getElementById('bg-color').value;
        let textColor = document.getElementById('text-color').value;
        let fontSize = document.getElementById('font-size').value;

        // Set the styles dynamically for the page elements
        document.body.style.backgroundColor = bgColor;
        document.body.style.color = textColor;
        document.body.style.fontSize = fontSize;

        // Apply custom styles to specific elements (like text in cards)
        document.querySelectorAll('.card').forEach(function(card) {
            card.style.backgroundColor = bgColor;  // Update card background color
            card.style.color = textColor;  // Update text color inside cards
        });

        document.querySelectorAll('.join-btn').forEach(function(btn) {
            btn.style.fontSize = fontSize;  // Change font size of the button
        });

        document.querySelectorAll('h2, h3, p').forEach(function(el) {
            el.style.fontSize = fontSize;  // Change font size of headings and paragraphs
        });
    }

    // Function to apply customizations
    function applyCustomizations() {
        alert('Customizations Applied!');
    }

    // Function to reset customizations to the default settings
    function resetCustomizations() {
        // Reset background and text color to default
        document.body.style.backgroundColor = '#f4f4f4';
        document.body.style.color = '#333';
        document.body.style.fontSize = '16px';

        // Reset input fields to default
        document.getElementById('bg-color').value = '#f4f4f4';
        document.getElementById('text-color').value = '#333';
        document.getElementById('font-size').value = '16px';

        // Reset other elements to default
        customizePage();  // Reapply default settings
    }
</script>