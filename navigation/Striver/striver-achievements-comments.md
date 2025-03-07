---
layout: base
title: Striver Home Page
search_exclude: true
permalink: /Striver/striver-achievements-comments
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<div class="sidebar">
    <a href="/StriverrFrontend/Striver/striver-achievement" class="sidebar-btn">Back to Achievements</a>
</div>
<div id="main-content">
    <div id="chatPanel">
        <h3>Comments</h3>
        <div id="outputDiv"></div>
        <form>
            <button class="plus-button" onclick="triggerFileUpload()">+</button>
            <input type="file" id="file-input" onchange="handleFileUpload(event)">
            <input placeholder="Enter message to send:" type="text" id="messageBox" name="message">
        </form>
    </div>

<style>
    .sidebar {
    position: fixed;
    left: 0;
    top: 0;
    width: 150px;
    height: 100%;
    background-color: #121212; /* Match the sidebar background */
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
    flex-direction: column;
    gap: 20px; /* Space between buttons */
    padding-top: 20px;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5); /* Add subtle shadow */
}
.sidebar-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 90%; /* Makes the button width slightly less than the sidebar */
    padding: 15px;
    margin: 0 auto; /* Center the button horizontally */
    background-color: #1c1c1c; /* Match the sidebar color */
    border: 2px solid #ddd; /* Light gray border */
    border-radius: 10px; /* Rounded corners */
    color: white; /* Text color */
    font-family: Arial, sans-serif;
    font-size: 16px; /* Button font size */
    text-decoration: none; /* Remove underline */
    transition: background-color 0.3s ease, transform 0.2s ease, color 0.3s ease;
    cursor: pointer;
    text-align: center;
}
.sidebar-btn:hover {
    background-color: #333333; /* Darker background on hover */
    color: #ffffff; /* Ensure text is clear on hover */
    transform: scale(1.05); /* Slight zoom on hover */
}
</style>

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
        border: 1px solid #28cee8;
        outline: none;
        background-color: #121212;
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
        background-color: #2C3E50;
        padding: 10px;
        border-radius: 10px;
        border: 1px solid #28cee8;
        margin: 5px 0;
        max-width: 80%;
        word-wrap: break-word;
    }
    .ai-bubble {
        background-color: #2C3E50;
        padding: 10px;
        border-radius: 10px;
        border: 1px solid #28cee8;
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
        border: 1px solid #28cee8;
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
</style>

<script>
    let commentCounter = 0; 
    // Simulate adding a comment
    function addComment(content) {
        commentCounter++;
        const commentId = `comment-${commentCounter}`;
        const commentDiv = document.createElement("div");
        commentDiv.id = commentId;
        commentDiv.className = "message-bubble";
        commentDiv.innerHTML = `
            <p>${content}</p>
            <a href="#${commentId}" onclick="scrollToComment('${commentId}')">Link to this comment</a>
        `;
        document.getElementById("outputDiv").appendChild(commentDiv);

        // Dynamically generate a link for each comment
        generateCommentLink(commentId);
    }

    // Function to generate links for each comment
    function generateCommentLink(commentId) {
        const linkDiv = document.createElement("div");
        linkDiv.className = "comment-link";
        linkDiv.innerHTML = `
            <a href="#${commentId}" onclick="scrollToComment('${commentId}')">Go to Comment ${commentId}</a>
        `;
        document.getElementById("outputDiv").appendChild(linkDiv);
    }

    // Scroll to the linked comment when the link is clicked
    function scrollToComment(commentId) {
        const commentElement = document.getElementById(commentId);
        if (commentElement) {
            commentElement.scrollIntoView({ behavior: "smooth" });
        }
    }

    // Example: Adding comments dynamically
    document.addEventListener("DOMContentLoaded", () => {
        addComment("This is the first comment.");
        addComment("This is the second comment.");
        addComment("Another comment to test links.");
    });
</script>