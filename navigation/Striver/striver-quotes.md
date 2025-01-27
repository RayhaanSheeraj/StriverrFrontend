---
layout: base
title: Striver Quotes
search_exclude: true
permalink: /Striver/striver-quotes
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
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
</div>


<h1 style="color:cyan;">Quotes API</h1>
<p>Find and share inspirational quotes!</p>

<div class="main">
    <div id="sidebar"></div>
    <div class="content">
        <div class="form-container">
            <form id="quoteForm">
                <div class="form-inputs">
                    <input type="text" id="category" name="category" placeholder="Enter Category (Optional)">
                    <button type="submit">Fetch Quote</button>
                </div>
            </form>
        </div>
        <div id="quote-container">
            <h3 id="quote" style="color: #333;"></h3>
            <p id="author" style="color: #555;"></p>
            <p id="error" style="color: red;"></p>
        </div>
    </div>
</div>

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

    /* Main Content */
    .main {
        margin-left: 200px;
        padding: 20px;
        font-family: Arial, sans-serif;
    }

    .form-container {
        margin: 20px 0;
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
    #category {
        flex: 1;
        padding: 12px;
        border-radius: 8px;
        border: 1px solid #ddd;
        font-size: 16px;
    }
    button[type="submit"] {
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

    #quote-container {
        margin-top: 20px;
        padding: 20px;
        background-color: #ffffff;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
</style>

<script>
    // Define the API endpoint
    const API_ENDPOINT = 'http://127.0.0.1:8887/api/quote';

    // Add event listener to the form
    document.getElementById('quoteForm').addEventListener('submit', async function(event) {
        event.preventDefault(); // Prevent form from refreshing the page

        // Clear previous results
        document.getElementById('quote').textContent = '';
        document.getElementById('author').textContent = '';
        document.getElementById('error').textContent = '';

        const category = document.getElementById('category').value;
        const url = category ? `${API_ENDPOINT}?category=${category}` : API_ENDPOINT;

        try {
            const response = await fetch(url);
            const data = await response.json();

            if (response.ok) {
                // Display the quote and author
                const quoteData = Array.isArray(data) ? data[0] : data;
                document.getElementById('quote').textContent = `"${quoteData.quote}"`;
                document.getElementById('author').textContent = `- ${quoteData.author || 'Unknown'}`;
            } else {
                // Handle API error
                document.getElementById('error').textContent = data.error || 'An error occurred';
            }
        } catch (error) {
            // Handle network or unexpected errors
            document.getElementById('error').textContent = 'An error occurred: ' + error.message;
        }
    });
</script>
