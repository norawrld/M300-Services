Container sichern und beschränken:

Image erstellen:
![Screenshot 2023-07-09 235310](https://github.com/norawrld/M300-Services/assets/87812697/aab9bce7-093e-4cb1-bc5b-728f31c1b623)

Dockerfile:

FROM python:3.9

RUN groupadd -r appuser && useradd -r -g appuser appuser

WORKDIR /app
COPY . /app

RUN pip install --no-cache-dir -r requirements.txt

RUN chown -R appuser:appuser /app
USER appuser

CMD ["python", "app.py"]

Container erstellen:
![Screenshot 2023-07-09 235501](https://github.com/norawrld/M300-Services/assets/87812697/ebb60fe1-b327-4bae-a28c-b008ed54280d)

Python file:

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello, World!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)

Requirements:
Flask==2.1.0

![Screenshot 2023-07-09 235701](https://github.com/norawrld/M300-Services/assets/87812697/8e7f9cd5-e76e-44fa-a2f7-fde89944f53d)

![Screenshot 2023-07-09 235755](https://github.com/norawrld/M300-Services/assets/87812697/744e9adf-7d05-46ad-a212-5b126c3cadcf)

