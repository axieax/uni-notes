# Perceptron Learning Algorithm table

Training data:

| Training Example | x1   | x2   | Class |
| ---------------- | ---- | ---- | ----- |
| a                | 0    | 1    | -1    |
| b                | 2    | 0    | -1    |
| c                | 1    | 1    | +1    |

Initial weights:

- w0 = -0.5
- w1 = 0
- w2 = 1

Assume learning rate $\eta$ is 1

| Step | Input | x1   | x2   | Class | Prediction           | Rounded        | w0                       | w1                 | w2                  |
| ---- | ----- | ---- | ---- | ----- | -------------------- | -------------- | ------------------------ | ------------------ | ------------------- |
| 0    | -     | -    | -    | -     | -                    | -              | -0.5                     | 0                  | 1                   |
| 1    | a     | 0    | 1    | -1    | $-0.5*1+0+1*1 = 0.5$ | $sgn(0.5) = 1$ | $-0.5 + (-1-1)*1 = -2.5$ | $0 + (-1-1)*0 = 0$ | $1 + (-1-1)*1 = -1$ |
|      |       |      |      |       |                      |                |                          |                    |                     |
|      |       |      |      |       |                      |                |                          |                    |                     |

Formulae:

- Adjusting weights
  - $w_i \leftarrow w_i + \eta(d-y)x_i$
  - $\eta > 0$ is the learning rate
  - $d$ is the desired output
  - $y$ is the actual output
- Prediction
  - $y = sgn(\sum_{i=0}^n) w_ix_i$



