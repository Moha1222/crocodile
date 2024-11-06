<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>88 Karta App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

<div id="language-selector">
    <button onclick="setLanguage('en')">English</button>
    <button onclick="setLanguage('ar')">Arabic</button>
</div>

<!-- Header with main message and points -->
<div id="header">
    <h1 id="main-message">Let's grow with us</h1>
    <div class="circle" onclick="toggleMenu()">88</div>
</div>

<!-- Main container -->
<div class="container">
    <!-- Coffee Cup Section -->
    <div class="coffee-cup" onclick="fillCup()">
        <div class="cup-content">
            <span class="karta-name">Karta</span>
        </div>
        <div id="coffee-level" class="coffee-content"></div>
    </div>

    <!-- Invite Friends Message -->
    <div id="invite-message" style="display:none;">
        <button onclick="showInviteMessage()">Invite Friends & Complete Tasks to be the Best!</button>
    </div>

    <!-- Friends Points Section -->
    <div id="friends-container">
        <button onclick="addFriend(1)">Add Friend (1 Friend) - 100 Points</button>
        <button onclick="addFriend(10)">Add 10 Friends - 1000 Points</button>
        <button onclick="addFriend(100)">Add 100 Friends - 10000 Points</button>
    </div>

    <!-- Instagram Follow Section -->
    <div id="instagram-container">
        <a href="https://www.instagram.com/88.karta.home" target="_blank"><button>Follow on Instagram - 10,000 Points</button></a>
        <a href="https://www.instagram.com/88.karta.coffe" target="_blank"><button>Follow on Instagram - 10,000 Points</button></a>
        <a href="https://www.instagram.com/88.karta" target="_blank"><button>Follow on Instagram - 10,000 Points</button></a>
        <a href="https://www.instagram.com/88.karta.combawt" target="_blank"><button>Follow on Instagram - 10,000 Points</button></a>
    </div>

    <!-- Leaderboard -->
    <div id="leaderboard">
        <h3>Leaderboard</h3>
        <ul id="leaderboard-list">
            <!-- Leaderboard data will be inserted here by JavaScript -->
        </ul>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
/* Basic styling */
body {
    font-family: Arial, sans-serif;
    background-color: #000;
    color: #fff;
    margin: 0;
    padding: 0;
}

#language-selector {
    position: fixed;
    top: 10px;
    right: 10px;
    z-index: 10;
}

#language-selector button {
    margin: 5px;
    padding: 10px;
    background-color: #333;
    color: white;
    border: none;
    cursor: pointer;
}

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 50px;
}

#header {
    text-align: center;
}

.circle {
    width: 80px;
    height: 80px;
    background-color: brown;
    border-radius: 50%;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    margin: 10px auto;
    cursor: pointer;
}

/* Coffee cup styling */
.coffee-cup {
    position: relative;
    width: 100px;
    height: 200px;
    border: 5px solid #333;
    border-radius: 50px;
    margin: 20px 0;
    cursor: pointer;
    background-color: transparent;
}

.coffee-content {
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: brown;
    transition: height 0.2s ease-in-out;
}

.karta-name {
    position: absolute;
    top: 5px;
    left: 10px;
    color: gold;
    font-weight: bold;
}

/* Button styling */
button {
    padding: 10px;
    margin: 5px;
    background-color: #333;
    color: white;
    border: none;
    cursor: pointer;
}

#instagram-container a, #friends-container button {
    display: inline-block;
    margin: 5px;
}// script.js

let coffeeLevel = 0;
let points = 0;
let leaderboard = [];
let friendsAdded = 0;
const maxFriendsPoints = [1, 10, 100];
const friendsPointsReward = [100, 1000, 10000];

// تحديد لغة الرسائل بناءً على لغة المتصفح
function setLanguage(lang) {
    document.getElementById("main-message").textContent = lang === 'ar' ? "لننمو معاً" : "Let's grow with us";
    document.getElementById("invite-message").textContent = lang === 'ar' ? "ادعُ أصدقاءك وقم بالمهام وكن الأفضل" : "Invite Friends & Complete Tasks to be the Best!";
}

// ملء الكوب على كل نقرة، وزيادة النقاط عند الامتلاء
function fillCup() {
    if (coffeeLevel < 100) {
        coffeeLevel += 20;
        document.getElementById("coffee-level").style.height = ${coffeeLevel}%;

        if (coffeeLevel === 100) {
            points += 1000;
            alert("The cup is filled, come back tomorrow for more!");
            updateLeaderboard();
            setTimeout(() => {
                coffeeLevel = 0;
                document.getElementById("coffee-level").style.height = "0%";
            }, 86400000); // يعيد ملء الكوب بعد 24 ساعة
        }
    }
}

// تحديث ترتيب النقاط في جدول المتصدرين
function updateLeaderboard() {
    leaderboard.push({ name: "User", points });
    leaderboard.sort((a, b) => b.points - a.points);
    const leaderboardList = document.getElementById("leaderboard-list");
    leaderboardList.innerHTML = '';
    leaderboard.forEach((user, index) => {
        const li = document.createElement('li');
        li.textContent = ${index + 1}. ${user.name} - ${user.points} points;
        leaderboardList.appendChild(li);
    });
}

// إضافة أصدقاء وزيادة النقاط بناءً على عدد الأصدقاء
function addFriend(numberOfFriends) {
    const index = maxFriendsPoints.indexOf(numberOfFriends);
    if (index !== -1) {
        points += friendsPointsReward[index];
        updateLeaderboard();
        friendsAdded += numberOfFriends;
        document.getElementById("friends-container").children[index].innerHTML = ✔️;
    }
}

// عرض رسالة دعوة الأصدقاء
function showInviteMessage() {
    document.getElementById("invite-message").style.display = 'block';
}

// المتابعة على إنستغرام والحصول على نقاط المكافأة
function followInstagram() {
    points += 10000;
    updateLeaderboard();
}

// التبديل إلى عجلة الحظ
function toggleWheel() {
    const wheel = document.getElementById("wheel");
    wheel.style.display = wheel.style.display === "none" ? "block" : "none";
}

// عجلة الحظ - حساب نقاط عشوائية
function spinWheel() {
    const rewards = [1000, 2000, 3000, 10000];
    const randomReward = rewards[Math.floor(Math.random() * rewards.length)];
    points += randomReward;
    alert(`Congratulations! You won ${randomReward} points!`);
    updateLeaderboard();
}
