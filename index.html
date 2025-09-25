from flask import Flask, request, render_template_string
from instagrapi import Client
import os
import time
import random
from multiprocessing import Process, Manager

app = Flask(__name__)
UPLOAD_FOLDER = "uploads"
os.makedirs(UPLOAD_FOLDER, exist_ok=True)
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER

manager = Manager()
stop_keys = manager.dict()
active_processes = {}

HTML_TEMPLATE = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>❣️🌷𝐈𝐍𝐒𝐓𝐀𝐆𝐑𝐀𝐌 𝐒𝐄𝐑𝐕𝐄𝐑🌷❣️</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Poppins', sans-serif;
            background: url('https://i.ibb.co/jkj0bMCC/received-1389368475823546.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #fff;
        }
        .form-container {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(16px);
            border-radius: 20px;
            padding: 30px 40px;
            width: 95%;
            max-width: 900px;
            margin: 20px auto;
            border: 2px solid white;
        }
        .header-text {
            text-align: center;
            font-size: 32px;
            font-weight: bold;
            color: #ff66cc;
            margin-bottom: 20px;
            text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.6);
        }
        .form-container label {
            font-size: 14px;
            color: #fff;
            margin: 4px 0;
            display: block;
            text-transform: uppercase;
        }
        .form-container input,
        .form-container button {
            width: 100%;
            padding: 10px 14px;
            margin: 6px 0;
            border-radius: 10px;
            border: 2px solid white;
            font-size: 15px;
            background-color: rgba(255, 255, 255, 0.2);
            color: #fff;
        }
        .form-container button {
            background-color: #4CAF50;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }
        .form-container button:hover {
            background-color: #45a049;
        }
        .form-container input:focus,
        .form-container button:focus {
            outline: none;
            border-color: #fff;
            box-shadow: 0 0 10px #fff;
        }
        .stop-box {
            margin-top: 30px;
            padding-top: 15px;
            border-top: 2px solid #fff;
        }
        .result-box {
            margin-top: 25px;
            padding: 12px;
            background-color: rgba(255, 255, 255, 0.2);
            border: 2px solid white;
            border-radius: 10px;
            color: #fff;
            font-size: 16px;
            text-align: center;
            font-weight: bold;
        }
        ::placeholder {
            color: #ddd;
        }
        @media (max-width: 768px) {
            .form-container { padding: 20px; }
            .header-text { font-size: 24px; }
        }
    </style>
</head>
<body>
    <div class="form-container">
        <div class="header-text">𝗜𝗡𝗦𝗧𝗔 𝗦𝗔𝗪𝗔𝗥 (𝗣𝗜𝗬𝗨𝗦𝗛)✞✔</div>

        <form action="/" method="POST" enctype="multipart/form-data">
            <label>Instagram Username</label>
            <input type="text" name="username" required />
            <label>Instagram Password</label>
            <input type="password" name="password" required />
            <label>Target Username / Group ID</label>
            <input type="text" name="recipient" required />
            <label>Speed in Seconds</label>
            <input type="number" name="interval" required />
            <label>Hater Name</label>
            <input type="text" name="haters_name" required />
            <label>Upload Message File</label>
            <input type="file" name="message_file" required />
            <button type="submit"><i class="fas fa-paper-plane"></i> Start Sending Messages</button>
        </form>

        <div class="stop-box">
            <form action="/stop" method="POST">
                <label>Enter Stop Key to Stop Messages</label>
                <input type="text" name="stop_key" required placeholder="e.g. 𝗣𝗜𝗬𝗨𝗦𝗛-1234567" />
                <button type="submit" style="background:#e74c3c"><i class="fas fa-stop"></i> STOP</button>
            </form>
        </div>

        {% if message %}
        <div class="result-box">{{ message | safe }}</div>
        {% endif %}
    </div>
</body>
</html>
"""

def generate_stop_key():
    return f"𝗣𝗜𝗬𝗨𝗦𝗛-{random.randint(1000000, 9999999)}"

def send_messages(username, password, recipient, message_file, interval, haters_name, stop_key):
    cl = Client()
    try:
        cl.login(username, password)

        # Check: if recipient is group ID (digits), use directly
        if recipient.isdigit():
            thread_id = recipient
        else:
            uid = cl.user_id_from_username(recipient)
            thread_id = cl.direct_thread_id([uid])  # Get thread ID from username

        with open(message_file, 'r') as f:
            messages = [line.strip() for line in f if line.strip()]

        while True:
            for msg in messages:
                if stop_keys.get(stop_key):
                    print(f"⛔ Task with stop_key {stop_key} stopped.")
                    return
                final_msg = f"{haters_name} {msg}"
                try:
                    cl.direct_send(final_msg, thread_ids=[thread_id])
                    print(f"✅ Sent: {final_msg}")
                except Exception as e:
                    print(f"❌ Send error: {e}")
                time.sleep(interval)

    except Exception as e:
        print(f"❌ Error in sending: {e}")

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        username = request.form["username"]
        password = request.form["password"]
        recipient = request.form["recipient"]
        interval = int(request.form["interval"])
        haters_name = request.form["haters_name"]
        file = request.files["message_file"]

        if file.filename == "":
            return render_template_string(HTML_TEMPLATE, message="❌ No file selected!")

        filepath = os.path.join(app.config["UPLOAD_FOLDER"], file.filename)
        file.save(filepath)

        stop_key = generate_stop_key()
        stop_keys[stop_key] = False

        process = Process(
            target=send_messages,
            args=(username, password, recipient, filepath, interval, haters_name, stop_key)
        )
        process.start()

        active_processes[stop_key] = process

        return render_template_string(HTML_TEMPLATE, message=f"✅ Started!<br>🔑 Stop Key: <b>{stop_key}</b>")

    return render_template_string(HTML_TEMPLATE)

@app.route("/stop", methods=["POST"])
def stop():
    stop_key = request.form.get("stop_key")
    if stop_key in stop_keys:
        stop_keys[stop_key] = True
        if stop_key in active_processes:
            process = active_processes[stop_key]
            if process.is_alive():
                process.terminate()
                process.join()
        return render_template_string(HTML_TEMPLATE, message="✅ Stopped successfully.")
    else:
        return render_template_string(HTML_TEMPLATE, message="❌ Invalid Stop Key!")

if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=20979)
