# -
питайся сбалансированно 
from flask import Flask, request, jsonify

app = Flask(__name__)

def calculate_kbju(data):
    weight = float(data['weight'])
    height = float(data['height'])
    age = int(data['age'])
    sex = data['sex']
    activity = data['activity']
    goal = data['goal']

    if sex.lower() == 'жен':
        bmr = 10 * weight + 6.25 * height - 5 * age - 161
    else:
        bmr = 10 * weight + 6.25 * height - 5 * age + 5

    activity_map = {
        "низкая": 1.2,
        "умеренная": 1.375,
        "средняя": 1.55,
        "высокая": 1.725
    }
    tdee = bmr * activity_map.get(activity.lower(), 1.375)

    if goal.lower() == 'похудение':
        calories = tdee - tdee * 0.2
    elif goal.lower() == 'набор':
        calories = tdee + tdee * 0.15
    else:
        calories = tdee

    proteins = weight * 1.8
    fats = weight * 0.9
    carbs = (calories - (proteins * 4 + fats * 9)) / 4

    return {
        "calories": round(calories),
        "proteins": round(proteins),
        "fats": round(fats),
        "carbs": round(carbs)
    }

@app.route('/calculate', methods=['POST'])
def calculate():
    data = request.json
    result = calculate_kbju(data)
    return jsonify(result)

@app.route('/')
def home():
    return "Бот-диетолог работает!"

if __name__ == '__main__':
    app.run()from flask import Flask, request, jsonify

app = Flask(__name__)

def calculate_kbju(data):
    weight = float(data['weight'])
    height = float(data['height'])
    age = int(data['age'])
    sex = data['sex']
    activity = data['activity']
    goal = data['goal']

    if sex.lower() == 'жен':
        bmr = 10 * weight + 6.25 * height - 5 * age - 161
    else:
        bmr = 10 * weight + 6.25 * height - 5 * age + 5

    activity_map = {
        "низкая": 1.2,
        "умеренная": 1.375,
        "средняя": 1.55,
        "высокая": 1.725
    }
    tdee = bmr * activity_map.get(activity.lower(), 1.375)

    if goal.lower() == 'похудение':
        calories = tdee - tdee * 0.2
    elif goal.lower() == 'набор':
        calories = tdee + tdee * 0.15
    else:
        calories = tdee

    proteins = weight * 1.8
    fats = weight * 0.9
    carbs = (calories - (proteins * 4 + fats * 9)) / 4

    return {
        "calories": round(calories),
        "proteins": round(proteins),
        "fats": round(fats),
        "carbs": round(carbs)
    }

@app.route('/calculate', methods=['POST'])
def calculate():
    data = request.json
    result = calculate_kbju(data)
    return jsonify(result)

@app.route('/')
def home():
    return "Бот-диетолог работает!"

if __name__ == '__main__':
    app.run()
    
