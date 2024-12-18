!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name=<"viewport" content="width=device-width, initial-scale=1.0">
  <title>Energy Management System</title>
<link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="app">
    <header>
      <h1>Energy Management System</h1>
    </header>
    <main>
      <div id="appliance-section">
        <h2>Appliances</h2>
        <ul id="appliance-list"></ul>
        <button id="add-appliance">Add Appliance</button>
      </div>
      <div id="stats-section">
        <h2>Energy Usage</h2>
        <p>Total Power Consumption: <span id="total-power">0</span> kW</p>
      </div>
    </main>
    <footer>
      <p>Developed by Moutaz Wael</p>
    </footer>
  </div>
  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f4f4f9;
}

header {
  background-color: #007acc;
  color: white;
  text-align: center;
  padding: 1em 0;
}
// Appliance List
const appliances = [
  { id: 1, name: "Refrigerator", power: 0.8, status: "on" },
  { id: 2, name: "Washing Machine", power: 2, status: "off" },
];

// DOM Elements
const applianceList = document.getElementById("appliance-list");
const totalPowerElement = document.getElementById("total-power");
const addApplianceButton = document.getElementById("add-appliance");

// Functions
function calculateTotalPower() {
  const totalPower = appliances
    .filter(appliance => appliance.status === "on")
    .reduce((sum, appliance) => sum + appliance.power, 0);
  totalPowerElement.textContent = totalPower.toFixed(2);
}

function renderAppliances() {
  applianceList.innerHTML = "";
  appliances.forEach(appliance => {
    const li = document.createElement("li");
    li.textContent = ${appliance.name} - ${appliance.power} kW (${appliance.status});
    const toggleButton = document.createElement("button");
    toggleButton.textContent = appliance.status === "on" ? "Turn Off" : "Turn On";
    toggleButton.onclick = () => toggleAppliance(appliance.id);
    li.appendChild(toggleButton);
    applianceList.appendChild(li);
  });
  calculateTotalPower();
}

function toggleAppliance(id) {
  const appliance = appliances.find(appliance => appliance.id === id);
  appliance.status = appliance.status === "on" ? "off" : "on";
  renderAppliances();
}

function addAppliance() {
  const name = prompt("Enter appliance name:");
  const power = parseFloat(prompt("Enter power consumption in kW:"));
  if (name && !isNaN(power)) {
    appliances.push({
      id: appliances.length + 1,
      name,
      power,
      status: "off",
    });
    renderAppliances();
  } else {
    alert("Invalid input. Please try again.");
  }
}

// Event Listeners
addApplianceButton.addEventListener("click", addAppliance);

// Initialize
renderAppliances();
