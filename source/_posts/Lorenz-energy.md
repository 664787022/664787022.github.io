---
title: Lorenz 能量循环框架推导
date: 2023-04-17 16:25:09
tags: 
    - 数学推导
    - 大气理论
category: 大气数学理论
cover: /img/cover11.jpg
---



# 前言

Lorenz大气能量循环框架推导。

参考文献：

1. Lorenz, E. N. Available Potential Energy and the Maintenance of the General Circulation. *Tellus* **7**, 157–167 (1955).

2. 大气动力学，刘式适、刘式达，第一版和第二版

3. 动力气象学，吕美仲，第一版

# 有效位能的定义

有效位能是大气全位能与最小全位能之差。

全位能是位能 $P$ 与内能 $I$ 之和，垂直积分结果为

$$
\begin{align}
P + I &= \int_0^{ + \infty } {\rho (gz + {c_v}T)} dz\\\\
 &= \int_0^{ + \infty } { - \frac{ {\partial p} }{ {\partial z} }z} dz + \int_0^{ + \infty } {\rho {c_v}T} dz\\\\(静力平衡)
 &=  - \int_{ {p_s} }^0 z dp + \int_0^{ + \infty } {\rho {c_v}T} dz\\\\
 &=  - \int_{ {p_s} }^0 z dp + \int_0^{ + \infty } {\rho {c_v}T} dz,\\\\(分部积分)
 &=  - [pz]_{ {p_s} }^0 + \int_0^{ + \infty } p dz + \int_0^{ + \infty } {\rho {c_v}T} dz\\\\
 &= \int_0^{ + \infty } {\rho RT} dz + \int_0^{ + \infty } {\rho {c_v}T} dz\\\\
 &= \int_0^{ + \infty } {\rho (R + {c_v})T} dz\\\\
 &= \int_0^{ + \infty } {\rho {c_p}T} dz\\\\ 
 &= \frac{ { {c_p} } }{g}\int_0^{ {p_0} } T dp 
\end{align}
$$

其中 $ p_s $ 是地面气压，由于 $ T=\theta(\frac{p_{0} }{p})^{-\frac{R}{c_p} } $ 代入公式 (9)

$$
\begin{align}
P + I &= \frac{ { {c_p} } }{g}{\int_0^{ {p_s} } {\theta (\frac{ { {p_0} } }{p})} ^{ - \frac{R}{ { {c_p} } } } }dp\\\\
& = \frac{ { {c_p} } }{g}(1 + \frac{R}{ { {c_p} } }){p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ {p_s} } {\theta d{p^{1 + \frac{R}{ { {c_p} } } } } } \\\\ （分部积分）
 &= \frac{ { {c_p} } }{g}(1 + \frac{R}{ { {c_p} } }){p_0}^{ - \frac{R}{ { {c_p} } } }([\theta {p^{1 + \frac{R}{ { {c_p} } } } }]_0^{ {p_s} } - \int_0^{ {p_s} } { {p^{1 + \frac{R}{ { {c_p} } } } }d\theta } )\\\\
 &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { {p^{1 + \frac{R}{ { {c_p} } } } }d\theta } 
\end{align}
$$

 由于定义地表以下$\theta=0$,对$p$的积分范围$\int_0^{ {p_s} }$相当于对$\theta$的积分范围$\int_{+\infty}^{ {0} }$

那么有效位能可以用大气全位能与大气参考状态的全位能之差来表示

$$
\begin{align}
\ A &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { {p^{1 + \frac{R}{ { {c_p} } } } }d\theta  - } \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }d\theta } \\\\
 &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {p^{1 + \frac{R}{ { {c_p} } } } } - { {\bar p}^{1 + \frac{R}{ { {c_p} } } } } } d\theta }
\end{align}
$$

$\bar p$  表示等熵参考面上气压的平均值。全球平均（水平平均）有效位能为

$$
\begin{align}
\bar A &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } {\overline { {p^{1 + \frac{R}{ { {c_p} } } } } - { {\bar p}^{1 + \frac{R}{ { {c_p} } } } } } d\theta } 
\end{align}
$$

取 $p=\bar p + p\prime$ 

$$
\begin{align}
\bar A &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } {\overline { {p^{1 + \frac{R}{ { {c_p} } } } } - { {\bar p}^{1 + \frac{R}{ { {c_p} } } } } } d\theta } \\\\
 &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } {(\overline {\bar p + p'{)^{1 + \frac{R}{ { {c_p} } } } } - { {\bar p}^{1 + \frac{R}{ { {c_p} } } } } } d\theta } \\\\
 &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }({ {(1 + \frac{ {p'} }{ {\bar p} })}^{1 + \frac{R}{ { {c_p} } } } } - 1)d\theta } \\\\(\frac{\bar p}{p\prime}=0处泰勒展开)
 &= \frac{ { {c_p} } }{g}{(1 + \frac{R}{ { {c_p} } })^{ - 1} }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } {\overline { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }(1 + \frac{ {(1 + \frac{R}{ { {c_p} } }){ {(1 + 0)}^{\frac{R}{ { {c_p} } } } } } }{ {1!} }(\frac{ {p'} }{ {\bar p} } - 0) + } } \\\\
&\overline { + \frac{ {(1 + \frac{R}{ { {c_p} } })\frac{R}{ { {c_p} } }{ {(1 + 0)}^{\frac{R}{ { {c_p} } } - 1} } } }{ {2!} }{ {(\frac{ {p'} }{ {\bar p} } - 0)}^2} + ... - 1)} d\theta \\\\(保留到2阶，1阶平均为0)
 &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }{ {(\overline {\frac{ {p'} }{ {\bar p} } } )}^2}d\theta } 
\end{align}
$$

即

$$
\begin{align}
\bar A &=\frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }{ {(\overline {\frac{ {p'} }{ {\bar p} } } )}^2}d\theta }
\end{align}
$$

## P坐标系下有效位能

定义 $\bar \theta$, $\theta'$ , $\bar T$, $T'$ 分别是等压面上的均值和偏差。对于等熵面上的气压，近似有 $ p=\bar p(\bar {\theta} ( p ) ) $ 。由此

$$
\begin{align}
p' &= p - \bar p\\\\
 &= \bar p(\bar \theta ) - \bar p(\theta )\\\\
 &= \bar p(\theta  - \theta ') - \bar p(\theta )\\\\(\bar p(\theta-\theta\prime)在\theta处泰勒展开)
 &= \bar p(\theta ) + \frac{ {\bar p(\theta )'} }{ {1!} }(\theta  - \theta ' - \theta ) - \bar p(\theta )\\\\
 &=  - \theta '\frac{ {\partial \bar p} }{ {\partial \theta } }
\end{align} 
$$

公式 (28) 代入 $\overline{(\frac{p'}{\bar p})^2}$ ，并设 $\bar p(\theta)$ 和 $\bar \theta(p)$ 互为反函数 ($\frac{\partial \bar p }{\theta}=(\frac{\partial \bar \theta }{p})^{-1}$, 动力气象P145)

$$
\begin{align}
\overline { { {(\frac{ {p'} }{ {\bar p} })}^2} }  &= \frac{1}{ { { {\bar p}^2} } }\overline { { {(\theta '\frac{ {\partial \bar p} }{ {\partial \theta } })}^2} } \\\\
 &= \frac{1}{ { { {\bar p}^2} } }\overline { { {(\theta ')}^2}{ {(\frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 2} } } 
\end{align}
$$

将公式 (30) 代入公式 (23) ，(认为 $d\theta≈\frac{\partial \bar \theta}{\partial p}dp$, 动力气象P145) 得

$$
\begin{align}
\bar A &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }\frac{1}{ { { {\bar p}^2} } }\overline { { {(\frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 2} }{ {(\theta ')}^2} } d\theta } \\\\
 &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_{ {p_s} }^0 { { {\bar p}^{\frac{R}{ { {c_p} } } - 1} }{ {(\frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 2} }\overline { { {(\theta ')}^2} } \frac{ {\partial \bar \theta } }{ {\partial p} }dp} \\\\
 &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ {p_s} } { { {\bar \theta }^2}{ {\bar p}^{\frac{R}{ { {c_p} } } - 1} }\overline { { {(\frac{ {\theta '} }{ {\bar \theta } })}^2} } { {( - \frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 1} }dp} 
\end{align}
$$

### 位温对气压的偏微分

由于 $\theta=T(\frac{p_{0} }{p})^{\frac{R}{c_p} }$ 取对数

$$
\begin{align}
\ln \theta  = \ln T + \frac{R}{ { {c_p} } }\ln {p_0} - \frac{R}{ { {c_p} } }\ln p
\end{align}
$$

对 $p$ 求偏导

$$
\begin{align}
\frac{1}{\theta }\frac{ {\partial \theta } }{ {\partial p} } &= \frac{1}{T}\frac{ {\partial T} }{ {\partial p} } - \frac{R}{ { {c_p}p} }\\\\
\frac{ {\partial \theta } }{ {\partial p} } &= \frac{\theta }{T}\frac{ {\partial T} }{ {\partial p} } - \frac{R}{ { {c_p} } }\frac{\theta }{p}
\end{align}
$$

又

$$
\begin{align}
\frac{ {\partial T} }{ {\partial p} } &= \frac{ {\partial T} }{ {\partial z} }\frac{ {\partial z} }{ {\partial p} }\\\\
 &=  - \gamma ( - \frac{1}{ {\rho g} })\\\\
 &= \gamma \frac{1}{ {\rho g} }
\end{align}
$$

其中 $\gamma = -\frac{\partial T}{\partial z}$ 是温度递减率。将公式 (39) 代入公式 (36)

$$
\begin{align}
\frac{ {\partial \theta } }{ {\partial p} } &= \frac{\theta }{T}\gamma \frac{1}{ {\rho g} } - \frac{ {gR} }{ {g{c_p} } }\frac{\theta }{p}\\\\
 &= \frac{\theta }{ {T\rho g} }\gamma  - \frac{R}{g}\frac{\theta }{p}{\gamma _d}\\\\
 &= (\frac{\theta }{ {T\rho g} }\gamma  - \frac{R}{g}\frac{\theta }{p}{\gamma _d})\frac{ {\frac{g}{ { {c_p} } } } }{ { {\gamma _d} } }\\\\
 &= \frac{ {\frac{\theta }{p}\frac{R}{ { {c_p} } }(\frac{ {p\gamma } }{ {T\rho R} } - {\gamma _d})} }{ { {\gamma _d} } }\\\\(状态方程)
 &=  - \theta {p^{ - 1} }\frac{R}{ { {c_p} } }({\gamma _d} - \gamma ){\gamma _d}^{ - 1}
\end{align}
$$

其中 $\gamma_d = \frac{g}{c_p}$ 是干绝热减温率。做等压面平均得

$$
\begin{align}
\frac{ {\partial \bar \theta } }{ {\partial p} }= - \bar \theta {\bar p^{ - 1} }\frac{R}{ { {c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1}
\end{align}
$$

将公式 (45) 代入公式 (33)得

$$
\begin{align}
\bar A &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ + \infty } { { {\bar p}^{1 + \frac{R}{ { {c_p} } } } }\frac{1}{ { { {\bar p}^2} } }\overline { { {(\frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 2} }{ {(\theta ')}^2} } d\theta } \\\\
 &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_{ {p_s} }^0 { { {\bar p}^{\frac{R}{ { {c_p} } } - 1} }{ {(\frac{ {\partial \bar \theta } }{ {\partial p} })}^{ - 2} }\overline { { {(\theta ')}^2} } \frac{ {\partial \bar \theta } }{ {\partial p} }dp} \\\\
 &= \frac{1}{2}\frac{ { {c_p} } }{g}\frac{R}{ { {c_p} } }{p_0}^{ - \frac{R}{ { {c_p} } } }\int_0^{ {p_s} } { { {\bar \theta }^2}{ {\bar p}^{\frac{R}{ { {c_p} } } - 1} }\overline { { {(\frac{ {\theta '} }{ {\bar \theta } })}^2} } \frac{ {\bar p{\gamma _d} } }{ {\bar \theta \frac{R}{ { {c_p} } }({\gamma _d} - \bar \gamma )} }dp} \\\\
 &= \frac{1}{2}\int_0^{ {p_s} } {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }\overline { { {(\frac{ {\theta '} }{ {\bar \theta } })}^2} } dp} 
\end{align}
$$

将 $\theta=\bar \theta+\theta'$ 和 $T=\bar T+T'$ 代入公式 (34) 得

$$
\begin{align}
\ln (\bar \theta  + \theta ') &= \ln (\bar T + T') + \frac{R}{ { {c_p} } }(\ln {p_0} - \ln p)\\\\
\ln \bar \theta (1 + \frac{ {\theta '} }{ {\bar \theta } }) &= \ln \bar T(1 + \frac{ {T'} }{ {\bar T} }) + \frac{R}{ { {c_p} } }(\ln {p_0} - \ln p),(T',\theta ' \ll \bar T,\bar \theta )\\\\
\ln \bar \theta  &= \ln \bar T + \frac{R}{ { {c_p} } }(\ln {p_0} - \ln p)
\end{align}
$$

公式 (51) 减公式 (52)得 （大气动力学P128）:

<div style="page-break-after: always;"></div>

$$
\begin{align}
\ln (1 + \frac{ {\theta '} }{ {\bar \theta } }) &= \ln (1 + \frac{ {T'} }{ {\bar T} }),(\frac{ {T'} }{ {\bar T} },\frac{ {\theta '} }{ {\bar \theta } } \ll 1)\\\\
 \Rightarrow \frac{ {\theta '} }{ {\bar \theta } } &= \frac{ {T'} }{ {\bar T} }
\end{align}
$$

将公式 (54) 代入公式 (49) 得

$$
\begin{align}
\bar A &= \frac{1}{2}\int_0^{ {p_s} } {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }\overline { { {(\frac{ {T'} }{ {\bar T} })}^2} } dp} 
\end{align}
$$

## 有效位能倾向

由熵形式热力学方程 (大气动力学P10)：

$$
\begin{align}
{c_p}T\frac{ {d\ln \theta } }{ {dt} } &= Q\\\\
\frac{ {d\ln (\bar \theta  + \theta ')} }{ {dt} } &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }\\\\
\frac{ {d\ln \bar \theta (1 + \frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }\\\\
\frac{ {d\ln \bar \theta } }{ {dt} } + \frac{ {d\ln (1 + \frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }\\\\
\frac{ {d(\frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } + \omega \frac{ {\partial \ln \bar \theta } }{ {\partial p} } &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }
\end{align}
$$

其中 $Q=\bar Q + Q'$ 是单位质量空气在单位时间内从外界得到的能量，包括分子热传导、辐射、相变等方式。 $\bar Q，Q'$ 分别是 $Q$ 在等压面上的均值和偏差。另外 $\frac{\theta'}{\bar \theta}\ll 1$， $\bar \theta$ 只于垂直坐标有关。$ T' \ll \bar T$

由公式 (40)-(44)知，公式 (60) 可进一步变化为

$$
\begin{align}
\frac{ {d(\frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } + \frac{\omega }{ {\bar \theta } }\frac{ {\partial \bar \theta } }{ {\partial p} } &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }\\\\
\frac{ {d(\frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } + \frac{\omega }{ {\bar \theta } }( - \bar \theta {p^{ - 1} }\frac{R}{ { {c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1}) &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }\\\\
\frac{ {d(\frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } - \omega \frac{R}{ {p{c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1} &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} }
\end{align}
$$

对公式 (60) 两边同乘 $\bar T (\gamma_d-\bar \gamma)^{-1}\frac{\theta'}{\bar \theta}$ 

$$
\begin{align}
\bar T{({\gamma _d} - \bar \gamma )^{ - 1} }\frac{ {\theta '} }{ {\bar \theta } } \cdot \frac{ {d(\frac{ {\theta '} }{ {\bar \theta } })} }{ {dt} } - \bar T{({\gamma _d} - \bar \gamma )^{ - 1} }\frac{ {\theta '} }{ {\bar \theta } } \cdot \omega \frac{R}{ {p{c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1} &= \frac{ {\bar Q + Q'} }{ { {c_p}\bar T} } \cdot \bar T{({\gamma _d} - \bar \gamma )^{ - 1} }\frac{ {\theta '} }{ {\bar \theta } }\\\\
\frac{1}{2}\bar T{({\gamma _d} - \bar \gamma )^{ - 1} }\frac{ {d{ {(\frac{ {\theta '} }{ {\bar \theta } })}^2} } }{ {dt} } - \bar T\frac{ {\theta '} }{ {\bar \theta } }\omega \frac{R}{ {p{c_p} } }{\gamma _d}^{ - 1} &= \frac{ {\bar Q + Q'} }{ { {c_p} } }{({\gamma _d} - \bar \gamma )^{ - 1} }\frac{ {\theta '} }{ {\bar \theta } }\\\\
\frac{ {dA} }{ {dt} } - \int_0^{ps} {\bar T\frac{ {T'} }{ {\bar T} }\omega \frac{R}{ {p{c_p} } }\frac{ { {c_p} } }{g} } dp &= \int_0^{ps} {\frac{ {\bar Q + Q'} }{ { {c_p} } }{ {({\gamma _d} - \bar \gamma )}^{ - 1} }\frac{ {T'} }{ {\bar T} } } dp\\\\
\frac{ {dA} }{ {dt} } = \int_0^{ps} {T'\omega \frac{R}{ {pg} } } dp + \int_0^{ps} {\frac{ {(\bar Q + Q')T'} }{ { {c_p}\bar T} }{ {({\gamma _d} - \bar \gamma )}^{ - 1} } } dp\\\\
\frac{ {\partial \bar A} }{ {\partial t} } = \int_0^{ps} {\overline {T\omega } \frac{R}{ {pg} } } dp + \int_0^{ps} {\frac{ {\overline {Q'T'} } }{ { {c_p}\bar T} }{ {({\gamma _d} - \bar \gamma )}^{ - 1} } } dp\\\\
\frac{ {\partial \bar A} }{ {\partial t} } = \frac{R}{g}\int_0^{ps} { {p^{ - 1} }\overline {T\omega } } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp
\end{align}
$$

> 在公式 (65) 到 (66) 的步骤中，等号左边 $\bar T$ 是与垂直坐标有关的，因此严格得来说不能直接放入微分号内凑出 $A$。
> 
> 在公式 (67) 到 (68) 的步骤中，等号左边的平流项先转为通量与散度的和的形式，通量在全球积分中为0，散度通过连续方程消去。`在等号右边第一项` $T'\omega$ `本应在水平平均中消去，Lorenz的文章中最终形式是` $\overline{T\omega}$ 。`不知如何处理`

因此全球积分的有效位能随时间倾向为

<div style="page-break-after: always;"></div>

$$
\begin{align}
\frac{ {\partial \bar A} }{ {\partial t} } &= \frac{R}{g}\int_0^{ps} { {p^{ - 1} }\overline {T\omega } } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp\\\\(状态方程)
 &= {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp\\\\
 &= \int_0^{ps} {\overline {V \cdot \nabla z} } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp
\end{align}
$$

公式 (72) 就是Lorenz 文章中的有效位能倾向方程。公式 (71) 到公式 (72)有点难理解，但可以反过来推导：

$$
\begin{align}
\int_0^{ps} {\overline {V \cdot \nabla z} } dp &= \int_0^{ps} {\overline {\nabla Vz} }  - \overline {z\nabla V} dp\\\\
 &=  - \int_0^{ps} {\overline {z\nabla V} } dp\\\\(连续方程)
 &= \int_0^{ps} {\overline {z\frac{ {\partial \omega } }{ {\partial p} } } } dp\\\\
 &= \int_0^{ps} {\overline z } d\omega \\\\
 &= [\overline {z\omega } ]_0^{ps} - \int_0^{ps} {\overline \omega  } dz\\\\(静力平衡)
 &=  - \int_0^{ps} {\overline {\omega \frac{1}{ { - \rho g} } } } dp\\\\
 &= {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp
\end{align}
$$

## 纬向平均与扰动有效位能

将物理量分解为纬向平均 (用 $[m]$ 表示) 与纬向偏差 (用 $m^*$ 表示) 

$$
\begin{align}
u &= [u] + u^* \\\\
v &= [v] + v^* \\\\
\omega  &= [\omega ] + \omega ^* \\\\
\theta '&= [\theta '] + \theta '^* \\\\
T '&= [T '] + T '^* \\\\
Q '&= [Q '] + Q '^*
\end{align}
$$

热力学量 $\theta$ 在前文已经分解为 $\bar \theta + \theta'$ 。其中 $\bar \theta$ 表示水平平均。将公式 (84) 代入公式 (55) (不做水平积分平均)

$$
\begin{align}
A=\frac{1}{2}\int_0^{ps} {\bar T{ { ( {\gamma_d} - \bar \gamma ) }^{ - 1} }\frac{ { { {[T']}^2} + 2[T']{ {T'}^* } + { { ( { {T'}^* } ) }^2} } }{ { { {\bar T}^2} } } } dp
\end{align}
$$

对方程纬向平均

$$
\begin{align}
[A] &= \frac{1}{2}\int_0^{ps} {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }\frac{ {[{ {T'}^2}] + [{ {({ {T'}^* })}^2}]} }{ { { {\bar T}^2} } } } dp \\\\
 &= \frac{1}{2}\int_0^{ps} {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {(\frac{ {[T']} }{ {\bar T} })}^2} } dp + \frac{1}{2}\int_0^{ps} {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }[{ {(\frac{ { { {T'}^* } } }{ {\bar T} })}^2}]} dp \\\\
 &= { { A}_m} + { { A}_p}
\end{align}
$$

即`有效位能沿纬圈的平均值` $[A]$ 可以分解为`基本气流的有效位能`也称平均有效位能 $A_m$ 与 `空气扰动的有效位能`也称扰动有效位能 $ A_p$ 。

> 学术研究中似乎并不是将`有效位能纬圈的平均值` 进行分解，而是分解`有效位能`。如果公式 (85) 到 (86) 不进行纬圈平均。那么`有效位能` 同样可以分解为 `平均有效位能` 和 `扰动有效位能`，但会多出一项 $[T']T'^*$ 。所以学术研究中一般是将这一项忽略掉？ 

## 纬向平均与扰动有效位能倾向

将公式 (80)-(85) 代入公式 (63)

$$
\begin{align}
\frac{ {\partial (\frac{ {[\theta '] + { {\theta '}^* } } }{ {\bar \theta } })} }{ {\partial t} } + ([u] + {u^* })\frac{ {\partial (\frac{ {[\theta '] + { {\theta '}^* } } }{ {\bar \theta } })} }{ {\partial x} } + ([v] + {v^* })\frac{ {\partial (\frac{ {[\theta '] + { {\theta '}^* } } }{ {\bar \theta } })} }{ {\partial y} } +... \\\\
 ...+ ([\omega ] + {\omega ^* })\frac{ {\partial (\frac{ {[\theta '] + { {\theta '}^* } } }{ {\bar \theta } })} }{ {\partial p} } - ([\omega ] + {\omega ^* })\frac{R}{ {p{c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1} = \frac{ {\bar Q + [Q'] + { {Q'}^* } } }{ { {c_p}\bar T} }
\end{align}
$$

利用连续方程将 $\frac{\partial}{\partial x}$ $\frac{\partial}{\partial y}$, $\frac{\partial}{\partial p}$ 项写为通量减散度的形式，利用连续方程消去散度项, 并对方程纬向平均

<div style="page-break-after: always;"></div>

$$
\begin{align}
\frac{ {\partial (\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial t} } + \frac{ {\partial ([v]\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial y} } + \frac{ {\partial ([{v^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial y} } + ...\\\\
... + \frac{ {\partial ([\omega ]\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial p} } + \frac{ {\partial ([{\omega ^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial p} } - [\omega ]\frac{R}{ {p{c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1} = \frac{ {\bar Q + [Q']} }{ { {c_p}\bar T} }
\end{align}
$$

方程两边同乘 $\frac{\bar T}{\gamma_d-\gamma} \frac{[\theta']}{\bar \theta}$ 。

$$
\begin{align}
\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial (\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial t} } + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([v]\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial y} } + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([{v^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial y} } + ...\\\\
... + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([\omega ]\frac{ {[\theta ']} }{ {\bar \theta } })} }{ {\partial p} } + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([{\omega ^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial p} } + ...\\\\
... - \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }[\omega ]\frac{R}{ {p{c_p} } }({\gamma _d} - \bar \gamma ){\gamma _d}^{ - 1} = \frac{ {\bar Q + [Q']} }{ { {c_p}\bar T} }\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }
\end{align}
$$

整理且代入公式 (54) $\frac{ {\theta '} }{ {\bar \theta } } = \frac{ {T'} }{ {\bar T} }$

$$
\begin{align}
\frac{ {\partial (\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial t} } + \frac{ {\partial ([v]\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial y} } + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([{v^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial y} } + ...\\\\
... + \frac{ {\partial ([\omega ]\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial p} } + \frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ {\bar \theta } }\frac{ {\partial ([{\omega ^* }\frac{ { { {\theta '}^* } } }{ {\bar \theta } }])} }{ {\partial p} } + ...\\\\
... - [T'][\omega ]\frac{R}{ {pg} } = \frac{ {(\bar Q + [Q'])[\theta ']} }{ { {c_p}\bar \theta} }\frac{1}{ { {\gamma _d} - \gamma } }
\end{align}
$$

将上式第三项和第五项写为通量减散度的形式, 且代入公式 (54) $\frac{ {\theta '} }{ {\bar \theta } } = \frac{ {T'} }{ {\bar T} }$

$$
\begin{align}
\frac{ {\partial (\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial t} } + \frac{ {\partial ([v]\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial y} } + \frac{ {\partial (\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ { { {\bar \theta }^2} } }[{v^* }{ {\theta '}^* }])} }{ {\partial y} } - [{v^* }{ {\theta '}^* }]\frac{ {\partial (\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ { { {\bar \theta }^2} } })} }{ {\partial y} } + ...\\\\
... + \frac{ {\partial ([\omega ]\frac{1}{2}\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }{ {(\frac{ {[\theta ']} }{ {\bar \theta } })}^2})} }{ {\partial p} } + \frac{ {\partial (\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ { { {\bar \theta }^2} } }[{\omega ^* }{ {\theta '}^* }])} }{ {\partial p} } - [{\omega ^* }{ {\theta '}^* }]\frac{ {\partial (\frac{ {\bar T} }{ { {\gamma _d} - \gamma } }\frac{ {[\theta ']} }{ { { {\bar \theta }^2} } })} }{ {\partial p} } + ...\\\\
... - [T'][\omega ]\frac{R}{ {pg} } = \frac{ {(\bar Q + [Q'])[T']} }{ { {c_p}\bar T} }\frac{1}{ { {\gamma _d} - \gamma } }
\end{align}
$$

$\int_0^{ps}{dp}$ 垂直积分且水平积分(平均)得

$$
\begin{align}
\frac{ {\partial { {\bar A}_m} } }{ {\partial t} } - \int_0^{ps} {\overline {\frac{ {\bar T[{v^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial y} } } } dp - \int_0^{ps} {\overline {\frac{ {\bar T[{\omega ^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial p} } } } dp - \int_0^{ps} {\overline {\frac{R}{ {pg} }[T][\omega ]} } dp = \int_0^{ps} {\overline {\frac{ {[Q'][T']} }{ { {c_p}\bar T} }\frac{1}{ { {\gamma _d} - \bar \gamma } } } } dp\\\\
\frac{ {\partial { {\bar A}_m} } }{ {\partial t} } = \int_0^{ps} {\overline {\frac{ {\bar T[{v^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial y} } } } dp + \int_0^{ps} {\overline {\frac{ {\bar T[{\omega ^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial p} } } } dp + \int_0^{ps} {\overline {\frac{R}{ {pg} }[T][\omega ]} } dp + \int_0^{ps} {\overline {\frac{ {[Q'][T']} }{ { {c_p}\bar T} }\frac{1}{ { {\gamma _d} - \bar \gamma } } } } dp
\end{align}
$$

> 上式的 $[T'][\omega]$ 在Lorenz的文章中写为 $[T][\omega]$。也不知道是哪里出了问题，还是用了什么近似。

将公式 (80)-(85) 代入公式 (70) （不做水平积分)

$$
\begin{align}
\frac{ {\partial A} }{ {\partial t} } = \int_0^{ps} {\frac{R}{ {gp} } } ([T] + {T^* })([\omega ] + {\omega ^* })dp + ...\\\\
... + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }([Q'] + { {Q'}^* })([T'] + { {T'}^* })}dp 
\end{align}
$$

纬向平均结合公式 (89) 得

$$
\begin{align}
\frac{ {\partial [A]} }{ {\partial t} } &= \int_0^{ps} {\frac{R}{ {gp} } } ([T][\omega ] + [{T^* }{\omega ^* }])dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }([Q'][T'] + [{ {Q'}^* }{ {T'}^* }])} dp\\\\
\frac{ {\partial {A_m} } }{ {\partial t} } + \frac{ {\partial {A_p} } }{ {\partial t} } &= \int_0^{ps} {\frac{R}{ {gp} } } ([T][\omega ] + [{T^* }{\omega ^* }])dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }([Q'][T'] + [{ {Q'}^* }{ {T'}^* }])} dp
\end{align}
$$

用公式 (108) 减公式 (104) (公式104做了全球平均，即使不做全球平均，相减后再平均也能消去通量项)

$$
\begin{align}
\frac{ {\partial { {\bar A}_p} } }{ {\partial t} } =  - \int_0^{ps} {\overline {\frac{ {\bar T[{v^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \overline \gamma  ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial y} } } } dp - \int_0^{ps} {\overline {\frac{ {\bar T[{\omega ^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \overline \gamma  ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial p} } } } dp + ...\\\\
... + \int_0^{ps} {\overline {\frac{R}{ {pg} }[{T^* }{\omega ^* }]} } dp + {g^{ - 1} }\int_0^{ps} {\overline { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }[{ {Q'}^* }{ {T'}^* }]} } dp
\end{align}
$$

## 有效位能小节

- 有效位能表达式（同公式55）

$$
\begin{align}
\bar A &= \frac{1}{2}\int_0^{ {p_s} } {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }\overline { { {(\frac{ {T'} }{ {\bar T} })}^2} } dp} 
\end{align}
$$

- 有效位能时间倾向（同公式70-72）

$$
\begin{align}
\frac{ {\partial \bar A} }{ {\partial t} } &= \frac{R}{g}\int_0^{ps} { {p^{ - 1} }\overline {T\omega } } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp\\\\
 &= {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp\\\\
 &= \int_0^{ps} {\overline {V \cdot \nabla z} } dp + {g^{ - 1} }\int_0^{ps} { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }\overline {Q'T'} } dp
\end{align}
$$

- 纬向平均有效位能和扰动有效位能（同公式88）

$$
\begin{align}
{ { A}_m} = \frac{1}{2}\int_0^{ps} {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {(\frac{ {[T']} }{ {\bar T} })}^2} } dp\\\\
{ { A}_p} = \frac{1}{2}\int_0^{ps} {\bar T{ {({\gamma _d} - \bar \gamma )}^{ - 1} }[{ {(\frac{ { { {T'}^* } } }{ {\bar T} })}^2}]} dp
\end{align}
$$

- 纬向平均有效位能和扰动有效位能时间倾向 （同公式104、109）

$$
\begin{align}
\frac{ {\partial { {\bar A}_m} } }{ {\partial t} } = \int_0^{ps} {\overline {\frac{ {\bar T[{v^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial y} } } } dp + \int_0^{ps} {\overline {\frac{ {\bar T[{\omega ^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial p} } } } dp + ...\\\\
... + \int_0^{ps} {\overline {\frac{R}{ {pg} }[T][\omega ]} } dp + {g^{ - 1} }\int_0^{ps} {\overline { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }[Q'][T']} } dp\\\\
\frac{ {\partial { {\bar A}_p} } }{ {\partial t} } =  - \int_0^{ps} {\overline {\frac{ {\bar T[{v^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial y} } } } dp - \int_0^{ps} {\overline {\frac{ {\bar T[{\omega ^* }{ {\theta '}^* }]} }{ {({\gamma _d} - \bar \gamma ){ {\bar \theta }^2} } }\frac{ {\partial ([\theta '])} }{ {\partial p} } } } dp + ...\\\\
... + \int_0^{ps} {\overline {\frac{R}{ {pg} }[{T^* }{\omega ^* }]} } dp + {g^{ - 1} }\int_0^{ps} {\overline { {\gamma _d}{ {({\gamma _d} - \bar \gamma )}^{ - 1} }{ {\bar T}^{ - 1} }[{ {Q'}^* }{ {T'}^* }]} } dp
\end{align}
$$

> 上式与大气动力学P469等价

---

# 动能的定义

在某个气压层上单位质量空气的动能是

$$
\begin{align}
K = \frac{1}{2}({u^2} + {v^2}) = \frac{1}{2}{\vec V^2}
\end{align}
$$

对于单位面积上整层大气的动能为

$$
\begin{align}
K &= \int_0^{ + \infty } {\frac{1}{2}\rho { {\vec V}^2} } dz\\\\
 &= \int_{ps}^0 {\frac{1}{2}\rho { {\vec V}^2} } ( - \frac{1}{ {\rho g} })dp\\\\
 &= \frac{1}{2}{g^{ - 1} }\int_0^{ps} { { {\vec V}^2} } dp
\end{align}
$$

对于全球积分(平均)的动能为 $\bar K= \frac{1}{2}{g^{ - 1} }\int_0^{ps} \overline { { {\vec V}^2} } dp$ 

## 动能时间倾向

对于二维动量方程

$$
\begin{align}
\frac{ {d\vec V} }{ {dt} } + \omega \frac{ {\partial \vec V} }{ {\partial p} } =  - f\vec k \times \vec V - \nabla \Phi  + \vec F
\end{align}
$$

其中 $\frac{d}{dt}=\frac{\partial}{\partial t}+u\frac{\partial}{\partial x}+v\frac{\partial}{\partial y}$ ，$f$ 是科氏参数，$\vec F$ 是水平摩擦力，$\phi$ 是位势

对公式 (125) 两边同乘 $\frac{1}{g}\vec V$ , 结合连续方程有

<div style="page-break-after: always;"></div>

$$
\begin{align}
\frac{1}{g}\vec V\frac{ {d\vec V} }{ {dt} } + \frac{1}{g}\vec V\omega \frac{ {\partial \vec V} }{ {\partial p} } = \frac{1}{g}\vec V \cdot ( - f\vec k \times \vec V) - \frac{1}{g}\vec V \cdot \nabla \Phi  + \frac{1}{g}\vec V \cdot \vec F\\\\
\frac{1}{g}\vec V\frac{ {\partial \vec V} }{ {\partial t} } + \frac{1}{g}\vec Vu\frac{ {\partial \vec V} }{ {\partial x} } + \frac{1}{g}\vec Vv\frac{ {\partial \vec V} }{ {\partial y} } + \frac{1}{g}\vec V\omega \frac{ {\partial \vec V} }{ {\partial p} } &=  - \frac{1}{g}\vec V \cdot \nabla \Phi  + \frac{1}{g}\vec V \cdot \vec F\\\\
\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial t} } + u\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial x} } + v\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial y} } + \omega \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial p} } &=  - \frac{1}{g}\vec V \cdot \nabla \Phi  + \frac{1}{g}\vec V \cdot \vec F\\\\
\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial t} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}u} }{ {\partial x} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}v} }{ {\partial y} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}\omega } }{ {\partial p} } - \frac{1}{ {2g} }{ {\vec V}^2}(\frac{ {\partial u} }{ {\partial x} } + \frac{ {\partial v} }{ {\partial y} } + \frac{ {\partial \omega } }{ {\partial p} }) &=  - \frac{1}{g}\vec V \cdot \nabla \Phi  + \frac{1}{g}\vec V \cdot \vec F\\\\
\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial t} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}u} }{ {\partial x} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}v} }{ {\partial y} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}\omega } }{ {\partial p} } &=  - \frac{1}{g}\nabla (\vec V\Phi ) + \frac{1}{g}\Phi \nabla  \cdot \vec V + \frac{1}{g}\vec V \cdot \vec F\\\\
\frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2} } }{ {\partial t} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}u} }{ {\partial x} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}v} }{ {\partial y} } + \frac{ {\partial \frac{1}{ {2g} }{ {\vec V}^2}\omega } }{ {\partial p} } &=  - \frac{1}{g}\nabla (\vec V\Phi ) - \frac{1}{g}\Phi \frac{ {\partial \omega } }{ {\partial p} } + \frac{1}{g}\vec V \cdot \vec F
\end{align}
$$

对公式 (131)做全球积分

$$
\begin{align}
\frac{ {\partial \bar K} }{ {\partial t} } &=  - \int_0^{ps} {\frac{1}{g}\nabla (\vec V\Phi )} dp - \int_0^{ps} {\frac{1}{g}\Phi \frac{ {\partial \omega } }{ {\partial p} } } dp + \int_0^{ps} {\frac{1}{g}\vec V \cdot \vec F} dp\\\\
\frac{ {\partial \bar K} }{ {\partial t} } &=  - \int_0^{ps} {\frac{1}{g}\Phi \frac{ {\partial \omega } }{ {\partial p} } } dp + \int_0^{ps} {\frac{1}{g}\vec V \cdot \vec F} dp\\\\
\frac{ {\partial \bar K} }{ {\partial t} } &=  - \frac{1}{g}\int_0^{ps} {\frac{ {\partial \omega \Phi } }{ {\partial p} }dp + \frac{1}{g}\int_0^{ps} {\omega \frac{ {\partial \Phi } }{ {\partial p} } } } dp + \int_0^{ps} {\frac{1}{g}\vec V \cdot \vec F} dp\\\\
\frac{ {\partial \bar K} }{ {\partial t} } &= \frac{1}{g}\int_0^{ps} {\omega \frac{1}{ { - \rho } } } dp + \int_0^{ps} {\frac{1}{g}\vec V \cdot \vec F} dp\\\\
\frac{ {\partial \bar K} }{ {\partial t} } &=  - {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp
\end{align}
$$

> 在公式 (69) 中将 $T'$ 换为了 $T$ 。如果不换的话就不能与动能倾向公式 (136) 相对应，有点难理解。公式 (69) 的推导过程可能还存在一些问题

即动能时间倾向为 (类比公式 (70)-(79))

$$
\begin{align}
\frac{ {\partial \bar K} }{ {\partial t} } &=  - {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp\\\\
 &= -\frac{R}{g}\int_0^{ps} { {p^{ - 1} }\overline {T\omega } } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp\\\\
 &= -\int_0^{ps} {\overline {V \cdot \nabla z} } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp
\end{align}
$$

## 纬向平均与扰动动能定义

将公式 (80) 和 (81) 代入公式 (124)，并纬向平均

$$
\begin{align}
K &= \frac{1}{2}{g^{ - 1} }\int_0^{ps} { { {[\vec V]}^2} + 2[\vec V] \cdot { {\vec V}^* } + { {\vec V}^* }^2} dp\\\\
(纬向平均)[K] &= \frac{1}{2}{g^{ - 1} }\int_0^{ps} { { {[\vec V]}^2} } dp + \frac{1}{2}{g^{ - 1} }\int_0^{ps} {[{ {\vec V}^* }^2]} dp\\\\
 &= {K_m} + {K_p}
\end{align}
$$

即`动能沿纬圈的平均值` $[K]$ 可以分解为`基本气流的动能`也称平均动能 $K_m$ 与 `空气扰动的动能`也称扰动动能  $K_p$ 。其中

$[\vec V]^2=[u]^2+[v]^2 $，$[\vec V^* ]^2=[{u^{* } }^2+{v^* }^2]$ 

## 纬向平均与扰动动能倾向

将公式 (125) 写为通量减散度的形式，并代入连续方程化简

$$
\begin{align}
\frac{ {\partial \vec V} }{ {\partial t} } + \frac{ {\partial \vec Vu} }{ {\partial x} } + \frac{ {\partial \vec Vv} }{ {\partial y} } + \frac{ {\partial \vec V\omega } }{ {\partial p} } - \vec V \cdot (\frac{ {\partial u} }{ {\partial x} } + \frac{ {\partial v} }{ {\partial y} } + \frac{ {\partial \omega } }{ {\partial p} }) =  - f\vec k \times \vec V - \nabla \Phi  + \vec F\\\\
\frac{ {\partial \vec V} }{ {\partial t} } + \frac{ {\partial \vec Vu} }{ {\partial x} } + \frac{ {\partial \vec Vv} }{ {\partial y} } + \frac{ {\partial \vec V\omega } }{ {\partial p} } =  - f\vec k \times \vec V - \nabla \Phi  + \vec F
\end{align}
$$

将公式 (80)-(82) 以及 $\Phi=[\Phi]+\Phi^* $，$\vec F=[\vec F]+\vec F^* $  代入公式 (144)

<div style="page-break-after: always;"></div>

$$
\begin{align}
\frac{ {\partial [\vec V] + { {\vec V}^* } } }{ {\partial t} } + \frac{ {\partial ([\vec V] + { {\vec V}^* })([u] + {u^* })} }{ {\partial x} } + \frac{ {\partial ([\vec V] + { {\vec V}^* })([v] + {v^* })} }{ {\partial y} } + ...\\\\
... + \frac{ {\partial ([\vec V] + { {\vec V}^* })([\omega ] + {\omega ^* })} }{ {\partial p} } =  - f\vec k \times ([\vec V] + { {\vec V}^* }) - \nabla ([\Phi ] + {\Phi ^* }) + [\vec F] + { {\vec F}^* }
\end{align}
$$

纬向平均得

$$
\begin{align}
\frac{ {\partial [\vec V]} }{ {\partial t} } + \frac{ {\partial [\vec V][v]} }{ {\partial y} } + \frac{ {\partial [\vec V][\omega ]} }{ {\partial p} } + ...\\\\
... + \frac{ {\partial [{ {\vec V}^* }{v^* }]} }{ {\partial y} } + \frac{ {\partial [{ {\vec V}^* }{\omega ^* }]} }{ {\partial p} } =  - f\vec k \times [\vec V] - \nabla [\Phi ] + [\vec F]
\end{align}
$$

方程两边同乘 $\frac{1}{g}[\vec V]$ 

$$
\begin{align}
\frac{1}{g}[\vec V]\frac{ {\partial [\vec V]} }{ {\partial t} } +  + \frac{1}{g}[\vec V]\frac{ {\partial [\vec V][v]} }{ {\partial y} } + \frac{1}{g}[\vec V]\frac{ {\partial [\vec V][\omega ]} }{ {\partial p} } + ...\\\\
... + \frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{v^* }]} }{ {\partial y} } + \frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{\omega ^* }]} }{ {\partial p} } = \frac{1}{g}[\vec V]( - f\vec k \times [\vec V]) + ...\\\\
... - \frac{1}{g}[\vec V] \cdot \nabla [\Phi ] + \frac{1}{g}[\vec V][\vec F]\\\\
\frac{ {\partial \frac{1}{ {2g} }{ {[\vec V]}^2} } }{ {\partial t} } + \frac{ {\partial \frac{1}{ {2g} }{ {[\vec V]}^2}[v]} }{ {\partial y} } + \frac{ {\partial \frac{1}{ {2g} }{ {[\vec V]}^2}[\omega ]} }{ {\partial p} } + ...\\\\
... + \frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{v^* }]} }{ {\partial y} } + \frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{\omega ^* }]} }{ {\partial p} } =  - \frac{1}{g}[\vec V] \cdot \nabla [\Phi ] + \frac{1}{g}[\vec V][\vec F]
\end{align}
$$

公式 (152) 中 $[\vec V]$ 放进了 $\frac{\partial}{\partial x}$，$\frac{\partial}{\partial y}$ 内部。结合连续方程，这步是正确的。

对公式 (152)-(153) 全球积分

$$
\begin{align}
\frac{ {\partial \bar K_m} }{ {\partial t} } + \int_0^{ps} {\overline {\frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{v^* }]} }{ {\partial y} } } } dp + \int_0^{ps} {\overline {\frac{1}{g}[\vec V]\frac{ {\partial [{ {\vec V}^* }{\omega ^* }]} }{ {\partial p} } } } dp =  - \frac{1}{g}\int_0^{ps} {\overline {[\vec V] \cdot \nabla [\Phi ]} } dp + \frac{1}{g}\int_0^{ps} {\overline {[\vec V][\vec F]} } dp\\\\
\frac{ {\partial \bar K_m} }{ {\partial t} } - \frac{1}{g}\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp - \frac{1}{g}\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp =  - \frac{1}{g}\int_0^{ps} {\overline {[\vec V] \cdot \nabla [\Phi ]} } dp + \frac{1}{g}\int_0^{ps} {\overline {[\vec V][\vec F]} } dp\\\\
\frac{ {\partial \bar K_m} }{ {\partial t} } = \frac{1}{g}\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp + \frac{1}{g}\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - \frac{1}{g}\int_0^{ps} {\overline {[\vec V] \cdot \nabla [\Phi ]} } dp + \frac{1}{g}\int_0^{ps} {\overline {[\vec V][\vec F]} } dp
\end{align}
$$

> 公式 (154) 的平流部分写成了通量减散度形式，结合连续方程得到公式 (155)

公式 (156) 右边第三项参考 公式 (132)-(136) 过程进行化简，得到纬向平均动能时间倾向方程

$$
\begin{align}
\frac{ {\partial { {\bar K}_m} } }{ {\partial t} } = {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp + {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - {g^{ - 1} }\int_0^{ps} {\overline {[\omega ][\alpha ]} } dp + {g^{ - 1} }\int_0^{ps} {\overline {[\vec V][\vec F]} } dp\\\\
 = {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp + {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - \int_0^{ps} {\frac{R}{ {pg} }\overline {[T][\omega ]} } dp + {g^{ - 1} }\int_0^{ps} {\overline {[\vec V][\vec F]} } dp
\end{align}
$$

对于公式 (138) 做水平平均之前，用 $T=[T]+T^* $，$\vec F=[\vec F]+\vec F^* $ ，$\vec V=[\vec V]+\vec V^* $，$\omega=[\omega]+\omega^* $ 代入 (之后再水平平均仍能消去通量项), 结合公式 (142)

$$
\begin{align}
\frac{ {\partial K} }{ {\partial t} } =  - \frac{R}{g}\int_0^{ps} { {p^{ - 1} }([T] + {T^* })([\omega ] + {\omega ^* })} dp + {g^{ - 1} }\int_0^{ps} {([\vec V] + { {\vec V}^* })([\vec F] + { {\vec F}^* })} dp\\\\(纬向平均)
\frac{ {\partial [K]} }{ {\partial t} } =  - \frac{R}{g}\int_0^{ps} { {p^{ - 1} }([T][\omega ] + [{T^* }{\omega ^* }])} dp + {g^{ - 1} }\int_0^{ps} {([\vec V][\vec F] + [{ {\vec V}^* }{ {\vec F}^* }])} dp\\\\
\frac{ {\partial {K_m} } }{ {\partial t} } + \frac{ {\partial {K_p} } }{ {\partial t} } =  - \frac{R}{g}\int_0^{ps} { {p^{ - 1} }([T][\omega ] + [{T^* }{\omega ^* }])} dp + {g^{ - 1} }\int_0^{ps} {([\vec V][\vec F] + [{ {\vec V}^* }{ {\vec F}^* }])} dp\\\\(水平平均)
\frac{ {\partial { {\bar K}_m} } }{ {\partial t} } + \frac{ {\partial { {\bar K}_p} } }{ {\partial t} } =  - \frac{R}{g}\int_0^{ps} { {p^{ - 1} }(\overline {[T][\omega ]}  + \overline {[{T^* }{\omega ^* }]} )} dp + {g^{ - 1} }\int_0^{ps} {(\overline {[\vec V][\vec F]}  + \overline {[{ {\vec V}^* }{ {\vec F}^* }]} )} dp
\end{align}
$$

用公式 (162) 减公式 (156)得扰动动能时间倾向方程

$$
\begin{align}
\frac{ {\partial { {\bar K}_p} } }{ {\partial t} } =  - {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp - {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - \int_0^{ps} {\frac{R}{ {pg} }\overline {[{T^* }{\omega ^* }]} } dp + {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{ {\vec F}^* }]} } dp
\end{align}
$$

## 动能小节

- 动能表达式 (同公式124)

$$
\begin{align}
\bar K = \frac{1}{2}{g^{ - 1} }\int_0^{ps} \overline { { {\vec V}^2} } dp
\end{align}
$$

- 有效位能时间倾向 (同公式137-139)

$$
\begin{align}
\frac{ {\partial \bar K} }{ {\partial t} } &=  - {g^{ - 1} }\int_0^{ps} {\overline {\omega \alpha } } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp\\\\
 &= -\frac{R}{g}\int_0^{ps} { {p^{ - 1} }\overline {T\omega } } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp\\\\
 &= -\int_0^{ps} {\overline {V \cdot \nabla z} } dp + {g^{ - 1} }\int_0^{ps} {\overline {\vec V \cdot \vec F} } dp
\end{align}
$$

- 纬向平均动能和扰动动能 (同公式141-142)

$$
\begin{align}
 {K_m} = \frac{1}{2}{g^{ - 1} }\int_0^{ps} { { {[\vec V]}^2} } dp\\\\
 {K_p} = \frac{1}{2}{g^{ - 1} }\int_0^{ps} {[{ {\vec V}^* }^2]} dp
\end{align}
$$

- 纬向平均动能和扰动动能时间倾向 (公式158、163)

$$
\begin{align}
\frac{ {\partial { {\bar K}_m} } }{ {\partial t} } &= {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp + {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - \int_0^{ps} {\frac{R}{ {pg} }\overline {[T][\omega ]} } dp + {g^{ - 1} }\int_0^{ps} {\overline {[\vec V][\vec F]} } dp\\\\
\frac{ {\partial { {\bar K}_p} } }{ {\partial t} } &=  - {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{v^* }]\frac{ {\partial [\vec V]} }{ {\partial y} } } } dp - {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{\omega ^* }]\frac{ {\partial [\vec V]} }{ {\partial p} } } } dp - \int_0^{ps} {\frac{R}{ {pg} }\overline {[{T^* }{\omega ^* }]} } dp + {g^{ - 1} }\int_0^{ps} {\overline {[{ {\vec V}^* }{ {\vec F}^* }]} } dp
\end{align}
$$
