# Password-Strength-Analyze-Custom-Wordlist-Generator-Project
# Password Strength & Awareness Web App

This project is a simple, user-friendly web application that helps users generate strong passwords, analyze password strength, and understand the importance of password security. It also includes a custom wordlist generator for educational purposes.


## 🚀 Features

- **Password Generator:**  
  Create strong, random passwords with customizable options (uppercase, lowercase, digits, special characters, and length).

- **Password Strength Analyzer:**  
  Instantly check the strength of any password and get suggestions for improvement.

- **Custom Wordlist Generator:**  
  Generate possible password variations based on personal information (for awareness and testing).

- **Password Security Awareness:**
    Educational content on why strong passwords matter and the risks of weak passwords.

- **Modern, Responsive Design:**
  Clean interface with a subtle watermark background.

## 🖥️ How to Use

1. **Clone or Download** this repository.
2. **Open** the `password prj.html` file in your web browser.
3. Use the tools provided:
    - Generate a password with your chosen options.
    - Analyze the strength of any password.
    - Generate a wordlist from personal info.
    - Read about password security best practices.


## 📂 Project Structure

```
password prj.html      # Main HTML file with all code (HTML, CSS, JS)
README.md              # Project documentation
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
      <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 500px;
            margin: 40px auto;
            background: #fff;
            padding: 2em;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        h2 {
            color: #333;
            margin-top: 0;
        }
        label {
            display: block;
            margin: 1em 0 0.5em;
        }
        input[type="text"], input[type="password"], input[type="number"] {
            width: 100%;
            padding: 0.5em;
            margin-bottom: 1em;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        .options {
            margin-bottom: 1em;
        }
        .options label {
            display: inline-block;
            margin-right: 1em;
        }
        button {
            background: #0078d4;
            color: #fff;
            border: none;
            padding: 0.7em 1.5em;
            border-radius: 4px;
            cursor: pointer;
            margin-right: 1em;
        }
        button:hover {
            background: #005fa3;
        }
        .result, .wordlist {
            background: #f9f9f9;
            border-radius: 4px;
            padding: 1em;
            margin-top: 1em;
            font-size: 1em;
        }
        .wordlist {
            max-height: 120px;
            overflow-y: auto;
        }
        .score-bar {
            height: 10px;
            border-radius: 5px;
            background: #ddd;
            margin: 0.5em 0;
            overflow: hidden;
        }
        .score-fill {
            height: 100%;
            border-radius: 5px;
            background: #4caf50;
            width: 0;
            transition: width 0.4s;
        }
        .warning {
            color: #d9534f;
        }
        .suggestion {
            color: #0078d4;
        }
    </style>
</head>
<body>
<div class="container">
    <h2>Password Generator</h2>
    <label>Password Length:</label>
    <input type="number" id="length" min="8" value="16">
    <div class="options">
        <label><input type="checkbox" id="uppercase" checked> Uppercase</label>
        <label><input type="checkbox" id="lowercase" checked> Lowercase</label>
        <label><input type="checkbox" id="digits" checked> Digits</label>
        <label><input type="checkbox" id="special" checked> Special Chars</label>
    </div>
    <button onclick="generatePassword()">Generate Password</button>
    <div class="result" id="passwordResult"></div>

    <h2>Password Strength Analyzer</h2>
    <label>Enter Password:</label>
    <input type="password" id="analyzeInput">
    <button onclick="analyzePassword()">Analyze Strength</button>
    <div class="result" id="analyzeResult"></div>

    <h2>Custom Wordlist Generator</h2>
    <label>Personal Info (name, birthday, etc.):</label>
    <input type="text" id="infoInput">
    <button onclick="generateWordlist()">Generate Wordlist</button>
    <div class="wordlist" id="wordlistResult"></div>

    <h2>Password Strength Awareness and Why It's Needed</h2>
    <p>
      Password strength awareness is crucial in the digital age to protect user accounts from cyber attacks.
      Weak passwords can be easily guessed or cracked, leading to data breaches and identity theft.
      By educating users about strong password practices—such as using a mix of characters, avoiding dictionary words, and enabling two-factor authentication—security risks can be greatly reduced.
    </p>
    <!-- Add this after your awareness paragraph or as a new section -->
<h3>Impacts of Using Weak Passwords</h3>
<ul>
  <li>Increased risk of unauthorized account access</li>
  <li>Potential for identity theft and financial loss</li>
  <li>Exposure of sensitive personal or business information</li>
  <li>Higher likelihood of data breaches and cyber attacks</li>
  <li>Loss of trust and reputation for individuals and organizations</li>
  <li>Difficulty recovering compromised accounts</li>
</ul>
</div>
<script>
function generatePassword() {
    const length = Math.max(8, parseInt(document.getElementById('length').value) || 16);
    const useUppercase = document.getElementById('uppercase').checked;
    const useLowercase = document.getElementById('lowercase').checked;
    const useDigits = document.getElementById('digits').checked;
    const useSpecial = document.getElementById('special').checked;

    let chars = '';
    if (useUppercase) chars += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    if (useLowercase) chars += 'abcdefghijklmnopqrstuvwxyz';
    if (useDigits) chars += '0123456789';
    if (useSpecial) chars += '!@#$%^&*()-_=+[]{}|;:,.<>?/`~';

    if (!chars) {
        document.getElementById('passwordResult').innerHTML = '<span class="warning">Select at least one character type.</span>';
        return;
    }

    let password = '';
    for (let i = 0; i < length; i++) {
        password += chars.charAt(Math.floor(Math.random() * chars.length));
    }

    document.getElementById('passwordResult').innerHTML = `<strong>${password}</strong>`;
}

function analyzePassword() {
    const password = document.getElementById('analyzeInput').value;
    if (!password) {
        document.getElementById('analyzeResult').innerHTML = '<span class="warning">Enter a password to analyze.</span>';
        return;
    }

    // Simple strength analysis (not as advanced as zxcvbn)
    let score = 0;
    let feedback = [];
    if (password.length >= 8) score++;
    if (/[A-Z]/.test(password)) score++;
    if (/[a-z]/.test(password)) score++;
    if (/\d/.test(password)) score++;
    if (/[^A-Za-z0-9]/.test(password)) score++;

    let warnings = '';
    if (password.length < 8) warnings += 'Password is too short. ';
    if (!/[A-Z]/.test(password)) feedback.push('Add uppercase letters.');
    if (!/[a-z]/.test(password)) feedback.push('Add lowercase letters.');
    if (!/\d/.test(password)) feedback.push('Add digits.');
    if (!/[^A-Za-z0-9]/.test(password)) feedback.push('Add special characters.');

    let scorePercent = Math.min(score, 4) * 25;
    let scoreText = ['Very Weak', 'Weak', 'Medium', 'Strong', 'Very Strong'][score];

    document.getElementById('analyzeResult').innerHTML = `
        <div>Password: <strong>${password}</strong></div>
        <div>Strength: <strong>${scoreText}</strong></div>
        <div class="score-bar"><div class="score-fill" style="width:${scorePercent}%"></div></div>
        ${warnings ? `<div class="warning">${warnings}</div>` : ''}
        ${feedback.length ? `<div class="suggestion">Suggestions: ${feedback.join(', ')}</div>` : ''}
    `;
}

function generateWordlist() {
    const info = document.getElementById('infoInput').value.trim();
    if (!info) {
        document.getElementById('wordlistResult').innerHTML = '<span class="warning">Enter some personal info.</span>';
        return;
    }
    // Tokenize by spaces and punctuation
    let tokens = info.split(/[\s,.;:!?]+/).filter(Boolean);
    let variations = new Set();

    tokens.forEach(word => {
        variations.add(word);
        variations.add(word.toLowerCase());
        variations.add(word.toUpperCase());
        variations.add(word.charAt(0).toUpperCase() + word.slice(1));
        variations.add(word.split('').reverse().join(''));
        for (let i = 0; i < 10; i++) {
            variations.add(word + i);
            variations.add(i + word);
        }
    });

    document.getElementById('wordlistResult').innerHTML =
        Array.from(variations).join(', ');
}
</script>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f4f4;
        margin: 0;
        padding: 0;
    }
    .container {
        max-width: 500px;
        margin: 40px auto;
        background: #fff;
        padding: 2em;
        border-radius: 8px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    h2 {
        color: #333;
        margin-top: 0;
    }
    label {
        display: block;
        margin: 1em 0 0.5em;
    }
    input[type="text"], input[type="password"], input[type="number"] {
        width: 100%;
        padding: 0.5em;
        margin-bottom: 1em;
        border-radius: 4px;
        border: 1px solid #ccc;
    }
    .options {
        margin-bottom: 1em;
    }
    .options label {
        display: inline-block;
        margin-right: 1em;
    }
    button {
        background: #0078d4;
        color: #fff;
        border: none;
        padding: 0.7em 1.5em;
        border-radius: 4px;
        cursor: pointer;
        margin-right: 1em;
    }
    button:hover {
        background: #005fa3;
    }
    .result, .wordlist {
        background: #f9f9f9;
        border-radius: 4px;
        padding: 1em;
        margin-top: 1em;
        font-size: 1em;
    }
    .wordlist {
        max-height: 120px;
        overflow-y: auto;
    }
    .score-bar {
        height: 10px;
        border-radius: 5px;
        background: #ddd;
        margin: 0.5em 0;
        overflow: hidden;
    }
    .score-fill {
        height: 100%;
        border-radius: 5px;
        background: #4caf50;
        width: 0;
        transition: width 0.4s;
    }
    .warning {
        color: #d9534f;
    }
    .suggestion {
        color: #0078d4;
    }
    /* Inserted watermark and content styles below */
    .watermark {
        position: absolute;
        top: 50%;
        left: 50%;
        font-size: 100px;
        color: rgba(0, 0, 0, 0.05);
        transform: translate(-50%, -50%);
        z-index: 0;
        pointer-events: none;
        white-space: nowrap;
    }
    .content {
        position: relative;
        z-index: 1;
        text-align: center;
        padding: 100px 20px;
    }
    h1 {
        font-size: 2.5em;
        color: #333;
        margin-bottom: 20px;
    }
    p {
        font-size: 1.2em;
        color: #555;
        max-width: 800px;
        margin: 0 auto;
    }
</style>
</body>
</html>

## 🛡️ Security Notes

- **No data is stored or sent anywhere.**  
  All password generation and analysis happens locally in your browser.
- This project is for educational and personal use only.  
  Do not use it to store or manage real passwords.

## ✅💻 Demo Output

<img width="1342" height="891" alt="image" src="https://github.com/user-attachments/assets/f0a1494c-700e-4bb5-8067-027c602e07af" />

<img width="808" height="907" alt="image" src="https://github.com/user-attachments/assets/cf11422b-57f7-4c43-84d4-1799ccad390d" />

<img width="753" height="868" alt="Screenshot 2025-07-29 001917" src="https://github.com/user-attachments/assets/8075c632-fd62-4abb-b8c3-06cdd2c2d09a" />

https://www.linkedin.com/posts/archana-b-b92183270_cybersecurity-python-passwordsecurity-activity-7353070697717358604-jUZ7?utm_source=share&utm_medium=member_android&rcm=ACoAAEI7rt4B4wsDW1H_WONWicHNrbvBmuls6Ng

```
file:///C:/Users/archa/.VirtualBox/python/password%20prj.html
```
## 📚 Educational Content

### Why Password Strength Matters

Weak passwords can be easily guessed or cracked, leading to data breaches and identity theft. By using strong passwords (mix of characters, avoiding dictionary words, enabling two-factor authentication), you greatly reduce your security risks.

### Impacts of Using Weak Passwords

- Increased risk of unauthorized account access
- Potential for identity theft and financial loss
- Exposure of sensitive personal or business information
- Higher likelihood of data breaches and cyber attacks
- Loss of trust and reputation for individuals and organizations
- Difficulty recovering compromised accounts

## ✨ Credits
Created by Archana.

## 📃 License

This project is open source and free to use for educational purposes.
