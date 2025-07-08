index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Digital Resume Builder</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>Resume Builder</h1>
    <form id="resumeForm">
      <input type="text" placeholder="Full Name" id="name" required>
      <input type="email" placeholder="Email" id="email" required>
      <input type="text" placeholder="Phone Number" id="phone" required>
      <input type="text" placeholder="Education (e.g., B.Tech - CSE)" id="education" required>
      <textarea placeholder="Experience (e.g., Internship at ABC Corp)" id="experience" required></textarea>
      <button type="submit">Generate Resume</button>
    </form>

    <div class="preview" id="preview">
      <h2 id="p_name"></h2>
      <p>Email: <span id="p_email"></span></p>
      <p>Phone: <span id="p_phone"></span></p>
      <p><strong>Education:</strong> <span id="p_education"></span></p>
      <p><strong>Experience:</strong></p>
      <p id="p_experience"></p>
      <button id="downloadBtn">Download as PDF</button>
    </div>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="script.js"></script>
</body>
</html>

style.css

body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 20px;
}
.container {
  max-width: 600px;
  margin: auto;
  background: white;
  padding: 20px;
  border-radius: 10px;
}
input, textarea {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
}
button {
  padding: 10px 15px;
  background-color: #0c6cf2;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.preview {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  background-color: #f9f9f9;
  display: none;
}

script.js

document.getElementById("resumeForm").addEventListener("submit", function(e) {
  e.preventDefault();

  // Get input values
  const name = document.getElementById("name").value;
  const email = document.getElementById("email").value;
  const phone = document.getElementById("phone").value;
  const education = document.getElementById("education").value;
  const experience = document.getElementById("experience").value;

  // Display preview
  document.getElementById("p_name").textContent = name;
  document.getElementById("p_email").textContent = email;
  document.getElementById("p_phone").textContent = phone;
  document.getElementById("p_education").textContent = education;
  document.getElementById("p_experience").textContent = experience;

  document.getElementById("preview").style.display = "block";
});

document.getElementById("downloadBtn").addEventListener("click", function() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.text("Resume", 20, 20);
  doc.text(`Name: ${document.getElementById("p_name").textContent}`, 20, 30);
  doc.text(`Email: ${document.getElementById("p_email").textContent}`, 20, 40);
  doc.text(`Phone: ${document.getElementById("p_phone").textContent}`, 20, 50);
  doc.text(`Education: ${document.getElementById("p_education").textContent}`, 20, 60);
  doc.text("Experience:", 20, 70);
  doc.text(document.getElementById("p_experience").textContent, 20, 80);

  doc.save("resume.pdf");
});
