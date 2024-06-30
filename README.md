<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Traffic Congestion Prediction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }

        .container {
            text-align: center;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        form {
            margin-bottom: 20px;
        }

        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        #result {
            margin-top: 20px;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Traffic Congestion Prediction</h1>
        <form id="uploadForm">
            <input type="file" id="imageInput" accept="image/*" required>
            <button type="submit">Upload and Predict</button>
        </form>
        <div id="result"></div>
    </div>
    <script>
        document.getElementById('uploadForm').addEventListener('submit', async (event) => {
            event.preventDefault();
            
            const imageInput = document.getElementById('imageInput');
            const file = imageInput.files[0];

            if (!file) {
                alert('Please select an image to upload');
                return;
            }

            const formData = new FormData();
            formData.append('file', file);

            try {
                const response = await fetch('http://localhost:3000/predict', {
                    method: 'POST',
                    body: formData
                });

                const result = await response.json();
                document.getElementById('result').innerText = `Prediction: ${result.prediction}`;
            } catch (error) {
                console.error('Error:', error);
                alert('Error uploading image. Please try again.');
            }
        });
    </script>
</body>
</html>
