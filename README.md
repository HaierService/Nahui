<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Inverter Troubleshooting</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .menu, .steps {
            margin-bottom: 20px;
        }
        .hidden {
            display: none;
        }
    </style>
    <script>
        const selectionCounts = {
            'question1': 0,
            'question2': 0,
            'question3': 0,
	    'question4': 0, 
		
        };

        function showMenu() {
            document.getElementById('menu').classList.remove('hidden');
            document.getElementById('steps').classList.add('hidden');
        }

        function showSteps(questionId) {
            document.getElementById('menu').classList.add('hidden');
            document.getElementById('steps').classList.remove('hidden');
            const steps = document.querySelectorAll('.step');
            steps.forEach(step => step.classList.add('hidden'));
            document.getElementById(questionId).classList.remove('hidden');
            selectionCounts[questionId]++;
        }

        function backToStart() {
            showMenu();
        }

        function exportToExcel() {
            let csvContent = "data:text/csv;charset=utf-8,Question,Count\n";
            for (const question in selectionCounts) {
                csvContent += `${question},${selectionCounts[question]}\n`;
            }
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "troubleshooting_counts.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
    </script>
</head>
<body>
    <div id="menu" class="menu">
        <h1>Inverter Troubleshooting</h1>
        <button onclick="showSteps('question1')">Why the inverter is not working?</button><br>
        <button onclick="showSteps('question2')">Why the inverter is limited with certain power?</button><br>
        <button onclick="showSteps('question3')">Why the battery is not charging?</button><br>
	<button onclick="showSteps('question4')">How to connect the inverter into internet?</button>

    </div>
    <div id="steps" class="steps hidden">
        <div id="question1" class="step hidden">
            <h2>Why the inverter is not working?</h2>
            <ol>
                <li>Check if the inverter is properly connected to the power source.</li>
                <li>Ensure the inverter's switch is turned on.</li>
                <li>Verify if there are any visible damages to the inverter.</li>
                <li>If the issue persists, contact technical support.</li>
            </ol>
        </div>
        <div id="question2" class="step hidden">
            <h2>Why the inverter is limited with certain power?</h2>
            <ol>
                <li>Check if the power load exceeds the inverter's capacity.</li>
                <li>Ensure the inverter settings are configured correctly.</li>
                <li>Verify if the input power source is stable and sufficient.</li>
                <li>If the issue persists, contact technical support.</li>
            </ol>
        </div>
        <div id="question3" class="step hidden">
            <h2>Why the battery is not charging?</h2>
            <ol>
                <li>Check if the battery is properly connected to the inverter.</li>
                <li>Ensure the battery is not damaged or too old.</li>
                <li>Verify if the inverter is providing the correct charging voltage.</li>
                <li>If the issue persists, contact technical support.</li>
            </ol>
        </div>
	<div id="question4" class="step hidden">
            <h2>How to connect the inverter into internet?</h2>
            <ol>
                <li>Open Nahui Business App and turn on Bluetooth.</li>
                <li>Select Icon Tools.</li>
                <li>Select the Doungle "D_xxxxxx".</li>
                <li>Select the Wifi-Name and enter the Password.</li>
            </ol>
        </div>

        <button onclick="backToStart()">Back to Start</button>
    </div>
    <button onclick="exportToExcel()">Export Troubleshooting Counts to Excel</button>
</body>
</html>
