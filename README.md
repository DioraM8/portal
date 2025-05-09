
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Diyora's Assignment Portal - Login Protected</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #0f0f1e;
      color: white;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
    }
    #login-section {
      margin-top: 50px;
      background-color: rgba(255, 255, 255, 0.05);
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
    }
    #login-form {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }
    input {
      padding: 10px;
      border-radius: 5px;
      border: none;
      font-size: 16px;
    }
    button {
      padding: 10px;
      background-color: #a770ff;
      border: none;
      border-radius: 5px;
      color: white;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover {
      background-color: #cf8fff;
    }
    #login-status {
      margin-top: 10px;
      color: #f77;
    }
    .container {
      display: none;
      margin-top: 50px;
      max-width: 800px;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.05);
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <div id="login-section">
    <h2>Login to Diyora's Assignment Portal</h2>
    <form id="login-form">
      <input type="email" id="email" placeholder="Email" required />
      <input type="password" id="password" placeholder="Password" required />
      <button type="submit">Login</button>
    </form>
    <div id="login-status"></div>
  </div>

  <div class="container">
    <h2>Welcome to the Assignment Dashboard!</h2>
    <p>Your assignments and grades will appear here after login.</p>
    <!-- You can expand this section as needed -->
  </div>

  <script>
    document.addEventListener("DOMContentLoaded", function () {
      document.getElementById("login-form").addEventListener("submit", async function (e) {
        e.preventDefault();
        const email = document.getElementById("email").value;
        const password = document.getElementById("password").value;

        const response = await fetch("https://script.google.com/macros/s/AKfycbwMa_ROBUQsgoMpNO3YoOLiuIRZAKWMT8B7RWgkGoHShpR00CIVje6kCtvfccZI5SUd/exec", {
          method: "POST",
          body: JSON.stringify({ email, password }),
        });

        const result = await response.json();

        if (result.success) {
          document.getElementById("login-section").innerHTML = `
            <h2>Welcome, ${result.name}!</h2>
            <p>Role: ${result.role}</p>
          `;
          document.querySelector(".container").style.display = "block";
        } else {
          document.getElementById("login-status").textContent = result.message;
        }
      });
    });
  </script>
</body>
</html>
