# omuga
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Webpage</title>
    <style>
        body {
            font-family: sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #007bff;
            border-bottom: 2px solid #007bff;
            padding-bottom: 5px;
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #1e7e34;
        }
        .hover-effect {
            padding: 15px;
            background-color: #eee;
            border: 1px solid #ccc;
            margin-top: 10px;
            border-radius: 5px;
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        .hover-effect:hover {
            background-color: #007bff;
            color: white;
        }
        #keypress-display {
            margin-top: 10px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        #interactive-button {
            margin-top: 15px;
        }
        #image-gallery {
            margin-top: 15px;
        }
        .gallery-image {
            width: 100px;
            height: auto;
            margin-right: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            cursor: pointer;
        }
        .gallery-image:hover {
            opacity: 0.8;
        }
        .tab-container {
            margin-top: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            overflow: hidden;
        }
        .tab-button {
            background-color: #f0f0f0;
            color: #333;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            float: left;
            transition: background-color 0.3s ease;
        }
        .tab-button:hover {
            background-color: #ddd;
        }
        .tab-content {
            padding: 15px;
            display: none;
            clear: both;
        }
        .tab-content.active {
            display: block;
        }
        form {
            margin-top: 20px;
            padding: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #f9f9f9;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        label {
            font-weight: bold;
        }
        input[type="text"],
        input[type="email"],
        input[type="password"] {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .error-message {
            color: red;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>1. Event Handling</h2>
        <button id="myButton">Click Me</button>
        <div class="hover-effect">Hover Over Me</div>
        <input type="text" id="keypressInput" placeholder="Type something here">
        <div id="keypress-display"></div>
        <button id="doubleClickButton">Double Click / Long Press Me</button>

        <h2>2. Interactive Elements</h2>
        <button id="interactive-button">Change Text</button>
        <div id="image-gallery">
            <img src="https://via.placeholder.com/100/FF0000/FFFFFF?Text=Image+1" alt="Image 1" class="gallery-image" onclick="changeMainImage(this.src)">
            <img src="https://via.placeholder.com/100/00FF00/FFFFFF?Text=Image+2" alt="Image 2" class="gallery-image" onclick="changeMainImage(this.src)">
            <img src="https://via.placeholder.com/100/0000FF/FFFFFF?Text=Image+3" alt="Image 3" class="gallery-image" onclick="changeMainImage(this.src)">
            <div id="main-image-container" style="margin-top: 10px;">
                <img id="main-image" src="https://via.placeholder.com/200" alt="Main Image" style="max-width: 100%;">
            </div>
        </div>

        <div class="tab-container">
            <button class="tab-button" onclick="openTab('tab1')">Tab 1</button>
            <button class="tab-button" onclick="openTab('tab2')">Tab 2</button>
            <div id="tab1" class="tab-content active">
                <p>Content for Tab 1.</p>
            </div>
            <div id="tab2" class="tab-content">
                <p>Content for Tab 2.</p>
            </div>
        </div>

        <h2>3. Form Validation</h2>
        <form id="myForm">
            <label for="name">Name:</label>
            <input type="text" id="name" required onblur="validateRequired(this)">
            <div class="error-message" id="nameError"></div>

            <label for="email">Email:</label>
            <input type="email" id="email" onblur="validateEmail(this)">
            <div class="error-message" id="emailError"></div>

            <label for="password">Password (min 8 characters):</label>
            <input type="password" id="password" onkeyup="validatePassword(this)" onblur="validatePassword(this)">
            <div class="error-message" id="passwordError"></div>

            <button type="submit">Submit</button>
        </form>
    </div>

    <script>
        // 1. Event Handling
        document.getElementById('myButton').addEventListener('click', function() {
            alert('Button Clicked!');
        });

        const hoverEffectDiv = document.querySelector('.hover-effect');
        hoverEffectDiv.addEventListener('mouseover', function() {
            this.textContent = 'You are hovering!';
        });
        hoverEffectDiv.addEventListener('mouseout', function() {
            this.textContent = 'Hover Over Me';
        });

        const keypressInput = document.getElementById('keypressInput');
        const keypressDisplay = document.getElementById('keypress-display');
        keypressInput.addEventListener('keyup', function(event) {
            keypressDisplay.textContent = 'You typed: ' + event.key;
        });

        const doubleClickButton = document.getElementById('doubleClickButton');
        doubleClickButton.addEventListener('dblclick', function() {
            alert('Double Clicked!');
        });

        let longPressTimer;
        doubleClickButton.addEventListener('mousedown', function() {
            longPressTimer = setTimeout(() => {
                alert('Long Press Detected!');
            }, 1000); // Adjust time (in milliseconds) for long press
        });
        doubleClickButton.addEventListener('mouseup', function() {
            clearTimeout(longPressTimer);
        });
        doubleClickButton.addEventListener('mouseleave', function() {
            clearTimeout(longPressTimer);
        });

        // 2. Interactive Elements
        const interactiveButton = document.getElementById('interactive-button');
        let buttonText = 'Change Text';
        interactiveButton.addEventListener('click', function() {
            buttonText = (buttonText === 'Change Text') ? 'Text Changed!' : 'Change Text';
            this.textContent = buttonText;
            this.style.backgroundColor = (this.style.backgroundColor === 'rgb(40, 167, 69)') ? '#007bff' : '#28a745';
        });

        function changeMainImage(newSrc) {
            document.getElementById('main-image').src = newSrc;
        }

        function openTab(tabId) {
            const tabContents = document.querySelectorAll('.tab-content');
            tabContents.forEach(content => content.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
        }

        // 3. Form Validation
        function validateRequired(input) {
            const errorDivId = input.id + 'Error';
            const errorDiv = document.getElementById(errorDivId);
            if (!input.value.trim()) {
                errorDiv.textContent = 'This field is required.';
                return false;
            } else {
                errorDiv.textContent = '';
                return true;
            }
        }

        function validateEmail(emailInput) {
            const errorDiv = document.getElementById('emailError');
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(emailInput.value)) {
                errorDiv.textContent = 'Invalid email format.';
                return false;
            } else {
                errorDiv.textContent = '';
                return true;
            }
        }

        function validatePassword(passwordInput) {
            const errorDiv = document.getElementById('passwordError');
            if (passwordInput.value.length < 8) {
                errorDiv.textContent = 'Password must be at least 8 characters long.';
                return false;
            } else {
                errorDiv.textContent = '';
                return true;
            }
        }

        document.getElementById('myForm').addEventListener('submit', function(event) {
            if (!validateRequired(document.getElementById('name')) ||
                !validateEmail(document.getElementById('email')) ||
                !validatePassword(document.getElementById('password'))) {
                event.preventDefault(); // Prevent form submission if validation fails
                alert('Please correct the form errors.');
            } else {
                alert('Form submitted successfully!');
            }
        });
    </script>
</body>
</html>
