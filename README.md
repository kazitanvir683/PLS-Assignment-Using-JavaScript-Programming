# PLS-Assignment-Using-JavaScript-Programming


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple ATM System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        .container {
            max-width: 400px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 10px;
        }
        .container h2 {
            text-align: center;
        }
        .btn {
            padding: 10px;
            margin: 10px;
            width: 100%;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .btn:hover {
            background-color: #45a049;
        }
        .error {
            color: red;
        }
        .info {
            color: green;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Simple ATM System</h2>
        <div id="atm-container">
            <label for="pin">Enter your PIN:</label>
            <input type="password" id="pin" placeholder="Enter PIN" required>
            <button class="btn" onclick="login()">Login</button>
            <p id="login-error" class="error"></p>
        </div>
        <div id="atm-menu" style="display:none;">
            <p id="balance-display"></p>
            <button class="btn" onclick="checkBalance()">Check Balance</button>
            <button class="btn" onclick="depositMoney()">Deposit Money</button>
            <button class="btn" onclick="withdrawMoney()">Withdraw Money</button>
            <button class="btn" onclick="logout()">Logout</button>
        </div>
    </div>
    <script>
        let balance = 0; // Initial balance
        const pinCode = "1234"; // Hardcoded PIN for simplicity

        // Function to login and validate the PIN
        function login() {
            const enteredPin = document.getElementById("pin").value;
            const loginError = document.getElementById("login-error");
            if (enteredPin === pinCode) {
                // Hide login and show ATM menu
                document.getElementById("atm-container").style.display = "none";
                document.getElementById("atm-menu").style.display = "block";
                updateBalanceDisplay();
            } else {
                loginError.textContent = "Incorrect PIN. Please try again.";
            }
        }

        // Function to display the current balance
        function updateBalanceDisplay() {
            document.getElementById("balance-display").textContent = `Current Balance: $${balance.toFixed(2)}`;
        }

        // Function to check balance
        function checkBalance() {
            updateBalanceDisplay();
            alert(`Your current balance is $${balance.toFixed(2)}`);
        }

        // Function to deposit money
        function depositMoney() {
            const amount = parseFloat(prompt("Enter amount to deposit:"));
            if (amount > 0) {
                balance += amount;
                updateBalanceDisplay();
                alert(`You have successfully deposited $${amount.toFixed(2)}.`);
            } else {
                alert("Invalid deposit amount.");
            }
        }

        // Function to withdraw money
        function withdrawMoney() {
            const amount = parseFloat(prompt("Enter amount to withdraw:"));
            if (amount <= 0) {
                alert("Invalid withdrawal amount.");
            } else if (amount > balance) {
                alert("Insufficient balance.");
            } else {
                balance -= amount;
                updateBalanceDisplay();
                alert(`You have successfully withdrawn $${amount.toFixed(2)}.`);
            }
        }

        // Function to logout and reset the system
        function logout() {
            balance = 0; // Reset balance
            document.getElementById("atm-container").style.display = "block"; // Show login
            document.getElementById("atm-menu").style.display = "none"; // Hide ATM menu
            document.getElementById("pin").value = ""; // Clear PIN input
        }
    </script>
</body>
</html>
