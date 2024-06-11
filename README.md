# ihc_public
Practice_public_IHC

## simple calculator
- chatgpt에게 코딩 시킴
- flask 사용한 웹 프로그램
- 단순한 계산기

### app.py
[코드연결](./simple_calculator/app.py)
```python
from flask import Flask, render_template, request
app = Flask(__name__)
@app.route('/')
def home():
    return render_template('index.html')

@app.route('/calculate', methods=['POST'])
def calculate():
    try:
        num1 = float(request.form['num1'])
        num2 = float(request.form['num2'])
        operation = request.form['operation']
        if operation == 'add':
            result = num1 + num2
        elif operation == 'subtract':
            result = num1 - num2
        elif operation == 'multiply':
            result = num1 * num2
        elif operation == 'divide':
            result = num1 / num2
        else:
            result = 'Invalid operation'
    except Exception as e:
        result = f'Error: {str(e)}'
    return render_template('index.html', result=result)

if __name__ == '__main__':
    app.run(debug=True)
```

### templates/index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
</head>
<body>
    <h1>Weather Information</h1>
    <form action="/weather" method="post">
        <input type="text" name="city" placeholder="Enter city name" required>
        <button type="submit">Get Weather</button>
    </form>
    {% if weather %}
        <h2>Weather in {{ weather.city }}</h2>
        <p>Temperature: {{ weather.temperature }}°C</p>
        <p>Description: {{ weather.description }}</p>
        <img src="http://openweathermap.org/img/w/{{ weather.icon }}.png" alt="Weather icon">
    {% endif %}
</body>
</html>
```