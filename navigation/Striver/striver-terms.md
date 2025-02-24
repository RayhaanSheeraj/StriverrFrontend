---
layout: base
title: Striver Terms
search_exclude: true
permalink: /Striver/striver-terms
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
        margin-top: auto;
    }

    /* Popup Styles */
    .terms-popup {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 9999;
    }
    .terms-content {
        background: white;
        padding: 20px;
        border-radius: 8px;
        text-align: center;
        max-width: 400px;
        width: 90%;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    }
    .terms-content h3 {
        margin-bottom: 10px;
        color: #333;
    }
    .terms-content p {
        margin-bottom: 20px;
        color: #555;
    }
    .accept-btn {
        background-color: #121212;
        color: white;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
        transition: background-color 0.3s;
    }
    .accept-btn:hover {
        background-color: #444;
    }
</style>

<h2>Terms</h2>

<p> As this is a school-related website, please make sure you recognize that anything you post that breaks any of the below rules may get you in legal trouble. If you are just here to keep a safe community and have fun, enjoy!</p>

<p> 1. Respectful Communication: Always communicate with respect. No abusive, offensive, or hateful language will be tolerated.</p>
<p> 2. No Spamming: Avoid posting repetitive messages, advertisements, or irrelevant links.</p>
<p> 3. Privacy Respect: Do not share personal information of yourself or others without consent.</p>
<p> 4. No Harassment: Harassment, bullying, or targeting individuals or groups will result in immediate action.</p>
<p> 5. Appropriate Content: Share content that is appropriate for all audiences. No explicit, violent, or illegal content.</p>
<p> 6. Report Violations: If you see any rule violations, report them to the moderators immediately.</p>
<p> 7. Follow Platform Guidelines: Adhere to the specific guidelines and terms of service of the platform.</p>
<p> 8. Constructive Feedback: Provide feedback in a constructive manner. Avoid negative or destructive criticism.</p>
<p> 9. No Impersonation: Do not impersonate other users, moderators, or public figures.</p>
<p> 10. Language: Use the primary language of the chatroom or social media site to ensure clear communication.</p>
<p> 11. Respect Moderators: Follow the instructions of moderators and respect their decisions.</p>
<p> 12. No Illegal Activities: Any form of illegal activity will be reported to the authorities and result in a ban.</p>

<p> By participating in this chatroom/social media site, you agree to follow these rules. Failure to comply may result in warnings, temporary bans, or permanent removal from the platform. </p>

<script>
    
    document.addEventListener('DOMContentLoaded', function () {
        
        const popup = document.createElement('div');
        popup.id = 'terms-popup';
        popup.className = 'terms-popup';

        
        popup.innerHTML = `
            <div class="terms-content">
                <h3>Welcome to Striver!</h3>
                <p>By accessing this platform, you agree to adhere to our Terms and Conditions. Please review the rules below to ensure a safe and respectful experience for all users.</p>
                <p>Click "Accept" to proceed.</p>
                <button id="accept-terms" class="accept-btn">Accept</button>
            </div>
        `;

        
        document.body.appendChild(popup);

        
        document.getElementById('accept-terms').addEventListener('click', function () {
            popup.style.display = 'none';
        });
    });
</script>
