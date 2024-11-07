<!DOCTYPE html>

<html>

<head>

  <title>網頁驗證碼</title>

  <style>

    #captchaCanvas {

      border: 1px solid black;

    }

  </style>

</head>


<body>


  <div align="center">

    <h1>canvas驗證碼+線條</h1>

    <canvas id="captchaCanvas" width="200" height="80"></canvas><br>

    <button id="regenerate">看不清楚，重新產生一張</button><br>

    <label id="hiddenCaptcha"></label><br>

    <input type="text" id="inputchaptcha">

  </div>



 <script>

        // 生成隨機字元

        function getRandomCharacter() {

            const characters = '23456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnpqrstuvwxyz';

            return characters[Math.floor(Math.random() * characters.length)];

        }


        // 生成隨機顏色

        function getRandomColor(usedColors) {

            const letters = '0123456789ABCDEF';

            let color;

            do {

                color = '#';

                for (let i = 0; i < 6; i++) {

                    color += letters[Math.floor(Math.random() * 16)];

                }

            } while (usedColors.includes(color)); // 檢查是否已經使用過

            usedColors.push(color);

            return color;

        }


        // 生成隨機線條

        function drawRandomLines(context, numLines, usedColors) {

            for (let i = 0; i < numLines; i++) {

                context.beginPath();

                context.moveTo(getRandomNumber(0, 200), getRandomNumber(0, 80));

                context.lineTo(getRandomNumber(0, 200), getRandomNumber(0, 80));

                context.strokeStyle = getRandomColor(usedColors); // 使用隨機顏色

                context.stroke();

            }

        }


        // 生成隨機數字

        function getRandomNumber(min, max) {

            return Math.floor(Math.random() * (max - min + 1)) + min;

        }


        // 生成驗證碼

        function generateCaptcha() {

            const canvas = document.getElementById('captchaCanvas');

            const context = canvas.getContext('2d');

            const usedColors = []; // 用於存儲已使用的顏色

           

            // 清空畫布

            context.clearRect(0, 0, canvas.width, canvas.height);


            // 生成隨機線條

            drawRandomLines(context, 50, usedColors);


            // 生成隨機字元

            const captchaText = Array.from({ length: 5 }, getRandomCharacter).join('');

            document.getElementById("hiddenCaptcha").textContent = captchaText;


            // 設定字體和大小

            context.font = '30px Arial';

            context.fillStyle = getRandomColor(usedColors); // 使用隨機顏色

            context.textAlign = 'center';

            context.textBaseline = 'middle';


            // 在畫布上繪製文字

            context.fillText(captchaText, canvas.width / 2, canvas.height / 2);

        }


        // 初始化驗證碼

        generateCaptcha();


        // 添加點擊事件，點擊時重新生成驗證碼

        document.getElementById('regenerate').addEventListener('click', function () {

            generateCaptcha();

        });

    </script>


</body>


</html>
