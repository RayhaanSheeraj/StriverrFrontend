---
layout: base
title: Striver Profile
search_exclude: true
permalink: 
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaid
---

<div class="sidebar">
    <a href="/StriverrFrontend/Striver/striver-achievements" class="sidebar-btn">⭐️ Achievements</a>
    <a href="/StriverrFrontend/Striver/striver-challenges" class="sidebar-btn">📉 Challenges</a>
    <a href="/StriverrFrontend/Striver/striver-ai" class="sidebar-btn">🤖 AI</a>
    <a href="/StriverrFrontend/Striver/striver-about" class="sidebar-btn">❓ About</a>
    <a href="/StriverrFrontend/Striver/striverr-terms" class="sidebar-btn">📄 Terms</a>
    <a href="/StriverrFrontend/Striver/striver-profile" class="sidebar-btn bottom-btn">👤 Profile</a>
    <a href="/StriverrFrontend/Striver/striver-steps" class="sidebar-btn bottom-btn">Step Tracker</a>
    <a href="/StriverrFrontend/Striver/striver-bucket-list" class="sidebar-btn bottom-btn">Bucket List</a>
    <a href="/StriverrFrontend/Striver/striver-quotes" class="sidebar-btn bottom-btn">Quotes</a>
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

<div>
  <div class="card">
    <div class="profile-box">
      <div class="profile-picture">
        <div class="image-container" id="profileImageBox">
        </div>
        <label for="profilePicture" class="file-icon">
          Upload Profile Picture <i class="fas fa-upload"></i>
        </label>
        <input type="file" id="profilePicture" accept="image/*" onchange="saveProfilePicture()">
      </div>
      <div class="profile-fields">
        <form>
          <div>
            <label for="newUid">Enter New Username:</label>
            <input type="text" id="newUid" placeholder="Username">
          </div>
          <div>
            <label for="newAboutMe">Change Your About Me:</label>
            <input type="text" id="newAboutMe" placeholder="About me">
          </div>
          <p id="profile-message" style="color: red;"></p>
        </form>
      </div>
    </div>
    <div class="preview-box">
      <h2>Preview</h2>
      <div class="preview-content">
        <div id="previewImageBox">
        </div>
        <div class="preview-text">
          <p><strong>Username:</strong> <span id="previewUsername">Not set</span></p>
          <p><strong>About Me:</strong> <span id="previewAboutMe">Not set</span></p>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
 
  .profile-container {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 100vh;
    padding-top: 30px; 
    background-color: #1A252F; 
  }

  
  .card {
    display: flex;
    flex-direction: column;
    background-color: #1A252F; 
    padding: 40px;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
    color: white;
    max-width: 900px;
    width: 95%;
  }

 
  .profile-box {
    display: flex;
    align-items: center;
    margin-bottom: 40px;
    background-color: #1A252F;
  }

 
  .profile-picture {
    flex: 1;
    text-align: center;
    background-color: #1A252F;
  }

  .profile-picture img {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    object-fit: cover;
    margin-bottom: 15px;
    border: 3px solid white;
  }

  .file-icon {
    display: inline-block;
    color: white;
    background-color: #1A252F;
    padding: 12px 20px;
    border: 2px solid white;
    border-radius: 12px;
    cursor: pointer;
    font-size: 16px;
    margin-top: 15px;
  }

  #profilePicture {
    display: none;
  }

  .profile-fields {
    flex: 2;
    padding-left: 30px;
    background-color: #1A252F;
  }

  .profile-fields label {
    display: block;
    font-size: 18px;
    margin-bottom: 10px;
    background-color: #1A252F;
  }

  .profile-fields input {
    width: 100%;
    padding: 15px;
    font-size: 18px;
    border-radius: 12px;
    border: 2px solid #28cee8;
    background-color: #1A252F;
    color: #28cee8;
    margin-bottom: 20px;
  }

  .profile-fields input::placeholder {
    color: #1A252F;
  }

  .profile-fields input:focus {
    outline: none;
    border-color: white;
  }

  .preview-box {
    margin-top: 20px;
    background-color: #1A252F;
    padding: 20px;
    border-radius: 12px;
    text-align: left;
  }

  .preview-box h2 {
    margin-bottom: 20px;
    text-align: center;
    color: #28cee8;
  }

  .preview-content {
    display: flex;
    align-items: center;
    background-color: #1A252F;
  }

  .preview-content img {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 20px;
    border: 3px #28cee8;
  }

  .preview-text {
    color: white;
    font-size: 18px;
    line-height: 1.6;
    background-color: #1A252F;
  }

  .preview-text p {
    margin: 5px 0;
  }
</style>

<script>
  function saveProfilePicture() {
    const fileInput = document.getElementById("profilePicture");
    const file = fileInput.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = function (e) {
      const previewImageBox = document.getElementById("previewImageBox");
      const img = document.createElement("img");
      img.src = e.target.result;
      img.alt = "Preview Profile Picture";
      previewImageBox.innerHTML = "";
      previewImageBox.appendChild(img);
    };
    reader.readAsDataURL(file);
  }

  document.getElementById("newUid").addEventListener("input", function () {
    const username = this.value || "Not set";
    document.getElementById("previewUsername").textContent = username;
  });

  document.getElementById("newAboutMe").addEventListener("input", function () {
    const aboutMe = this.value || "Not set";
    document.getElementById("previewAboutMe").textContent = aboutMe;
  });
</script> 