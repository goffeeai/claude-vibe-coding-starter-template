# Flask

## Overview
Lightweight Python web framework

## Installation

```bash
pip install flask
```

---

## Basic Server

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def hello():
    return jsonify({'message': 'Hello World!'})

if __name__ == '__main__':
    app.run(debug=True)
```

---

## Project Structure

```
app/
├── __init__.py       # App factory
├── routes/
│   ├── __init__.py
│   └── users.py
├── models/
│   └── user.py
├── services/
│   └── user_service.py
├── templates/
├── static/
└── config.py
```

---

## App Factory Pattern

```python
# app/__init__.py
from flask import Flask

def create_app():
    app = Flask(__name__)
    app.config.from_object('config')

    from .routes import users
    app.register_blueprint(users.bp)

    return app
```

---

## Routing

```python
from flask import Blueprint, jsonify, request

bp = Blueprint('users', __name__, url_prefix='/users')

@bp.route('/', methods=['GET'])
def get_users():
    return jsonify(users)

@bp.route('/', methods=['POST'])
def create_user():
    data = request.get_json()
    return jsonify(data), 201

@bp.route('/<int:user_id>', methods=['GET'])
def get_user(user_id):
    return jsonify({'id': user_id})
```

---

## Request & Response

```python
from flask import request, jsonify

@app.route('/users', methods=['POST'])
def create_user():
    # Request
    json_data = request.get_json()
    form_data = request.form
    query_param = request.args.get('name')
    header = request.headers.get('Authorization')

    # Response
    return jsonify({'user': json_data}), 201
```

---

## Flask-SQLAlchemy

```bash
pip install flask-sqlalchemy
```

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    email = db.Column(db.String(120), unique=True)

# In app factory
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///app.db'
db.init_app(app)

with app.app_context():
    db.create_all()
```

---

## Error Handling

```python
@app.errorhandler(404)
def not_found(error):
    return jsonify({'error': 'Not found'}), 404

@app.errorhandler(500)
def internal_error(error):
    return jsonify({'error': 'Internal server error'}), 500
```

---

## Running

```bash
# Development
flask run --debug

# Or
python app.py

# Production (with gunicorn)
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 "app:create_app()"
```

---

## Why Flask?

- Simple and lightweight
- Easy to learn
- Flexible (choose your own tools)
- Great for small-medium apps
- Good for APIs and microservices
