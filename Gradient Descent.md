```python
import matplotlib # learn more: https://python.org/pypi/matplotlib
from numpy import *
import matplotlib.pyplot as plt

def compute_error_for_line_given_points(b, m, points):
    totalError = 0
    for i in range(0, len(points)):
        x = points[i][0]
        y = points[i][1]
        totalError += (y - (m * x + b)) ** 2
    return totalError / float(len(points))

def stepGradient(b_current, m_current, points, learningRate):
    b_gradient = 0
    m_gradient = 0
    N = float(len(points))
    for i in range(0, len(points)):
        b_gradient += -(2/N)*(points[i][1] - ((m_current*points[i][0]) + b_current))
        m_gradient += -(2/N)*points[i][0]*(points[i][1] - ((m_current*points[i][0]) + b_current))
    new_b = b_current - (learningRate*b_gradient)
    new_m = m_current - (learningRate*m_gradient)
    return [new_b, new_m]

def gradient_descent_runner(points, starting_b, starting_m, learning_rate):
    b = starting_b
    m = starting_m
    a=compute_error_for_line_given_points(b, m, points)
    while(a > 5):
        b, m = stepGradient(b, m, points, learning_rate)
        a=compute_error_for_line_given_points(b, m, points)
        print(a, m, b)
    return [b, m]

points = [(92,95),(55,70),(100,95),(88,85),(61,75),(75,80)]
learning_rate = 0.00015
initial_b = 20 # initial y-intercept guess
initial_m = 1 # initial slope guess
b,m = gradient_descent_runner(points, initial_b, initial_m, learning_rate)

print(b,m)
```
