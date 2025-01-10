---
layout: page 
title: Login
permalink: /login
search_exclude: true
show_reading_time: false 
---

<br>

<style>
.login-container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap; /* allows the cards to wrap onto the next line if the screen is too small */
}

.login-card {
    margin-top: 0; /* remove the top margin */
    width: 45%;
    border: 4px solid #07027d;
    border-radius: 50px;
    padding: 40px;
    box-shadow: 10px 10px 25px rgba(23, 7, 201, 1);
    margin-bottom: 20px;
    overflow-x: auto; /* Enable horizontal scrolling */
}

.login-card h1 {
    margin-bottom: 20px;
}

.signup-card {
    margin-top: 0; /* remove the top margin */
    width: 45%;
    border: 4px solid #07027d;
    border-radius: 50px;
    padding: 40px;
    box-shadow: 10px 10px 25px rgba(23, 7, 201, 1);
    margin-bottom: 20px;
    overflow-x: auto; /* Enable horizontal scrolling */
}

.signup-card h1 {
    margin-bottom: 20px;
}
</style>

<div class="login-container">
    <!-- Python Login Form -->
    <div class="login-card">
        <h1 id="pythonTitle">User Login (Python/Flask)</h1>
        <form id="pythonForm" onsubmit="pythonLogin(); return false;">
            <p>
                <label>
                    GitHub ID:
                    <input type="text" name="uid" id="uid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="password" id="password" required>
                </label>
            </p>
            <p>
                <button type="submit">Login</button>
            </p>
            <p id="message" style="color: red;"></p>
        </form>
    </div>
    <div class="signup-card">
        <h1 id="signupTitle">Sign Up</h1>
        <form id="signupForm" onsubmit="signup(); return false;">
            <p>
                <label>
                    Name:
                    <input type="text" name="name" id="name" required>
                </label>
            </p>
            <p>
                <label>
                    GitHub ID:
                    <input type="text" name="signupUid" id="signupUid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="signupPassword" id="signupPassword" required>
                </label>
            </p>
            <p>
                <button type="submit">Sign Up</button>
            </p>
            <p id="signupMessage" style="color: green;"></p>
        </form>
    </div>
</div>

<script type="module">
    import { login, pythonURI, fetchOptions } from '{{site.baseurl}}/assets/js/api/config.js';

    // Function to handle Python login
    window.pythonLogin = function() {
        const options = {
            URL: `${pythonURI}/api/authenticate`,
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                uid: document.getElementById("uid").value,
                password: document.getElementById("password").value,
            })
        };
        console.log("Login options:", options);
        fetch(options.URL, {
            method: options.method,
            headers: options.headers,
            body: options.body,
            credentials: 'include' // Include credentials for cross-origin requests
        })
        .then(response => {
            if (!response.ok) {
                throw new Error(`Login failed: ${response.status}`);
            }
            return response.json();
        })
        .then(data => {
            console.log("Login successful:", data);
            document.getElementById("message").textContent = "Login successful!";
            // Redirect or handle successful login
        })
        .catch(error => {
            console.error("Login Error:", error);
            document.getElementById("message").textContent = `Login Error: ${error.message}`;
        });
    }

    // Function to handle signup
    window.signup = function() {
        const signupButton = document.querySelector(".signup-card button");

        // Disable the button and change its color
        signupButton.disabled = true;
        signupButton.style.backgroundColor = '#d3d3d3'; // Light gray to indicate disabled state

        const signupOptions = {
            URL: `${pythonURI}/api/user`,
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                name: document.getElementById("name").value,
                uid: document.getElementById("signupUid").value,
                password: document.getElementById("signupPassword").value
            })
        };

        console.log("Signup options:", signupOptions);

        fetch(signupOptions.URL, {
            method: signupOptions.method,
            headers: signupOptions.headers,
            body: signupOptions.body,
            credentials: 'include' // Include credentials for cross-origin requests
        })
        .then(response => {
            if (!response.ok) {
                throw new Error(`Signup failed: ${response.status}`);
            }
            return response.json();
        })
        .then(data => {
            document.getElementById("signupMessage").textContent = "Signup successful!";
            // Optionally redirect to login page or handle as needed
            // window.location.href = '{{site.baseurl}}/profile';
        })
        .catch(error => {
            console.error("Signup Error:", error);
            document.getElementById("signupMessage").textContent = `Signup Error: ${error.message}`;
            // Re-enable the button if there is an error
            signupButton.disabled = false;
            signupButton.style.backgroundColor = ''; // Reset to default color
        });
    }

    // Function to fetch and display Python data
    function pythonDatabase() {
        const URL = `${pythonURI}/api/id`;

        fetch(URL, {
            method: 'GET',
            headers: {
                "Content-Type": "application/json"
            },
            credentials: 'include' // Include credentials for cross-origin requests
        })
        .then(response => {
            if (!response.ok) {
                throw new Error(`Flask server response: ${response.status}`);
            }
            return response.json();
        })
        .then(data => {
            window.location.href = '/StriverrFrontend/Striver/striver-profile';
        })
        .catch(error => {
            console.error("Python Database Error:", error);
            const errorMsg = `Python Database Error: ${error.message}`;
        });
    }

    // Call relevant database functions on the page load
    window.onload = function() {
         pythonDatabase();
    };
</script>