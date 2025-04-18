<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Multi Calculator</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background: #f4f4f4;
    }

    .tabs {
      display: flex;
      flex-wrap: wrap;
      background-color: #333;
    }

    .tab {
      flex: 1;
      text-align: center;
      padding: 14px 10px;
      color: white;
      cursor: pointer;
      min-width: 100px;
    }

    .tab.active, .tab:hover {
      background-color: #555;
    }

    .content {
      display: none;
      padding: 20px;
      background-color: white;
    }

    .content.active {
      display: block;
    }

    .calculator {
      max-width: 400px;
      margin: 0 auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    input[type="number"],
    input[type="date"] {
      width: 100%;
      padding: 12px;
      margin-bottom: 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #007BFF;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      background-color: #0056b3;
    }

    .result {
      margin-top: 12px;
      text-align: center;
      font-weight: bold;
      color: #333;
    }

    @media screen and (max-width: 600px) {
      .tab {
        flex: 100%;
      }

      .calculator {
        padding: 15px;
        margin: 10px;
      }
    }
  </style>
</head>
<body>

  <!-- Tabs -->
  <div class="tabs">
    <div class="tab active" onclick="openTab('financial')">Financial</div>
    <div class="tab" onclick="openTab('age')">Time / Age</div>
    <div class="tab" onclick="openTab('health')">Health Tracker</div>
  </div>

  <!-- Financial Calculator -->
  <div id="financial" class="content active">
    <div class="calculator">
      <h2>Financial Calculator</h2>
      <input type="number" id="revenue" placeholder="Enter Revenue" />
      <input type="number" id="expense" placeholder="Enter Expense" />
      <button onclick="calculateProfit()">Calculate Profit</button>
      <div class="result" id="financialResult"></div>
    </div>
  </div>

  <!-- Age Calculator -->
  <div id="age" class="content">
    <div class="calculator">
      <h2>Age Calculator</h2>
      <input type="date" id="dob" />
      <button onclick="calculateAge()">Calculate Age</button>
      <div class="result" id="ageResult"></div>
    </div>
  </div>

  <!-- Health Tracker -->
  <div id="health" class="content">
    <div class="calculator">
      <h2>BMI Calculator</h2>
      <input type="number" id="weight" placeholder="Weight (kg)" />
      <input type="number" id="height" placeholder="Height (cm)" />
      <button onclick="calculateBMI()">Calculate BMI</button>
      <div class="result" id="bmiResult"></div>
    </div>
  </div>

  <script>
    function openTab(tabId) {
      const tabs = document.querySelectorAll('.tab');
      const contents = document.querySelectorAll('.content');

      tabs.forEach(tab => tab.classList.remove('active'));
      contents.forEach(c => c.classList.remove('active'));

      document.getElementById(tabId).classList.add('active');
      event.currentTarget.classList.add('active');
    }

    function calculateProfit() {
      const revenue = parseFloat(document.getElementById("revenue").value);
      const expense = parseFloat(document.getElementById("expense").value);
      const result = document.getElementById("financialResult");

      if (!isNaN(revenue) && !isNaN(expense)) {
        const profit = revenue - expense;
        result.textContent = "Profit: $" + profit.toFixed(2);
      } else {
        result.textContent = "Please enter valid numbers.";
      }
    }

    function calculateAge() {
      const dob = new Date(document.getElementById("dob").value);
      const result = document.getElementById("ageResult");

      if (dob instanceof Date && !isNaN(dob)) {
        const today = new Date();
        let age = today.getFullYear() - dob.getFullYear();
        const m = today.getMonth() - dob.getMonth();
        if (m < 0 || (m === 0 && today.getDate() < dob.getDate())) {
          age--;
        }
        result.textContent = "Your Age: " + age + " years";
      } else {
        result.textContent = "Please select a valid date.";
      }
    }

    function calculateBMI() {
      const weight = parseFloat(document.getElementById("weight").value);
      const height = parseFloat(document.getElementById("height").value) / 100;
      const result = document.getElementById("bmiResult");

      if (!isNaN(weight) && !isNaN(height) && height > 0) {
        const bmi = weight / (height * height);
        let status = "";
        if (bmi < 18.5) status = "Underweight";
        else if (bmi < 24.9) status = "Normal weight";
        else if (bmi < 29.9) status = "Overweight";
        else status = "Obese";
        result.textContent = `BMI: ${bmi.toFixed(2)} (${status})`;
      } else {
        result.textContent = "Enter valid weight and height.";
      }
    }
  </script>

</body>
</html>
