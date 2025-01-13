---
layout: base
title: Striver Bucket List
search_exclude: true
permalink: /Striver/striver-bucket-list
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bucket List App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            margin: 50px auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background: #f9f9f9;
            margin: 10px 0;
            padding: 10px 15px;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        button {
            background-color: #ff6b6b;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #ff5252;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>My Bucket List</h1>
        <ul id="bucket-list"></ul>
    </div>

    <script>
        // Define the API URL (replace with your actual backend API URL)
        const API_URL = "https://api.api-ninjas.com/v1/bucketlist
        
        "; // Adjust port or URL as needed

        // DOM elements
        const bucketListContainer = document.getElementById("bucket-list");

        // Function to fetch bucket list items from the API
        async function fetchBucketList() {
            try {
                const response = await fetch(API_URL);

                if (response.ok) {
                    const data = await response.json();
                    renderBucketList(data);
                } else {
                    console.error("Error fetching bucket list:", response.status, response.statusText);
                }
            } catch (error) {
                console.error("Network error:", error);
            }
        }

        // Function to render the bucket list on the page
        function renderBucketList(items) {
            // Clear the list
            bucketListContainer.innerHTML = "";

            // Loop through the items and create list elements
            items.forEach((item) => {
                const listItem = document.createElement("li");
                listItem.textContent = item.item;

                // Add a remove button (if needed)
                const removeButton = document.createElement("button");
                removeButton.textContent = "Remove";
                removeButton.onclick = () => removeBucketItem(item.id);

                listItem.appendChild(removeButton);
                bucketListContainer.appendChild(listItem);
            });
        }

        // Function to remove an item (future feature - needs backend support)
        async function removeBucketItem(id) {
            console.log(`Remove item with ID: ${id}`);
            
        }

        fetchBucketList();
    </script>
</body>
</html>