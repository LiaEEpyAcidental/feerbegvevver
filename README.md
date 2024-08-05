# feerbegvevver

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Username and Code Generator</title>
    <script>
        function generateCodes() {
            const username = document.getElementById('username').value;
            
            // Check if the username contains a string followed by an integer
            const match = username.match(/^([a-zA-Z]+)(\d+)$/);
            if (match) {
                const str = match[1];
                const int = match[2];
                window.location.href = `${str}${int}.html`;
                return;
            }
            
            // Generate two random 3-digit codes
            const threeDigitCode1 = Math.floor(100 + Math.random() * 900);
            const threeDigitCode2 = Math.floor(100 + Math.random() * 900);
            
            // Generate a 10-digit alphanumeric code based on the second 3-digit code
            const tenDigitCode = hashCode(threeDigitCode2);

            // Display the results
            document.getElementById('result').innerHTML = `Username with code: ${username}${threeDigitCode1}<br>3-digit code: ${threeDigitCode2}<br>10-digit code: ${tenDigitCode}`;
            
            // Call hiwii744 function to create the HTML file
            hiwii744(username, threeDigitCode1, threeDigitCode2);
        }

        function hashCode(code) {
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            let hash = '';
            while (hash.length < 10) {
                hash += characters[code % characters.length];
                code = Math.floor(code / characters.length);
            }
            return hash.padEnd(10, '0'); // Ensure the hash is always 10 characters long
        }

        function hiwii744(username, threeDigitCode1, threeDigitCode2) {
            const filename = `${username}${threeDigitCode1}.html`;
            const htmlContent = `
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>Username and Codes</title>
                </head>
                <body>
                    <h1>Generated Codes</h1>
                    <p>Username with code: ${username}${threeDigitCode1}</p>
                    <h2>Check Code and Hash Match</h2>
                    <form onsubmit="checkMatch(); return false;">
                        <label for="inputCode">Enter 3-digit code:</label>
                        <input type="text" id="inputCode" name="inputCode" required>
                        <br>
                        <label for="inputHash">Enter 10-digit hash:</label>
                        <input type="text" id="inputHash" name="inputHash" required>
                        <br>
                        <button type="submit">Check Match</button>
                    </form>
                </body>
                </html>
            `;
            
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = filename;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        function checkMatch() {
            const inputCode = document.getElementById('inputCode').value;
            const inputHash = document.getElementById('inputHash').value;
            const generatedHash = hashCode(parseInt(inputCode));

            if (inputHash === generatedHash) {
                alert('The 3-digit code and 10-digit hash match!');
            } else {
                alert('The 3-digit code and 10-digit hash do not match.');
            }
        }
    </script>
</head>
<body>
    <h1>Username and Code Generator</h1>
    <p>To use the "Username and Code Generator," enter your username in the field and click "Generate Codes." If your username is formatted with letters followed by numbers, you'll be redirected to a new page. Otherwise, the tool will display random 3-digit and 10-digit codes on the same page. Additionally, an HTML file containing these codes and a form for verifying the code and hash will be automatically downloaded. Open the downloaded file to check if the 3-digit code matches the 10-digit hash by entering them into the provided form.</p>
    

    <form onsubmit="generateCodes(); return false;">
        <label for="username">Enter Username:</label>
        <input type="text" id="username" name="username" required>
        <button type="submit">Generate Codes</button>
    </form>
    <div id="result" style="margin-top:20px;"></div>
</body>
</html>
