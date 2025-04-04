<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice Discount</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        .dice-container { margin: 20px; }
        .dice { font-size: 50px; }
        .hidden { display: none; }
    </style>
</head>
<body>
    <h1>Roll the Dice for a Discount!</h1>
    <p>You can roll once per day.</p>
    <div class="dice-container">
        <span class="dice" id="dice1">🎲</span>
        <span class="dice" id="dice2">🎲</span>
    </div>
    <button id="rollButton">Roll Dice</button>
    <p id="result"></p>
    <p>Contact us on WhatsApp: <a href="https://wa.me/919756448178" target="_blank">+91 9756448178</a></p><script>
    function getRandomDice() {
        return Math.floor(Math.random() * 6) + 1;
    }

    function checkRollEligibility() {
        const lastRollDate = localStorage.getItem("lastRollDate");
        const today = new Date().toISOString().split('T')[0];
        return lastRollDate !== today;
    }

    document.getElementById("rollButton").addEventListener("click", function() {
        if (!checkRollEligibility()) {
            document.getElementById("result").textContent = "You have already rolled today. Try again tomorrow!";
            return;
        }

        const dice1 = getRandomDice();
        const dice2 = getRandomDice();
        const total = dice1 + dice2;
        const discount = total; // 1 point = 1% discount

        document.getElementById("dice1").textContent = "🎲".repeat(dice1);
        document.getElementById("dice2").textContent = "🎲".repeat(dice2);
        document.getElementById("result").textContent = `You rolled ${total}. You get a ${discount}% discount!`;

        localStorage.setItem("lastRollDate", new Date().toISOString().split('T')[0]);
    });
</script>

</body>
</html>
