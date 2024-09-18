# tgweb.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telegram Mini App</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
    </style>
</head>
<body>
    <h1>Welcome to Telegram Mini App</h1>
    <div id="user-info">
        <!-- Информация о пользователе будет здесь -->
    </div>

    <script>
        window.onload = function () {
            const tg = window.Telegram.WebApp;
            const user = tg.initDataUnsafe.user;

            const userInfo = document.getElementById('user-info');
            if (user) {
                userInfo.innerHTML = `<p>Username: ${user.username || 'N/A'}</p>
                                      <p>User ID: ${user.id}</p>`;
            } else {
                userInfo.innerHTML = '<p>Cannot get user data</p>';
            }

            tg.onEvent('mainButtonClicked', function() {
                tg.sendData(JSON.stringify({
                    username: user.username,
                    user_id: user.id
                }));
            });
            
            tg.MainButton.text = "Send Data";
            tg.MainButton.show();
        };
    </script>
</body>
</html>
