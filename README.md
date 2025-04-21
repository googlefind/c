<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multiple Text Boxes with Copy Buttons</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .text-box-container {
            display: flex;
            margin-bottom: 15px;
            align-items: center;
        }
        .text-box {
            flex-grow: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        .copy-btn {
            margin-left: 10px;
            padding: 10px 15px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        .copy-btn:hover {
            background-color: #45a049;
        }
        .copy-btn.copied {
            background-color: #2196F3;
        }
    </style>
</head>
<body>
    <h1>Text Boxes with Copy Buttons</h1>
    
    <div id="text-boxes-container">
        <!-- Text boxes will be added here by JavaScript -->
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const container = document.getElementById('text-boxes-container');
            
            // Create 20 text boxes with copy buttons
            for (let i = 1; i <= 20; i++) {
                const boxId = `text-box-${i}`;
                const btnId = `copy-btn-${i}`;
                
                const boxDiv = document.createElement('div');
                boxDiv.className = 'text-box-container';
                boxDiv.innerHTML = `
                    <input type="text" id="${boxId}" class="text-box" placeholder="Enter text for box ${i}">
                    <button id="${btnId}" class="copy-btn">Copy ${i}</button>
                `;
                
                container.appendChild(boxDiv);
                
                // Add click event to copy button
                document.getElementById(btnId).addEventListener('click', function() {
                    const textToCopy = document.getElementById(boxId).value;
                    if (textToCopy) {
                        navigator.clipboard.writeText(textToCopy).then(() => {
                            // Visual feedback
                            this.textContent = 'Copied!';
                            this.classList.add('copied');
                            
                            // Reset button after 2 seconds
                            setTimeout(() => {
                                this.textContent = `Copy ${i}`;
                                this.classList.remove('copied');
                            }, 2000);
                        }).catch(err => {
                            console.error('Failed to copy: ', err);
                            alert('Failed to copy text. Please try again.');
                        });
                    } else {
                        alert('Text box is empty!');
                    }
                });
            }
        });
    </script>
</body>
</html>
