<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice Discount</title>
    <style>
        body {
            text-align: center;
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            color: white;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            min-height: 100vh;
            padding-top: 30px;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }

        p {
            font-size: 1.2rem;
        }

        input {
            padding: 10px;
            font-size: 1rem;
            border-radius: 5px;
            border: none;
            margin-bottom: 15px;
            width: 250px;
            text-align: center;
        }

        .dice-container {
            margin: 20px;
            display: flex;
            justify-content: center;
            gap: 20px;
        }

        .dice {
            font-size: 80px;
            transition: transform 0.5s ease-in-out;
        }

        #rollButton {
            padding: 12px 20px;
            font-size: 1.2rem;
            font-weight: bold;
            background: #ff416c;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            box-shadow: 2px 4px 10px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
        }

        #rollButton:hover {
            background: #ff4b2b;
            transform: scale(1.05);
        }

        #result {
            font-size: 1.4rem;
            font-weight: bold;
            margin-top: 15px;
        }

        a {
            color: #fff;
            text-decoration: none;
            font-weight: bold;
        }

        a:hover {
            text-decoration: underline;
        }

        #reviewSection {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-top: 30px;
            margin-bottom: 30px;
        }

        .review-screenshot {
            width: 200px;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }

        @media (max-width: 500px) {
            .dice {
                font-size: 60px;
            }

            #rollButton {
                font-size: 1rem;
            }

            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>

    <h1>🎲 Roll the Dice for a Discount! 🎲</h1>
    <p>You can roll once per day.</p>

    <!-- Player Input -->
    <input type="text" id="playerNameInput" placeholder="Enter your name" />
    <input type="text" id="orderIdInput" placeholder="Enter your Order ID" />

    <!-- Dice Display -->
    <div class="dice-container">
        <span class="dice" id="dice1">⚀</span>
        <span class="dice" id="dice2">⚀</span>
    </div>

    <!-- Roll Button -->
    <button id="rollButton">🎲 Roll Dice</button>

    <!-- Result Message -->
    <p id="result"></p>

    <!-- WhatsApp Contact -->
    <p>Contact us on WhatsApp: <a href="https://wa.me/919756448178" target="_blank">+91 9756448178</a></p>

    <!-- Review Screenshots -->
    <h2>Happy Rollers</h2>
    <div id="reviewSection">
        <img src="review1.png" alt="Review Screenshot 1" class="review-screenshot">
        <img src="review2.png" alt="Review Screenshot 2" class="review-screenshot">
        <!-- Add more screenshots if needed -->
    </div>

    <script>
        const diceFaces = ["⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];

        function getRandomDice() {
            return Math.floor(Math.random() * 6) + 1;
        }

        function checkRollEligibility() {
            const lastRollDate = localStorage.getItem("lastRollDate");
            const today = new Date().toISOString().split('T')[0];
            return lastRollDate !== today;
        }

        function isValidOrderId(orderId) {
            return orderId.trim().length >= 5;
        }

        function rollDiceAnimation(finalDice1, finalDice2, playerName) {
            let rolls = 10;
            let interval = setInterval(() => {
                document.getElementById("dice1").innerText = diceFaces[Math.floor(Math.random() * 6)];
                document.getElementById("dice2").innerText = diceFaces[Math.floor(Math.random() * 6)];
                rolls--;
                if (rolls === 0) {
                    clearInterval(interval);
                    document.getElementById("dice1").innerText = diceFaces[finalDice1 - 1];
                    document.getElementById("dice2").innerText = diceFaces[finalDice2 - 1];

                    const total = finalDice1 + finalDice2;
                    document.getElementById("result").innerText =
                        `${playerName}, you rolled ${total}! 🎉 You get a ${total}% discount!`;
                    localStorage.setItem("lastRollDate", new Date().toISOString().split('T')[0]);
                }
            }, 100);
        }

        document.getElementById("rollButton").addEventListener("click", function () {
            const playerName = document.getElementById("playerNameInput").value.trim();
            const orderId = document.getElementById("orderIdInput").value.trim();

            if (playerName === "") {
                document.getElementById("result").innerText = "Please enter your name.";
                return;
            }

            if (!isValidOrderId(orderId)) {
                document.getElementById("result").innerText = "Please enter a valid Order ID.";
                return;
            }

            if (!checkRollEligibility()) {
                document.getElementById("result").innerText = "You have already rolled today. Try again tomorrow!";
                return;
            }

            const dice1 = getRandomDice();
            const dice2 = getRandomDice();

            rollDiceAnimation(dice1, dice2, playerName);
        });
    </script>

</body>
</html>