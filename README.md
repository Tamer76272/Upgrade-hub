# Upgrade-hub
Upgrade
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Азартный Апгрейд</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #121212;
            color: white;
            margin: 0;
            padding: 20px;
        }
        #spinner {
            width: 120px;
            height: 120px;
            border: 10px solid white;
            border-top: 10px solid gold;
            border-radius: 50%;
            margin: 20px auto;
            animation: spin 0.5s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .button {
            padding: 15px 30px;
            font-size: 20px;
            border: none;
            background-color: gold;
            color: black;
            cursor: pointer;
            border-radius: 10px;
            font-weight: bold;
            transition: 0.3s;
        }
        .button:hover {
            background-color: orange;
        }
        #result {
            font-size: 26px;
            font-weight: bold;
            margin-top: 20px;
        }
        .chance-box {
            font-size: 20px;
            margin-top: 10px;
            padding: 10px;
            border: 2px solid gold;
            display: inline-block;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>🎰 Апгрейд предмета 🎰</h1>
    <p class="chance-box">Шанс успеха: <span id="chance">1</span>%</p>
    <div id="spinner"></div>
    <button class="button" onclick="upgradeItem()">🔥 Улучшить 🔥</button>
    <p id="result"></p>

    <script>
        let successChance = 1;
        const increaseRate = 5; // Насколько увеличивается шанс после неудачи
        const maxChance = 95; // Максимальный шанс
        const guaranteedLossChance = 2; // 2% вероятность гарантированного слива

        function upgradeItem() {
            let roll = Math.random() * 100;
            let resultText = "";
            document.getElementById("spinner").style.animation = "spin 2s linear";

            setTimeout(() => {
                if (Math.random() * 100 < guaranteedLossChance) {
                    resultText = "💀 Гарантированный слив!";
                } else if (roll <= successChance) {
                    resultText = "✅ Успех! Предмет улучшен!";
                    successChance = 1; // После успеха шанс сбрасывается
                } else {
                    resultText = "❌ Неудача! Шанс увеличен.";
                    successChance += increaseRate;
                }

                if (successChance > maxChance) successChance = maxChance;
                document.getElementById("result").innerText = resultText;
                document.getElementById("chance").innerText = successChance;
                document.getElementById("spinner").style.animation = "none";
            }, 2000);
        }
    </script>

</body>
</html>
