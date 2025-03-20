# Shape-area-calculator
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Shape Area Calculator</title>

    <style>

        body {

            font-family: Arial, sans-serif;

            text-align: center;

            margin: 50px;

        }

        .container {

            max-width: 500px;

            margin: auto;

            padding: 20px;

            border: 1px solid #ccc;

            border-radius: 10px;

            box-shadow: 2px 2px 10px rgba(0,0,0,0.1);

        }

        .output {

            margin-top: 20px;

            text-align: left;

        }

    </style>

</head>

<body>

    <div class="container">

        <h2>Choose a Shape</h2>

        <button onclick="chooseShape('circle')">Circle</button>

        <button onclick="chooseShape('rectangle')">Rectangle</button>

        <br><br>

        <div id="dimensions"></div>

        <br>

        <div id="inputSection" style="display: none;">

            <label for="sValue">Enter S Value:</label>

            <input type="number" id="sValue" required>

            <button onclick="calculateValues()">Calculate</button>

        </div>

        <div class="output" id="output"></div>

    </div>



    <script>

        let shape = "";

        let area = 0;

        

        function chooseShape(selectedShape) {

            shape = selectedShape;

            let dimensionsHTML = "";

            

            if (shape === "circle") {

                dimensionsHTML = '<label for="radius">Enter Radius:</label> <input type="number" id="radius">';

            } else if (shape === "rectangle") {

                dimensionsHTML = '<label for="length">Enter Length:</label> <input type="number" id="length"><br><label for="width">Enter Width:</label> <input type="number" id="width">';

            }

            

            document.getElementById("dimensions").innerHTML = dimensionsHTML + '<br><button onclick="calculateArea()">Submit</button>';

        }

        

        function calculateArea() {

            if (shape === "circle") {

                let radius = parseFloat(document.getElementById("radius").value);

                area = Math.PI * radius * radius;

            } else if (shape === "rectangle") {

                let length = parseFloat(document.getElementById("length").value);

                let width = parseFloat(document.getElementById("width").value);

                area = length * width;

            }

            

            let p = area / 9;

            let k = (p % 1 > 0.1) ? Math.ceil(p) : Math.floor(p);

            

            document.getElementById("inputSection").style.display = "block";

            document.getElementById("output").innerHTML = `<p>Area: ${area.toFixed(2)}</p><p>P: ${p.toFixed(2)}</p><p>K: ${k}</p>`;

        }



        function calculateValues() {

            let S = parseFloat(document.getElementById("sValue").value);

            let values = [];

            

            function computeValue(mul, div, defaultValue) {

                let temp = S * mul;

                let rounded = Math.floor(temp / div) * div;

                let result = temp - rounded;

                return result === 0 ? defaultValue : result;

            }

            

            values.push(computeValue(9, 120, 0));

            values.push(computeValue(9, 8, 0));

            values.push(computeValue(8, 12, 12));

            values.push(computeValue(3, 8, 8));

            values.push(values[2] - values[3]);

            values.push(computeValue(3, 8, 8));

            values.push([computeValue(6, 30, 30), computeValue(8, 30, 30)]);

            values.push(computeValue(9, 7, 7));

            values.push([computeValue(5, 7, 7), computeValue(5, 11, 11)]);

            values.push(computeValue(8, 27, 27));

            values.push(computeValue(4, 27, 27));

            values.push(computeValue(6, 9, 9));

            values.push(computeValue(9, 12, 12));

            values.push(computeValue(3, 5, 5));

            values.push(computeValue(9, 4, 4));

            values.push(computeValue(12, 16, 16));

            

            let outputHTML = "<h3>Calculated Values</h3>";

            values.forEach((val, index) => {

                outputHTML += `<p>Value ${index + 1}: ${Array.isArray(val) ? val.join(' , ') : val}</p>`;

            });

            

            document.getElementById("output").innerHTML += outputHTML;

        }

    </script>

</body>

</html>

