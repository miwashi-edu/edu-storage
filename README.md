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
<html>
<head>
  <script src="index.js" defer></script>
  <link rel="stylesheet" href="index.css" />
</head>
<body>
<p id="userDisplay">Not logged in</p>
<button id="logoutUser">Logout</button>

<h2>Register</h2>
<input type="text" id="username" placeholder="Enter username" />
<input type="password" id="password" placeholder="Enter password" />
<button id="registerUser">Register</button>

<h2>Login</h2>
<input type="text" id="loginUsername" placeholder="Enter username" />
<input type="password" id="loginPassword" placeholder="Enter password" />
<button id="loginUser">Login</button>
<p id="loginStatus"></p>

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
  const usersKey = "registeredUsers";
  const sessionUserKey = "loggedInUser";

  function displayUser() {
    let userDisplay = document.getElementById("userDisplay");
    const sessionUser = sessionStorage.getItem(sessionUserKey);
    userDisplay.textContent = sessionUser ? `Logged in as: ${sessionUser}` : "Not logged in";
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

  function loginUser() {
    const username = document.getElementById("loginUsername").value.trim();
    const password = document.getElementById("loginPassword").value.trim();
    const loginStatus = document.getElementById("loginStatus");

    const users = JSON.parse(localStorage.getItem(usersKey)) || [];
    const user = users.find(u => u.username === username && u.password === password);

    if (user) {
      sessionStorage.setItem(sessionUserKey, username);
      loginStatus.textContent = "Login successful!";
      displayUser();
    } else {
      loginStatus.textContent = "Invalid username or password.";
    }
  }

  function logoutUser() {
    sessionStorage.removeItem(sessionUserKey);
    displayUser();
  }

  document.getElementById("registerUser").addEventListener("click", registerUser);
  document.getElementById("loginUser").addEventListener("click", loginUser);
  document.getElementById("logoutUser").addEventListener("click", logoutUser);

  displayUser();
  displayUsers();
});
EOF
```

## index.css

```bash
cat > index.css << 'EOF'
body {
  font-family: Arial, sans-serif;
  margin: 20px;
  padding: 20px;
  background-color: #f4f4f4;
}

h2 {
  color: #333;
}

p {
  font-size: 16px;
  font-weight: bold;
}

input {
  display: block;
  margin: 10px 0;
  padding: 8px;
  width: 100%;
  max-width: 300px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  background-color: #28a745;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #218838;
}

#userDisplay {
  padding: 10px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

#loginStatus {
  color: red;
  font-weight: bold;
  margin-top: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

ul li {
  background-color: white;
  padding: 8px;
  margin: 5px 0;
  border-radius: 4px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
}

EOF
```
