#Repositorio sobre GIT/GITHUB DIO


<!DOCTYPE html>
<html>
<head>
  <title>Simple CRUD App</title>
</head>
<body>
  <h1>Simple CRUD App</h1>
  <form id="userForm">
    <label for="name">Name:</label>
    <input type="text" id="name" required><br><br>
    <label for="email">Email:</label>
    <input type="email" id="email" required><br><br>
    <button type="submit">Add User</button>
  </form>
  <hr>
  <h2>Users:</h2>
  <ul id="userList"></ul>

  <script>
    document.getElementById('userForm').addEventListener('submit', async function (e) {
      e.preventDefault();
      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const response = await fetch('/users', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ name, email }),
      });
      const newUser = await response.json();
      const userList = document.getElementById('userList');
      const listItem = document.createElement('li');
      listItem.textContent = `${newUser.name} - ${newUser.email}`;
      userList.appendChild(listItem);
      document.getElementById('userForm').reset();
    });

    async function fetchUsers() {
      const response = await fetch('/users');
      const users = await response.json();
      const userList = document.getElementById('userList');
      userList.innerHTML = '';
      users.forEach((user) => {
        const listItem = document.createElement('li');
        listItem.textContent = `${user.name} - ${user.email}`;
        userList.appendChild(listItem);
      });
    }

    fetchUsers();
  </script>
</body>
</html>
