# Chapter3 문제풀이


## P3.1
![image](https://github.com/minjae0512/Reports/assets/127775263/b01c3c50-a2fe-4063-b501-79dda46b462f)
### <Solution>
(a)

$$
x(t) = (x_1(t), x_2(t))
$$

$$
x_1(t) = y(t), x_2(t) = \frac{dy(t)}{dt}
$$

(b)

$$
M\frac{dy_2(t)}{dt} + by_2(t) + ky_1(t) = f(t)
$$

위에서 정의한 상태변수를 미분방정식에 대입하여 아래와 같은 두 개의 1차 미분방정식을 구할 수 있다.

$$
\frac{dx_1(t)}{dt} = x_2(t)
$$

$$
\frac{dx_2(t)}{dt} = -\frac{b}{M}x_2(t) -\frac{k}{M}x_1(t) + \frac{1}{M}f(t)
$$

(c)

$$
x(t) = \begin{bmatrix} x_1(t) \\
x_2(t) \end{bmatrix}
$$

$$
y(t) = x_1(t)
$$

위의 두 행렬을 이용해 다음과 같은 상태미분 방정식을 나타낼 수 있다.

$$
\dot{x}(t) = \begin{bmatrix} 0 & 1\\
-\frac{k}{M} & -\frac{b}{M} \end{bmatrix}x(t) + \begin{bmatrix} 0 \\
\frac{1}{M} \end{bmatrix}f(t)
$$

$$
y(t) = \begin{bmatrix} 1 & 0\end{bmatrix}x(t)
$$


## P3.3
![image](https://github.com/minjae0512/Reports/assets/127775263/e796cffa-f8a1-47b4-8206-35366c889e9d)
상태변수는 다음과 같다.

$$
x_1(t) = i_L(t), x_2(t) = v_c(t)
$$

KVL을 적용하면 다음과 같은 식을 얻을 수 있다.

$$
L\frac{di_L(t)}{dt} - v_c(t) + v_2(t) - v_1(t) = 0
$$

KCL을 적용하면 다음과 같은 식을 얻을 수 있다.

$$
C\frac{dv_c(t)}{dt} = -i_L(t) + i_R
$$

저항에 흐르는 전류를 다음에서 얻을 수 있다.

$$
i_RR - v_2(t) + v_c(t) = 0
$$

$$
i_R = \frac{v_2(t)}{R} - \frac{v_1(t)}{R}
$$

이를 위에서 구한 KCL 식에 대입하면 다음과 같이 정리할 수 있다.

$$
C\frac{dv_c(t)}{dt} = -i_L(t) + \frac{v_2(t)}{R} - \frac{v_1(t)}{R}
$$

위에서 구한 식들을 2개의 1차미분 방정식으로 정리하면 다음과 같다.

$$
\frac{di_L(t)}{dt} = \frac{v_c(t)}{L} + \frac{v_1(t)}{L} - \frac{v_2(t)}{L}
$$

$$
\frac{dv_c(t)}{dt} = - \frac{i_L(t)}{C} -\frac{v_c(t)}{RC} + \frac{v_2(t)}{RC}
$$

위의 두 식들을 이용하여 상태미분 방정식을 표현하면 다음과 같다.

$$
x(t) = \begin{bmatrix} i_L(t) \\
v_c(t)\end{bmatrix}
$$

$$
v(t) = \begin{bmatrix} v_1(t) \\
v_2(t)\end{bmatrix}
$$

$$
\dot{x}(t)= \begin{bmatrix} 0 & 1/L \\
-1/C & -1/RC
\end{bmatrix}x(t) + \begin{bmatrix} 1/L & -1/L \\
0 & 1/RC
\end{bmatrix}v(t)
$$


## P3.5
![image](https://github.com/minjae0512/Reports/assets/127775263/ee02c299-27a1-4233-9f47-214de75d5407)

(a)

폐루프 전달함수는 다음과 같다.

$$
T(s) = \frac{Y(s)}{R(s)} = \frac{G(s)}{1+G(s)} = \frac{\frac{s+2}{s^3+5s^2-24s}}{1+\frac{s+2}{s^3+5s^2-24s}} = \frac{s+2}{s^3 + 5s^2 - 23s +2}
$$

(b)
Phase variable canonical form을 이용하여 전달함수를 통해 상태공간 방정식을 다음과 같이 구할 수 있다.

$$
T(S) = \frac{Y(S)}{R(S)} = \frac{S + 2}{S^3 + 5S^2 -23S + 2}
$$

$$
\frac{Y(S)}{R(S)} = \frac{(S + 2)Z(S)}{(S^3 + 5S^2 -23S + 2)Z(S)}
$$

$$
y(t) = \dot{z}(t) + 2z(t) , r(t) = \dddot{z}(t) + 5\ddot{z}(t) -23\dot{z}(t) +2z(t)
$$

$$
\dot{x}(t) = \begin{bmatrix} x_1(t) \\
x_2(t) \\
x_3(t)\end{bmatrix} = \begin{bmatrix} z(t)\\
\dot{z}(t) \\
\ddot{z}(t) \end{bmatrix}
$$

$$
x(t) = \begin{bmatrix} 0 & 1 & 0 \\
0 & 0 & 1 \\
-2 & 23 & -5 \end{bmatrix}x(t) + \begin{bmatrix} 0 \\
0 \\
1 \end{bmatrix}r(t)
$$

$$
y(t) = \begin{bmatrix} 2 & 1 & 0\end{bmatrix}x(t)
$$

이를 matlab으로 표현하면 다음과 같다.

```matlab
num = [0 0 1 2];
den = [1 5 -23 2];

[A,B,C,D] = tf2ss(num,den);

A
B
C
D

syms s
Phi = inv(s*eye(3) - A);
G = C*Phi*B + D;
[n,d] = numden(G)

```
![image](https://github.com/minjae0512/Reports/assets/127775263/2d96fe62-8d71-49cc-ba2f-dc5c11eb4b3d)

## P3.12
![image](https://github.com/minjae0512/Reports/assets/127775263/ba8676cb-782c-4a80-92d0-b19e1479f58c)
(a)
상태공간모델은 matlab을 이용하여 다음과 같이 나타낼 수 있다.
![image](https://github.com/minjae0512/Reports/assets/127775263/8997fcd8-110b-4b5c-acdd-018da6997c01)

$$
\dot{x} = \begin{bmatrix} 0 & 1 & 0 \\
0 & 0 & 1\\
-48 & -44 & -12 \end{bmatrix}x + \begin{bmatrix} 0 \\
0 \\
1 \end{bmatrix}r
$$

$$
y = \begin{bmatrix} 40 & 8 & 0\end{bmatrix}x
$$

(b)
상태천이행렬 $\Phi(t)$는 $\Phi(S) = [sI-A]^-$를 역라플라스로 치환하여 구할 수 있다.

$$
\Phi(t) = \begin{bmatrix} \Phi_1(t) \vdots \Phi_2(t) \vdots \Phi3(t)\end{bmatrix}
$$

$$
\Phi_1(t) = \begin{bmatrix} e^{-6t} - 3e^{-4t} + 3e^{-2t} \\
-6e^{-6t} - 12e^{-4t} - 6e^{-2t} \\
36e^{-6t} - 48e^{-4t} + 12e^{-2t} \end{bmatrix}
$$


$$
\Phi_2(t) = \begin{bmatrix} \frac{3}{4}e^{-6t} - 2e^{-4t} + \frac{5}{4}e^{-2t} \\
-\frac{9}{2}e^{-6t} + 8e^{-4t} - \frac{5}{2}e^{-2t} \\
27e^{-6t} - 32e^{-4t} + 5e^{-2t} \end{bmatrix}
$$


$$
\Phi_3(t) = \begin{bmatrix} \frac{1}{8}e^{-6t} - \frac{1}{4}e^{-4t} + \frac{1}{8}e^{-2t} \\
-\frac{3}{4}e^{-6t} - e^{-4t} - \frac{1}{4}e^{-2t} \\
\frac{9}{2}e^{-6t} - 4e^{-4t} + \frac{1}{2}e^{-2t} \end{bmatrix}
$$

이를 matlab으로 표현하면 다음과 같다.
![image](https://github.com/minjae0512/Reports/assets/127775263/b54436c7-77e5-490f-8677-a8e4a81ae0c0)

## P3.17
![image](https://github.com/minjae0512/Reports/assets/127775263/7f2d51fa-6884-44f8-8871-ab24e1b240e6)
matlab을 이용하여 다음과 같이 전달함수를 얻을 수 있다.

```matlab
syms s
A = [1, 1, -1; 4, 3, 0; -2, 1, 10];
B = [0; 0; 4];
C = [1, 0, 0];
D = 0;
Phi = inv(s*eye(3) - A);
G = C*Phi*B+D;
[n,d] = numden(G)
```
![image](https://github.com/minjae0512/Reports/assets/127775263/c1c170b7-dc20-43f5-9c8c-8a52bc73bd6a)
