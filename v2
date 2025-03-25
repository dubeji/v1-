<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Posture Reminder</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        }
        
        :root {
            --primary-color: #5E81AC;
            --accent-color: #88C0D0;
            --dark-bg: rgba(0, 0, 0, 0.85);
            --light-text: #E5E9F0;
            --secondary-text: rgba(229, 233, 240, 0.7);
        }
        
        body {
            background: #2E3440;
            color: var(--light-text);
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            overflow: hidden;
            font-weight: 300;
            text-align: center;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100%;
            padding: 2rem;
        }
        
        h1 {
            font-size: 2.5rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--accent-color);
        }
        
        p {
            font-size: 1.2rem;
            font-weight: 300;
            color: var(--secondary-text);
            max-width: 500px;
            line-height: 1.5;
        }
        
        .timer-container {
            background-color: var(--dark-bg);
            padding: 1.5rem 2.5rem;
            border-radius: 12px;
            margin-bottom: 2rem;
        }
        
        .timer-display {
            font-size: 4rem;
            font-weight: 500;
            color: var(--light-text);
            letter-spacing: -0.05em;
        }
        
        .controls {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }
        
        button {
            background-color: var(--primary-color);
            border: none;
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            padding: 0.75rem 1.5rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        
        button:hover {
            background-color: var(--accent-color);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Posture Reminder</h1>
        <p>Maintain your posture and stay healthy with gentle reminders</p>
        
        <div class="timer-container">
            <div class="timer-display" id="timer">--:--</div>
        </div>
        
        <div class="controls">
            <button id="pauseBtn">Pause</button>
            <button id="testBtn">Test Notification</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const timerDisplay = document.getElementById('timer');
            const pauseBtn = document.getElementById('pauseBtn');
            const testBtn = document.getElementById('testBtn');
            
            // Sound for reminders
            const reminderSounds = [
                'data:audio/wav;base64,UklGRhQCAABXQVZFZm10IBAAAAABAAEARKwAAIhYAQACABAAAABkYXRhoAEAAP/+/wD9/f4A8vf7AOvy9ADg5+sA4ubs/+Tm7P/k5uz/5Obs/+Tn7f/k5+3/5efs/+Pm7ADv8fUA9Pj6APT4+gD0+PoA9Pj6AP37/QD+/v4A/f39AAEAAAD+/v4A/v7+AP39/QD9/f0A/f39AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gA=',
                'data:audio/wav;base64,UklGRswAAABXQVZFZm10IBAAAAABAAEARKwAAIhYAQACABAAAABkYXRhkAAAAA==',
                'data:audio/wav;base64,UklGRhQCAABXQVZFZm10IBAAAAABAAEARKwAAIhYAQACABAAAABkYXRhsgEAAP/+/wD9/f4A8vf7AOry9ADg5+sA4ubs/+Tm7P/k5uz/5Obs/+Tn7f/k5+3/5efs/+Pm7ADv8fUA9Pj6APT4+gD0+PoA9Pj6AP37/QD+/v4A/f39AAEAAAD+/v4A/v7+AP39/QD9/f0A/f39AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gD+/f4A/f3+AAEAAAD+/f4A/v3+AP39/gABAQEA/v7+AP79/gD9/f4AAQEBAP79/gA='
            ];
            
            let interval;
            let isActive = true;
            let nextReminderTime;
            
            function formatTime(seconds) {
                const mins = Math.floor(seconds / 60);
                const secs = seconds % 60;
                return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
            }
            
            function calculateNextReminderTime() {
                const now = new Date();
                const minutes = now.getMinutes();
                const seconds = now.getSeconds();
                
                const nextTime = new Date(now);
                
                if (minutes < 30) {
                    nextTime.setMinutes(30, 0, 0);
                } else {
                    nextTime.setHours(nextTime.getHours() + 1, 0, 0, 0);
                }
                
                return nextTime;
            }
            
            function updateDisplay() {
                if (!isActive) {
                    timerDisplay.textContent = "--:--";
                    return;
                }
                
                const now = new Date();
                const diffMs = nextReminderTime - now;
                const diffSec = Math.floor(diffMs / 1000);
                
                if (diffSec <= 0) {
                    showNotification();
                    nextReminderTime = calculateNextReminderTime();
                }
                
                timerDisplay.textContent = formatTime(diffSec > 0 ? diffSec : 0);
            }
            
            function startApp() {
                nextReminderTime = calculateNextReminderTime();
                updateDisplay();
                interval = setInterval(updateDisplay, 1000);
                
                pauseBtn.textContent = 'Pause';
                isActive = true;
            }
            
            function togglePause() {
                if (isActive) {
                    clearInterval(interval);
                    isActive = false;
                    pauseBtn.textContent = 'Resume';
                } else {
                    startApp();
                }
            }
            
            function showNotification() {
                // Play a random sound
                const randomSound = reminderSounds[Math.floor(Math.random() * reminderSounds.length)];
                try {
                    const audio = new Audio(randomSound);
                    audio.play().catch(e => console.log('Audio play prevented by browser'));
                } catch (e) {
                    console.log('Audio playback error:', e);
                }
                
                // Optional: Add visual notification or alert
                alert('Time to check your posture!');
            }
            
            pauseBtn.addEventListener('click', togglePause);
            testBtn.addEventListener('click', showNotification);
            
            startApp();
        });
    </script>
</body>
</html>
