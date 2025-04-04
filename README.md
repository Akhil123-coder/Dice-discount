<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice Discount</title>
    <style>
        /* General Styling */
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
            justify-content: center;
            height: 100vh;
        }

        h1 {
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }

        p {
            font-size: 1.2rem;
        }

        /* Dice Container */
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

        /* Button Styling */
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

        /* WhatsApp Contact */
        a {
            color: #fff;
            text-decoration: none;
            font-weight: bold;
        }

        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <h1>🎲 Roll the Dice for a Discount! 🎲</h1>
    <p>You can roll once per day.</p>

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

    <script>
        function getRandomDice() {
            return Math.floor(Math.random() * 6) + 1;
        }

        function checkRollEligibility() {
            const lastRollDate = localStorage.getItem("lastRollDate");
            const today = new Date().toISOString().split('T')[0];
            return lastRollDate !== today;
        }

        function rollDice() {
            if (!checkRollEligibility()) {
                document.getElementById("result").innerText = "You have already rolled today. Try again tomorrow!";
                return;
            }

            const dice1 = getRandomDice();
            const dice2 = getRandomDice();
            document.getElementById("dice1").innerText = getDiceEmoji(dice1);
            document.getElementById("dice2").innerText = getDiceEmoji(dice2);

            localStorage.setItem("lastRollDate", new Date().toISOString().split('T')[0]);

            const total = dice1 + dice2;
            document.getElementById("result").innerText = `You rolled a ${total}! Your discount is ${total * 5}%`;
        }

        function getDiceEmoji(number) {
            const diceFaces = ["⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];
            return diceFaces[number - 1];
        }

        document.getElementById("rollButton").addEventListener("click", rollDice);
    </script>

</body>
</html>
