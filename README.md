# Calculator
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Basic Calculator</title>
    <style>
.calculator-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
}

button {
    background-color: #f0f0f0;
    border: none;
    padding: 10px;
    font-size: 18px;
    cursor: pointer;
}

button:hover {
    background-color: #ccc;
}

#display {
    width: 98%;
    height: 30px;
    font-size: 20px;
    padding: 10px;
    text-align: right;
}
    </style>
</head>
<body>
    <h1>Basic Calculator</h1>
    <input type="text" id="display" readonly>
    <div class="calculator-grid">
    <button class="number">7</button>
    <button class="number">8</button>
    <button class="number">9</button>
    <button class="operator">/</button>
    <button class="number">4</button>
    <button class="number">5</button>
    <button class="number">6</button>
    <button class="operator">*</button>
    <button class="number">1</button>
    <button class="number">2</button>
    <button class="number">3</button>
    <button class="operator">-</button>
    <button class="number">0</button>
    <button class="operator">C</button>
    <button class="operator">=</button>
    <button class="operator">+</button>

        <button id="decimal">.</button>
    </div>

    <script>
           // script.js
let display = document.getElementById('display');
let buttons = document.querySelectorAll('button');

let calculator = {
    displayValue: '',
    firstOperand: null,
    secondOperand: null,
    operator: null,
};

buttons.forEach(button => {
    button.addEventListener('click', handleButtonPress);
});

function handleButtonPress(event) {
    let buttonValue = event.target.textContent;

    if (buttonValue === 'C') {
        calculator.displayValue = '';
        calculator.firstOperand = null;
        calculator.secondOperand = null;
        calculator.operator = null;
    } else if (buttonValue === '=' && calculator.operator) {
        calculator.secondOperand = parseFloat(calculator.displayValue);
        let result = calculate(calculator.firstOperand, calculator.secondOperand, calculator.operator);
        calculator.displayValue = result.toString();
        calculator.firstOperand = null;
        calculator.secondOperand = null;
        calculator.operator = null;
    } else if (buttonValue === '+' || buttonValue === '-' || buttonValue === '*' || buttonValue === '/') {
        calculator.firstOperand = parseFloat(calculator.displayValue);
        calculator.operator = buttonValue;
        calculator.displayValue = '';
    } else {
        calculator.displayValue += buttonValue;
    }

    display.value = calculator.displayValue;
}

function calculate(a, b, operator) {
    switch (operator) {
        case '+':
            return a + b;
        case '-':
            return a - b;
        case '*':
            return a * b;
        case '/':
            return a / b;
        default:
            return null;
    }
}
    </script>
</body>
</html>
