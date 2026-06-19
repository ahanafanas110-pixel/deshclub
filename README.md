from flask import Flask, jsonify
from flask_cors import CORS
import requests
import time

app = Flask(__name__)
CORS(app) # ফ্রন্টএন্ড থেকে রিকোয়েস্ট এক্সেপ্ট করার জন্য

@app.route('/get-data', methods=['GET'])
def get_game_data():
    target_url = "https://api.inpay88.net/api/webapi/GetNoaverageEmerdList"
    
    headers = {
        "accept": "application/json, text/plain, */*",
        "authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOiIxNzgxODkwMzE5IiwibmJmIjoiMTc4MTg5MDMxOSIsImV4cCI6IjE3ODE4OTIxMTkiLCJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL2V4cGlyYXRpb24iOiI2LzIwLzIwMjYgMTI6MDE6NTkgQU0iLCJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3JvbGUiOiJBY2Nlc3NfVG9rZW4iLCJVc2VySWQiOiIxMjE4MzIiLCJVc2VyTmFtZSI6Ijg4MDY2OTk4ODU2NjkiLCJVc2VyUGhvdG8iOiIyNiIsIk5pY2tOYW1lIjoiT1dORVIgRkFISU0gIiwiQW1vdW50IjoiMTE1OTI1LjgwIiwiSW50ZWdyYWwiOiIwIiwiTG9naW5NYXJrIjoiSDUiLCJMb2dpblRpbWUiOiI2LzE5LzIwMjYgMTE6MzE6NTkgUE0iLCJMb2dpbklQQWRkcmVzcyI6IjEwMy4xMzUuODkuMjAzIiwiRGJOdW1iZXIiOiIwIiwiSXN2YWxpZGF0b3IiOiIwIiwiS2V5Q29kZSI6IjiMzgiLCJUb2tlblR5cGUiOiJBY2Nlc3NfVG9rZW4iLCJQaG9uZVR5cGUiOiIwIiwiVXNlclR5cGUiOiIxIiwiVXNlck5hbWUyIjoiIiwiaXNzIjoqd3RJc3N1ZXIiLCJhdWQiOiJsb3R0ZXJ5VGlja2V0In0.t2kVHuZ7ZVKcLb4ZltI4pU9J7xMF_s1LcyS1sdG198E",
        "content-type": "application/json;charset=UTF-8",
        "referrer": "https://deshclub2.com/",
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36"
    }
    
    payload = {
        "pageSize": 10,
        "pageNo": 1,
        "typeId": 30,
        "language": 0,
        "visitorId": "3badb09dcd2e1ba43d947e028548b6c9",
        "random": "2259d74633354723b58ecbfbc99c26c6",
        "signature": "246A101325615106C6CEE67FA997C07C",
        "timestamp": int(time.time())
    }
    
    try:
        response = requests.post(target_url, json=payload, headers=headers, timeout=10)
        return jsonify(response.json())
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
