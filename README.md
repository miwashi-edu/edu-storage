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
  <script src="https://cdn.jsdelivr.net/npm/random-username-generator@1.0.4/index.min.js"></script>
  <script src="index.js" defer></script>
  <link rel="stylesheet" href="index.css" />
</head>
<body>
  <p id="userDisplay">Checking user...</p>
  <button id="forgetUser">Forget User</button>
</body>
</html>>
EOF
```


## index.js

```bash
cat > index.js << 'EOF'
document.addEventListener("DOMContentLoaded", () => {
  const userKey = "randomUser";

  function generateRandomUser() {
    return RandomUsernameGenerator.generate();
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
    if (!userDisplay) {
      userDisplay = document.createElement("p");
      userDisplay.id = "userDisplay";
      document.body.appendChild(userDisplay);
    }
    userDisplay.textContent = `User: ${user}`;
  }

  function forgetUser() {
    localStorage.removeItem(userKey);
    let userDisplay = document.getElementById("userDisplay");
    if (userDisplay) {
      userDisplay.textContent = "User forgotten.";
    }
  }

  const forgetButton = document.createElement("button");
  forgetButton.textContent = "Forget User";
  forgetButton.addEventListener("click", forgetUser);
  document.body.appendChild(forgetButton);

  checkAndSetUser();
});
EOF
```

## index.css

```bash
cat > index.css << 'EOF'

EOF
```
