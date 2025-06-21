# testlabor
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>AI ChatBot Web - RakhaCyber</title>
    <style>
        body { background: #000; color: #0ff; font-family: Arial, sans-serif; padding: 20px; }
        #chatbox { border: 1px solid #0ff; padding: 10px; height: 400px; overflow-y: scroll; margin-bottom: 10px; }
        input { width: 70%; padding: 10px; margin-top: 10px; border: 1px solid #0ff; background: #111; color: #0ff; }
        button { padding: 10px; background: #0ff; color: #000; border: none; cursor: pointer; margin-left: 10px; }
    </style>
</head>
<body>
    <h1>AI ChatBot Web - RakhaCyber</h1>
    <div id="chatbox"></div>
    <input type="text" id="userInput" placeholder="Ketik pesan..." />
    <button onclick="sendMessage()">Kirim</button>

    <script>
        const apiKey = "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" ; // <-- GANTI dengan API KEY kamu

        async function sendMessage() {
            const input = document.getElementById("userInput");
            const message = input.value.trim();
            if (!message) return;
            input.value = "";

            const chatbox = document.getElementById("chatbox");
            chatbox.innerHTML += `<p><b>Kamu:</b> ${message}</p>`;

            const response = await fetch("https://api.openai.com/v1/chat/completions", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "Authorization": `Bearer ${apiKey}`
                },
                body: JSON.stringify({
                    model: "gpt-3.5-turbo",
                    messages: [{ role: "user", content: message }]
                })
            });

            const data = await response.json();
            const botReply = data.choices[0].message.content.trim();

            chatbox.innerHTML += `<p><b>Bot:</b> ${botReply}</p>`;
            chatbox.scrollTop = chatbox.scrollHeight;
        }
    </script>
</body>
</html>
