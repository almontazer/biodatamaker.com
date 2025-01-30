<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Biodata Maker</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label { display: block; margin: 10px 0 5px; }
    input { width: 100%; padding: 8px; margin: 5px 0 15px; }
    button { padding: 10px 15px; background-color: #4CAF50; color: white; border: none; cursor: pointer; }
    .result { margin-top: 20px; padding: 10px; background-color: #f4f4f4; border: 1px solid #ddd; }
  </style>
</head>
<body>

  <h1>Biodata Maker</h1>
  <form id="biodataForm">
    <label for="name">Full Name</label>
    <input type="text" id="name" name="name" placeholder="Enter your full name" required>
    
    <label for="dob">Date of Birth</label>
    <input type="date" id="dob" name="dob" required>
    
    <label for="email">Email</label>
    <input type="email" id="email" name="email" placeholder="Enter your email" required>
    
    <label for="address">Address</label>
    <input type="text" id="address" name="address" placeholder="Enter your address" required>
    
    <button type="submit">Generate Biodata</button>
  </form>

  <div id="result" class="result"></div>
  <button id="downloadBtn" style="display:none;">Download as PDF</button>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script>
    document.getElementById("biodataForm").addEventListener("submit", function(e) {
      e.preventDefault();
      
      // Get form data
      let name = document.getElementById("name").value;
      let dob = document.getElementById("dob").value;
      let email = document.getElementById("email").value;
      let address = document.getElementById("address").value;

      // Display biodata result
      let resultHTML = `
        <h2>Your Biodata</h2>
        <p><strong>Name:</strong> ${name}</p>
        <p><strong>Date of Birth:</strong> ${dob}</p>
        <p><strong>Email:</strong> ${email}</p>
        <p><strong>Address:</strong> ${address}</p>
      `;
      document.getElementById("result").innerHTML = resultHTML;

      // Show the download button
      document.getElementById("downloadBtn").style.display = "inline-block";

      // Generate PDF on download click
      document.getElementById("downloadBtn").onclick = function() {
        const { jsPDF } = window.jspdf;
        const doc = new jsPDF();
        doc.text("Biodata", 10, 10);
        doc.text(`Name: ${name}`, 10, 20);
        doc.text(`Date of Birth: ${dob}`, 10, 30);
        doc.text(`Email: ${email}`, 10, 40);
        doc.text(`Address: ${address}`, 10, 50);
        doc.save("biodata.pdf");
      };
    });
  </script>

</body>
</html>
