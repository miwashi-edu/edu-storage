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
  <script src="https://cdn.jsdelivr.net/npm/nanoid@4.0.0/nanoid.min.js"></script>
  <script src="index.js" defer></script>
  <link rel="stylesheet" href="index.css" />
</head>
<body>
  <p id="userDisplay">Checking user...</p>
  <button id="forgetUser">Forget User</button>
  <button id="rememberUser">Remember User</button>
</body>
</html>
EOF
```


## index.js

```bash
cat > index.js << 'EOF'
document.addEventListener("DOMContentLoaded", () => {
  const userKey = "randomUser";

  const adjectives = [
    "Quick", "Lazy", "Happy", "Sad", "Bright", "Dark", "Mighty", "Brave"
  ];

  const nouns = [
    "Lion", "Tiger", "Bear", "Eagle", "Shark", "Wolf", "Panther", "Dragon"
  ];

  function getRandomElement(array) {
    const randomIndex = Math.floor(Math.random() * array.length);
    return array[randomIndex];
  }

  function generateRandomUser() {
    const adjective = getRandomElement(adjectives);
    const noun = getRandomElement(nouns);
    const number = Math.floor(Math.random() * 1000);
    return `${adjective}${noun}${number}`;
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

  document.getElementById("forgetUser").addEventListener("click", forgetUser);
  document.getElementById("rememberUser").addEventListener("click", checkAndSetUser);

  checkAndSetUser();
});
EOF
```

## index.css

```bash
cat > index.css << 'EOF'

EOF
```
