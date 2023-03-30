# project
*how to fetch data*
interface User {
  id: number;
  name: string;
  username: string;
  email: string;
}

function fetchUsers() {
  const xhr = new XMLHttpRequest();
  xhr.open('GET', 'https://jsonplaceholder.typicode.com/users');
  xhr.onload = () => {
    if (xhr.status === 200) {
      const users: User[] = JSON.parse(xhr.responseText);
      displayUsers(users);
    } else {
      console.error('Error fetching users:', xhr.statusText);
    }
  };
  xhr.onerror = () => {
    console.error('Error fetching users:', xhr.statusText);
  };
  xhr.send();
}

function displayUsers(users: User[]) {
  const table = document.getElementById('userTable');
  users.forEach(user => {
    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${user.id}</td>
      <td>${user.name}</td>
      <td>${user.username}</td>
      <td>${user.email}</td>
    `;
    table.appendChild(row);
  });
}

fetchUsers();
