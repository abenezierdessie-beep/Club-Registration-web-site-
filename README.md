<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Student Club Registration</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      padding: 20px;
    }
    .container {
      max-width: 600px;
      margin: auto;
      background: white;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    label {
      font-weight: bold;
      display: block;
      margin-top: 15px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
    }
    .clubs label {
      font-weight: normal;
      display: block;
      margin-top: 5px;
    }
    button {
      margin-top: 20px;
      width: 100%;
      padding: 12px;
      background: #2c7be5;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: #1a5fd0;
    }
    #qr {
      margin-top: 25px;
      text-align: center;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>Student Club Registration</h1>

  <label>School ID Code</label>
  <input type="text" id="idCode" required>

  <label>Google Account (Email)</label>
  <input type="email" id="email" required>

  <label>Grade</label>
  <input type="text" id="grade" required>

  <label>Section</label>
  <input type="text" id="section" required>

  <label>Choose Club(s)</label>
  <div class="clubs">
    <label><input type="checkbox" value="STEM"> STEM</label>
    <label><input type="checkbox" value="Art & Creativity"> Art & Creativity</label>
    <label><input type="checkbox" value="Gardening & Environmental Sustainability"> Gardening & Environmental Sustainability</label>
    <label><input type="checkbox" value="Language, Literature & Communication"> Language, Literature & Communication</label>
    <label><input type="checkbox" value="Community Service"> Community Service</label>
    <label><input type="checkbox" value="Health & Hygiene"> Health & Hygiene</label>
    <label><input type="checkbox" value="Character Formation"> Character Formation</label>
    <label><input type="checkbox" value="Culture & Heritage"> Culture & Heritage</label>
    <label><input type="checkbox" value="Model of African Union"> Model of African Union</label>
  </div>

  <button onclick="generateQR()">Register & Generate Code</button>

  <div id="qr"></div>
</div>

<script>
  function generateQR() {
    const id = document.getElementById("idCode").value;
    const email = document.getElementById("email").value;
    const grade = document.getElementById("grade").value;
    const section = document.getElementById("section").value;

    const clubs = [];
    document.querySelectorAll('input[type="checkbox"]:checked')
      .forEach(cb => clubs.push(cb.value));

    if (!id || !email || !grade || !section || clubs.length === 0) {
      alert("Please fill all fields and select at least one club.");
      return;
    }

    const data = `
ID: ${id}
Email: ${email}
Grade: ${grade}
Section: ${section}
Clubs: ${clubs.join(", ")}
    `;

    const qrUrl = "https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=" 
                  + encodeURIComponent(data);

    document.getElementById("qr").innerHTML = `
      <h3>Registration Code</h3>
      <img src="${qrUrl}" alt="QR Code">
      <p>Scan to view student information</p>
    `;
  }
</script>

</body>
</html>
