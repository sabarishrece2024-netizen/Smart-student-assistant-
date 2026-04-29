# Smart-student-assistant-
from flask import Flask, request, jsonify
from datetime import datetime

app = Flask(__name__)

students = []
assignments = []
attendance = {}

# Home Route
@app.route('/')
def home():
    return "Smart Student Assistant App Running Successfully"

# Add Student
@app.route('/add_student', methods=['POST'])
def add_student():
    data = request.json

    student = {
        "name": data['name'],
        "department": data['department'],
        "year": data['year']
    }

    students.append(student)

    return jsonify({
        "message": "Student Added Successfully",
        "student": student
    })

# Add Assignment
@app.route('/add_assignment', methods=['POST'])
def add_assignment():
    data = request.json

    assignment = {
        "title": data['title'],
        "subject": data['subject'],
        "deadline": data['deadline']
    }

    assignments.append(assignment)

    return jsonify({
        "message": "Assignment Added Successfully",
        "assignment": assignment
    })

# View Assignments
@app.route('/view_assignments', methods=['GET'])
def view_assignments():
    return jsonify(assignments)

# Attendance Tracker
@app.route('/mark_attendance', methods=['POST'])
def mark_attendance():
    data = request.json

    name = data['name']
    status = data['status']

    attendance[name] = status

    return jsonify({
        "message": "Attendance Marked Successfully",
        "attendance": attendance
    })

# Productivity Score
@app.route('/productivity', methods=['GET'])
def productivity():
    completed = len(assignments)
    score = completed * 10

    return jsonify({
        "productivity_score": score
    })

# AI Study Recommendation
@app.route('/study_recommendation', methods=['GET'])
def study_recommendation():

    recommendation = {
        "tip": "Focus on difficult subjects during morning hours for better concentration."
    }

    return jsonify(recommendation)

if __name__ == '__main__':
    app.run(debug=True)
