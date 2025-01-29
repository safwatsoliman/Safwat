<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Signal Filter Bot</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: black; /* Black background */
            color: cyan; /* Cyan text */
            border: 2px solid cyan; /* Cyan border */
            border-radius: 10px; /* Rounded corners */
            box-shadow: 0 0 20px cyan; /* Light glow effect */
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: #222; /* Table background */
            color: cyan; /* Table text color */
        }
        th, td {
            border: 1px solid cyan; /* Table border color */
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #444; /* Header background */
        }
        .no-results {
            color: red; /* No results message color */
            margin-top: 20px;
        }
        button {
            background-color: cyan; /* Button color */
            color: black; /* Button text color */
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #00bfff; /* Button hover effect */
        }
        textarea {
            width: 100%;
            height: 100px;
            border: 1px solid cyan; /* Textarea border */
            border-radius: 5px; /* Rounded corners */
            background-color: #333; /* Textarea background */
            color: cyan; /* Textarea text color */
        }
    </style>
</head>
<body>

<h1>Signal Filter Bot</h1>
<label for="signalsInput">Enter the list of signals (one per line):</label><br>
<textarea id="signalsInput" rows="10" cols="50" placeholder="CAD/CHF➢ ; 14:14 ; CALL"></textarea><br><br>

<label for="minProfit">Minimum profit percentage (0 to 100):</label>
<input type="number" id="minProfit" value="70" min="0" max="100" /><br><br>

<button onclick="filterSignals()">Filter Signals</button>

<h3>Good Signals:</h3>
<table id="signalsTable">
    <thead>
        <tr>
            <th>Signal</th>
        </tr>
    </thead>
    <tbody>
        <!-- Good signals will be added here -->
    </tbody>
</table>

<div class="no-results" id="noResultsMessage" style="display: none;">No matching signals found.</div>

<script>
    function filterSignals() {
        const signalsInput = document.getElementById('signalsInput').value;
        const minProfit = parseFloat(document.getElementById('minProfit').value);
        const tableBody = document.getElementById('signalsTable').getElementsByTagName('tbody')[0];
        const noResultsMessage = document.getElementById('noResultsMessage');

        // Clear the current table
        tableBody.innerHTML = '';
        noResultsMessage.style.display = 'none'; // Hide no results message

        // Split the input into lines
        const signals = signalsInput.split('\n');
        let foundMatch = false; // Variable to check if any matches are found

        signals.forEach(signal => {
            if (signal.trim() === '') return; // Skip empty lines
            
            const parts = signal.split(';');
            if (parts.length < 3) return; // Ensure all parts are present

            const tradeDetail = parts[0].trim(); // Signal details
            const tradeTime = parts[1].trim(); // Signal time
            const tradeType = parts[2].trim(); // Signal type (CALL or PUT)

            // Randomly simulating profit percentage (modify this logic later)
            const profitPercentage = Math.random() * 100; 

            // Adjust profit percentage threshold to display more signals
            if (profitPercentage >= minProfit) {
                const row = tableBody.insertRow();
                const cell = row.insertCell(0);
                cell.textContent = `${tradeDetail} ; ${tradeTime} ; ${tradeType}`; // Add signal to the table without profit percentage
                foundMatch = true; // A matching signal has been found
            }
        });

        // If no matching signals are found, display a message
        if (!foundMatch) {
            noResultsMessage.style.display = 'block';
        }
    }
</script>

</body>
</html>
