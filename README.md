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
    return "user-" + nanoid(10); // Generates a username prefixed with "user-" and 10 random characters
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

  document.getElementById("forgetUser").addEventListener("click", forgetUser);

  checkAndSetUser();
});
EOF
```

## index.css

```bash
cat > index.css << 'EOF'

EOF
```
