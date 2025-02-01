# edu-storage

# Instructions

```bash
cd ~
cd ws
mkdir storage
cd storage
touch index.html
touch index.css
touch index.js
```

## index.html

```bash
cat > index.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
  <script src="index.js" defer></script>
  <link rel="stylesheet" href="index.css" />
</head>
<body>
  <p id="userDisplay">Checking user...</p>
  <button id="forgetUser">Forget User</button>
  
  <h2>Register</h2>
  <input type="text" id="username" placeholder="Enter username" />
  <input type="password" id="password" placeholder="Enter password" />
  <button id="registerUser">Register</button>
  
  <h2>Registered Users</h2>
  <ul id="userList"></ul>
</body>
</html>
EOF
```


## index.js

```bash
cat > index.js << 'EOF'
document.addEventListener("DOMContentLoaded", () => {
  const userKey = "randomUser";
  const usersKey = "registeredUsers";

  const adjectives = [
    "Quick", "Lazy", "Happy", "Sad", "Bright", "Dark", "Mighty", "Brave"
  ];

  const nouns = [
    "Lion", "Tiger", "Bear", "Eagle", "Shark", "Wolf", "Panther", "Dragon"
  ];

  function getRandomElement(array) {
    return array[Math.floor(Math.random() * array.length)];
  }

  function generateRandomUser() {
    return `${getRandomElement(adjectives)}${getRandomElement(nouns)}${Math.floor(Math.random() * 1000)}`;
  }

  function checkAndSetUser() {
    let user = localStorage.getItem(userKey);
    if (!user) {
      user = generateRandomUser();
      localStorage.setItem(userKey, user);
    }
    displayUser(user);
  }

  function displayUser(user) {
    let userDisplay = document.getElementById("userDisplay");
    userDisplay.textContent = `User: ${user}`;
  }

  function forgetUser() {
    localStorage.removeItem(userKey);
    document.getElementById("userDisplay").textContent = "User forgotten.";
  }

  function registerUser() {
    const username = document.getElementById("username").value.trim();
    const password = document.getElementById("password").value.trim();

    if (username && password) {
      const users = JSON.parse(localStorage.getItem(usersKey)) || [];
      users.push({ username, password });
      localStorage.setItem(usersKey, JSON.stringify(users));
      displayUsers();
    }
  }

  function displayUsers() {
    const userList = document.getElementById("userList");
    userList.innerHTML = "";
    const users = JSON.parse(localStorage.getItem(usersKey)) || [];
    users.forEach(user => {
      const li = document.createElement("li");
      li.textContent = `Username: ${user.username}`;
      userList.appendChild(li);
    });
  }

  document.getElementById("forgetUser").addEventListener("click", forgetUser);
  document.getElementById("registerUser").addEventListener("click", registerUser);

  checkAndSetUser();
  displayUsers();
});
EOF
```

## index.css

```bash
cat > index.css << 'EOF'

EOF
```
