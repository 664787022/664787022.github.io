---
title: EP通量、能量与eddy通量关系推导
date: 2023-05-09 11:07:40
tags: 大气理论
categories: 大气数学理论
cover: /img/cover13.jpg
---

[TOC]

# 前言

Eliassem-Palm，1961第二章能量通量与eddy通量关系推导整理

参考文献：

1. Eliassen & Palm. On the transfer of energy in stationary mountain waves. *Geofys. Publ.* (1961).



# 扰动方程组

由原始方程组 (绝热、静力平衡、无摩擦)
$$
\begin{align}
&\frac{ {du} }{ {dt} } =  - \frac{ {\partial \phi } }{ {\partial x} } + fv\\\\
&\frac{ {dv} }{ {dt} } =  - \frac{ {\partial \phi } }{ {\partial y} } - fu\\\\
&\frac{ {\partial p} }{ {\partial z} } =  - \rho g\\\\
&\frac{ {\partial u} }{ {\partial x} } + \frac{ {\partial v} }{ {\partial y} } + \frac{ {\partial \omega } }{ {\partial p} } = 0\\\\
&\frac{ {d\theta } }{ {dt} } = 0
\end{align}
$$
考虑基本流场为纬向均匀的U风场，无大尺度垂直运动，缓变（时间偏导数为0），即
$$
\begin{align}
u &= \bar u + u'\\\\
v &= v'\\\\
\omega  &= \omega'\\\\
\phi &= \bar \phi + \phi'\\\\
\frac{\partial}{\partial t} &= 0\\\\
\frac{\partial \bar u}{\partial x} &= \frac{\partial \bar \phi}{\partial x} = 0\\\\
\end{align}
$$
认为各动力学变量纬向均匀即 $\bar \phi=\bar \phi(y,p)$, $\bar u=\bar u(y,p)$, $\rho=\rho(y,p)$ 。

## x方向

将公式 (6-11) 代入公式 (1) 得
$$
\begin{align}
(\bar u + u')\frac{ {\partial \bar u + u'} }{ {\partial x} } + v'\frac{ {\partial \bar u + u'} }{ {\partial y} } + \omega'\frac{ {\partial \bar u + u'} }{ {\partial p} } &=  - \frac{ {\partial \bar \phi  + \phi'} }{ {\partial x} } + fv'\\\\(消去偏x和二阶小量)
\bar u\frac{ {\partial u'} }{ {\partial x} } + v'\frac{ {\partial \bar u} }{ {\partial y} } + \omega'\frac{ {\partial \bar u} }{ {\partial p} } &=  - \frac{ {\partial \phi'} }{ {\partial x} } + fv'\\\\
\bar u\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)v' + \omega'\frac{ {\partial \bar u} }{ {\partial p} } + \frac{ {\partial \phi'} }{ {\partial x} } &= 0
\end{align}
$$




## y方向

由于平均量需要满足公式 (2) 即
$$
\begin{align}
\frac{ {d\bar v} }{ {dt} } &=  - \frac{ {\partial \bar \phi } }{ {\partial y} } - f\bar u\\\\(\bar v=0)
f\bar u &=  - \frac{ {\partial \bar \phi } }{ {\partial y} }
\end{align}
$$


将公式 (6-11) 代入公式 (2) 得
$$
\begin{align}
(\bar u + u')\frac{ {\partial v'} }{ {\partial x} } + v'\frac{ {\partial v'} }{ {\partial y} } + \omega'\frac{ {\partial v'} }{ {\partial p} } &=  - \frac{ {\partial \bar \phi  + \phi'} }{ {\partial y} } - f(\bar u + u')\\\\(代入公式16, 消去二阶小量)
\bar u\frac{ {\partial v'} }{ {\partial x} } &=  - \frac{ {\partial \phi'} }{ {\partial y} } - fu'\\\\
fu' + \bar u\frac{ {\partial v'} }{ {\partial x} } + \frac{ {\partial \phi'} }{ {\partial y} } &= 0
\end{align}
$$

## 热力学

又静力平衡公式 (3) 得
$$
\begin{align}
\frac{ {\partial \phi } }{ {\partial p} } =  - \frac{1}{\rho }
\end{align}
$$
公式 (20) 对 y 偏导，公式 (16) 对 p 偏导，两者消去 $\phi$ 项得
$$
\begin{align}
f\frac{ {\partial \bar u} }{ {\partial p} } &= \frac{\partial }{ {\partial y} }(\frac{1}{\rho })\\\\
f\frac{ {\partial \bar u} }{ {\partial p} } &= \frac{\partial }{ {\partial y} }(\frac{ {RT} }{p})\\\\
f\frac{ {\partial \bar u} }{ {\partial p} } &= \frac{R}{p}\frac{ {\partial \theta } }{ {\partial y} }{(\frac{ { {p_0} } }{p})^{ - \frac{R}{ { {c_p} } } } }\\\\
\frac{ {\partial \theta } }{ {\partial y} } &= \frac{ {fp} }{R}{(\frac{ { {p_0} } }{p})^{\frac{R}{ { {c_p} } } } }\frac{ {\partial \bar u} }{ {\partial p} }
\end{align}
$$


将公式 (9) 代入公式 (20) 得
$$
\begin{align}
\frac{ {\partial \bar \phi  + \phi'} }{ {\partial p} } &=  - \frac{1}{\rho }\\\\
\frac{ {\partial \bar \phi  + \phi'} }{ {\partial p} } &=  - \frac{R}{p}{(\frac{ { {p_0} } }{p})^{ - \frac{R}{ { {c_p} } } } }\theta \\\\(两边对x求导)
\frac{ { {\partial ^2}\bar \phi  + \phi'} }{ {\partial x\partial p} } &=  - \frac{R}{p}{(\frac{ { {p_0} } }{p})^{ - \frac{R}{ { {c_p} } } } }\frac{ {\partial \theta } }{ {\partial x} }\\\\(\bar \phi 与x无关)
\frac{ {\partial \theta } }{ {\partial x} } &=  - \frac{R}{p}{(\frac{ { {p_0} } }{p})^{ - \frac{R}{ { {c_p} } } } }\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} }
\end{align}
$$




将公式 (6-11) 代入公式 (5) 得
$$
\begin{align}
(\bar u + u')\frac{ {\partial \theta } }{ {\partial x} } + v'\frac{ {\partial \theta } }{ {\partial y} } + \omega'\frac{ {\partial \theta } }{ {\partial p} } = 0
\end{align}
$$
将公式 (24、28) 代入公式 (29)
$$
\begin{align}
 -(\bar u + u')\frac{p}{R}{(\frac{ { {p_0} } }{p})^{\frac{R}{ { {c_p} } } } }\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } + v'\frac{ {fp} }{R}{(\frac{ { {p_0} } }{p})^{\frac{R}{ { {c_p} } } } }\frac{ {\partial \bar u} }{ {\partial p} } + \omega'\frac{ {\partial \theta } }{ {\partial p} } = 0\\\\ (消去二阶小量)
 -\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } + v'f\frac{ {\partial \bar u} }{ {\partial p} } + \frac{ {\omega'\frac{ {\partial \theta } }{ {\partial p} } } }{ {\frac{p}{R}{ {(\frac{ { {p_0} } }{p})}^{\frac{R}{ { {c_p} } } } } } } = 0 \\\\
\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } - v'f\frac{ {\partial \bar u} }{ {\partial p} } + \frac{ {\omega'\frac{ {\partial \theta } }{ {\partial p} } } }{ { -\rho \theta } } = 0 \\\\
\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } - v'f\frac{ {\partial \bar u} }{ {\partial p} } + \sigma \omega' = 0
\end{align}
$$
其中 $\sigma= -\frac{ {\frac{ {\partial \theta } }{ {\partial p} } } }{ {\rho \theta } }$ 

联立公式 (14、19、33、4) 得扰动方程组
$$
\begin{align}
\bar u\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)v' + \omega'\frac{ {\partial \bar u} }{ {\partial p} } + \frac{ {\partial \phi'} }{ {\partial x} } &= 0\\\\
fu' + \bar u\frac{ {\partial v'} }{ {\partial x} } + \frac{ {\partial \phi'} }{ {\partial y} } &= 0\\\\
\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } - v'f\frac{ {\partial \bar u} }{ {\partial p} } + \sigma \omega' &= 0\\\\
\frac{ {\partial u'} }{ {\partial x} } + \frac{ {\partial v'} }{ {\partial y} } + \frac{ {\partial \omega' } }{ {\partial p} } &= 0
\end{align}
$$

# 能量散度方程

公式 (34) 乘 $u'$ , 公式 (35) 乘 $v'$ , 公式 (36) 乘 $\sigma^{-1} \frac{\partial \phi'}{\partial p}$ 
$$
\begin{align}
\bar uu'\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)u'v' + u'\omega'\frac{ {\partial \bar u} }{ {\partial p} } + u'\frac{ {\partial \phi'} }{ {\partial x} } = 0\\\\
fu'v' + \bar uv'\frac{ {\partial v'} }{ {\partial x} } + v'\frac{ {\partial \phi'} }{ {\partial y} } = 0\\\\
\bar u{\sigma ^{ - 1} }\frac{ {\partial \phi'} }{ {\partial p} }\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } - v'f{\sigma ^{ - 1} }\frac{ {\partial \phi'} }{ {\partial p} }\frac{ {\partial \bar u} }{ {\partial p} } + \omega'\frac{ {\partial \phi'} }{ {\partial p} } = 0
\end{align}
$$
公式 (38-40) 相加得
$$
\begin{align}
\frac{1}{2}\bar u\frac{ {\partial { {u'}^2} + { {v'}^2} } }{ {\partial x} } + \frac{1}{ {2\sigma } }\bar u\frac{\partial }{ {\partial x} }{(\frac{ {\partial \phi' } }{ {\partial p} })^2} + \frac{ {\partial \phi'u'} }{ {\partial x} } + \frac{ {\partial \phi'v'} }{ {\partial y} } + \frac{ {\partial \phi'\omega'} }{ {\partial p} } = ...\\\\
 -\frac{ {\partial \bar u} }{ {\partial y} }u'v' - \frac{ {\partial \bar u} }{ {\partial p} }u'\omega' + \frac{ {f\frac{ {\partial \bar u} }{ {\partial p} } } }{\sigma }v'\frac{ {\partial \phi'} }{ {\partial p} }\\\\
\frac{ {\partial E\bar u + \phi'u'} }{ {\partial x} } + \frac{ {\partial \phi'v'} }{ {\partial y} } + \frac{ {\partial \phi'\omega'} }{ {\partial p} } =  - \frac{ {\partial \bar u} }{ {\partial y} }u'v' - \frac{ {\partial \bar u} }{ {\partial p} }u'\omega' + \frac{ {f\frac{ {\partial \bar u} }{ {\partial p} } } }{\sigma }v'\frac{ {\partial \phi'} }{ {\partial p} }
\end{align}
$$
其中  $E=\frac{1}{2}\frac{ {\partial { {u'}^2} + { {v'}^2} } }{ {\partial x} } + \frac{1}{ {2\sigma } }\frac{\partial }{ {\partial x} }{(\frac{ {\partial \phi' } }{ {\partial p} })^2}$  表示单位质量的波能量（动能+有效位能）



# 经向、垂直方向能量输送

### 经向输送

将公式 (36) 代入公式 (34) 消去 $\omega'$ 
$$
\begin{align}
\bar u\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)v' + {\sigma ^{ - 1} }( - \bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } + v'f\frac{ {\partial \bar u} }{ {\partial p} })\frac{ {\partial \bar u} }{ {\partial p} } + \frac{ {\partial \phi'} }{ {\partial x} } = 0\\\\
\bar u\frac{ {\partial u'} }{ {\partial x} } - {\sigma ^{ - 1} }\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} }\frac{ {\partial \bar u} }{ {\partial p} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})v' + \frac{ {\partial \phi'} }{ {\partial x} } = 0\\\\
\frac{\partial }{ {\partial x} }(\bar uu' + \phi' - {\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} }) = (f - \frac{ {\partial \bar u} }{ {\partial y} } - {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})v'
\end{align}
$$

> 公式 (45) 到 (46) 过程中，$\bar u$ 与 $x$ 无关所以可以放入偏微分号内部。但 $\sigma$ 这一项是与 $\theta$ 关联的，而 $\theta$ 是否与 $x$ 有关呢？

对公式 (46) 乘 $\bar uu' + \phi' - {\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} }$ 并对方程两边求纬向平均
$$
\begin{align}
{\rm{0} } &= \overline {(\bar uu' + \phi' - {\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} })(f - \frac{ {\partial \bar u} }{ {\partial y} } - {\sigma ^{ - 1} }f{ {(\frac{ {\partial \bar u} }{ {\partial p} })}^2})v'} \\\\ (下面纬向平均符号省略)
0 &= (f\bar uu' + f\phi' - f{\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} } - \frac{ {\partial \bar u} }{ {\partial y} }\bar uu' - \frac{ {\partial \bar u} }{ {\partial y} }\phi' + {\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \bar u} }{ {\partial y} }\frac{ {\partial \phi'} }{ {\partial p} } + ...\\\\
&... - \bar uu'{\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2} - \phi'{\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2} + {\sigma ^{ - 2} }\bar uf{(\frac{ {\partial \bar u} }{ {\partial p} })^3}\frac{ {\partial \phi'} }{ {\partial p} })v'\\\\
(\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})\phi'v' &= (f\bar uu' - f{\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} } - \frac{ {\partial \bar u} }{ {\partial y} }\bar uu' + {\sigma ^{ - 1} }\bar u\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \bar u} }{ {\partial y} }\frac{ {\partial \phi'} }{ {\partial p} } + ...\\\\
&... - \bar uu'{\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2} + {\sigma ^{ - 2} }\bar uf{(\frac{ {\partial \bar u} }{ {\partial p} })^3}\frac{ {\partial \phi'} }{ {\partial p} })v'\\\\
(\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})\phi'v' &= \bar u(f - \frac{ {\partial \bar u} }{ {\partial y} } - {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})u'v' + ...\\\\
&... + \bar u({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial y} }\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} } - {\sigma ^{ - 1} }f\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} } + {\sigma ^{ - 2} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^3}\frac{ {\partial \phi'} }{ {\partial p} })v'\\\\
(\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})\phi'v' &=  - \bar u(\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})u'v' + ...\\\\
&... + \bar u{\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} }(\frac{ {\partial \bar u} }{ {\partial y} } - f + {\sigma ^{ - 1} }f{(\frac{ {\partial \bar u} }{ {\partial p} })^2})v'\\\\
\phi'v' &=  - \bar uu'v' + \bar u{\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\frac{ {\partial \phi'} }{ {\partial p} }v'\\\\
\overline {\phi'v'}  &= \bar u({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} )
\end{align}
$$

### 垂直输送

对公式 (34) 乘 $\bar uu' + \phi' $ 
$$
\begin{align}
{ {\bar u}^2}u'\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)\bar uu'v' + \bar uu'\omega'\frac{ {\partial \bar u} }{ {\partial p} } + \bar uu'\frac{ {\partial \phi'} }{ {\partial x} } + ...\\\\
... + \bar u\phi'\frac{ {\partial u'} }{ {\partial x} } + (\frac{ {\partial \bar u} }{ {\partial y} } - f)v'\phi' + \phi'\omega'\frac{ {\partial \bar u} }{ {\partial p} } + \phi'\frac{ {\partial \phi'} }{ {\partial x} } = 0\\\\
\frac{ {\partial \bar u} }{ {\partial p} }(\bar uu'\omega' + \phi'\omega') + \bar uu'v'(\frac{ {\partial \bar u} }{ {\partial y} } - f) + v'\phi'(\frac{ {\partial \bar u} }{ {\partial y} } - f) + ...\\\\
... + \frac{1}{2}{ {\bar u}^2}\frac{ {\partial { {u'}^2} } }{ {\partial x} } + \frac{1}{2}\frac{ {\partial { {\phi'}^2} } }{ {\partial x} } + \bar u\frac{ {\partial u'\phi'} }{ {\partial x} } = 0
\end{align}
$$
做纬向平均得
$$
\begin{align}
(\bar u\overline {u'v'}  + \overline {v'\phi'} )(f - \frac{ {\partial \bar u} }{ {\partial y} }) = \frac{ {\partial \bar u} }{ {\partial p} }(\bar u\overline {u'\omega'}  + \overline {\phi'\omega'} )
\end{align}
$$
将公式 (57) 代入 公式 (62) 得
$$
\begin{align}
(\bar u\overline {u'v'}  + \bar u({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} ))(f - \frac{ {\partial \bar u} }{ {\partial y} }) = \frac{ {\partial \bar u} }{ {\partial p} }(\bar u\overline {u'\omega'}  + \overline {\phi'\omega'} )\\\\
\bar u{\sigma ^{ - 1} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'} (f - \frac{ {\partial \bar u} }{ {\partial y} }) = (\bar u\overline {u'\omega'}  + \overline {\phi'\omega'} )\\\\
\overline {\phi'\omega'}  = \bar u[{\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'} ]
\end{align}
$$


对公式 (43) 求纬向平均并将公式 (57) 和 (65) 代入方程
$$
\begin{align}
&\frac{ {\partial \overline {\phi'v'} } }{ {\partial y} } + \frac{ {\partial \overline {\phi'\omega'} } }{ {\partial p} } =  - \frac{ {\partial \bar u} }{ {\partial y} }\overline {u'v'}  - \frac{ {\partial \bar u} }{ {\partial p} }\overline {u'\omega'}  + \frac{ {f\frac{ {\partial \bar u} }{ {\partial p} } } }{\sigma }\overline {v'\frac{ {\partial \phi'} }{ {\partial p} } } \\\\
&\frac{\partial }{ {\partial y} }[\bar u({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} )] + \frac{\partial }{ {\partial p} }[\bar u[{\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'} ]] =  - \frac{ {\partial \bar u} }{ {\partial y} }\overline {u'v'}  - \frac{ {\partial \bar u} }{ {\partial p} }\overline {u'\omega'}  + \frac{ {f\frac{ {\partial \bar u} }{ {\partial p} } } }{\sigma }\overline {v'\frac{ {\partial \phi'} }{ {\partial p} } } \\\\
&\frac{ {\partial \bar u} }{ {\partial y} }({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} ) + \bar u\frac{\partial }{ {\partial y} }({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} ) + ...\\\\
&... + \frac{ {\partial \bar u} }{ {\partial p} }({\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'} ) + \bar u\frac{\partial }{ {\partial p} }({\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'} ) =  - \frac{ {\partial \bar u} }{ {\partial y} }\overline {u'v'}  - \frac{ {\partial \bar u} }{ {\partial p} }\overline {u'\omega'}  + \frac{ {f\frac{ {\partial \bar u} }{ {\partial p} } } }{\sigma }\overline {v'\frac{ {\partial \phi'} }{ {\partial p} } } \\\\
&\frac{\partial }{ {\partial y} }({\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'} ) + \frac{\partial }{ {\partial p} }({\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'} ) = 0
\end{align}
$$
记 $\frac{ {\partial \psi } }{ {\partial p} }={\sigma ^{ - 1} }\frac{ {\partial \bar u} }{ {\partial p} }\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'v'}$ 和 $\frac{ {\partial \psi } }{ {\partial y} }={\sigma ^{ - 1} }(f - \frac{ {\partial \bar u} }{ {\partial y} })\overline {\frac{ {\partial \phi'} }{ {\partial p} }v'}  - \overline {u'\omega'}$  因此
$$
\begin{align}
\overline {\phi'v'}  &= \bar u\frac{ {\partial \psi } }{ {\partial p} }\\\\
\overline {\phi'\omega'}  &=  - \bar u\frac{ {\partial \psi } }{ {\partial y} }
\end{align}
$$

# 准地转近似

上述公式在准地转近似下会有更为简单的形式

### 扰动方程组

由公式 (1)，(2) 得地转关系
$$
\begin{align}
fv = \frac{ {\partial \phi } }{ {\partial x} }\\\\
fu =  - \frac{ {\partial \phi } }{ {\partial y} }
\end{align}
$$
基本流场需满足地转关系，同时扰动也满足地转关系
$$
\begin{align}
f\bar v = \frac{ {\partial \bar \phi } }{ {\partial x} }\\\\
f\bar u =  - \frac{ {\partial \bar \phi } }{ {\partial y} }\\\\
fv' = \frac{ {\partial \phi'} }{ {\partial x} }\\\\
fu' =  - \frac{ {\partial \phi'} }{ {\partial y} }
\end{align}
$$
对公式 (1), (2) 的平流项取地转风 ($\bar u$, $\bar v$ )，公式 (5) 的经向平流取地转风， 忽略 $\omega$ 平流
$$
\begin{align}
\frac{ {\partial u} }{ {\partial t} } + \bar u\frac{ {\partial u} }{ {\partial x} } + \bar v\frac{ {\partial u} }{ {\partial y} } &=  - \frac{ {\partial \phi } }{ {\partial x} } + fv\\\\
\frac{ {\partial v} }{ {\partial t} } + \bar u\frac{ {\partial v} }{ {\partial x} } + \bar v\frac{ {\partial v} }{ {\partial y} } &=  - \frac{ {\partial \phi } }{ {\partial y} } - fu\\\\
\frac{ {\partial \theta } }{ {\partial t} } + u\frac{ {\partial \theta } }{ {\partial x} } + \bar v\frac{ {\partial \theta } }{ {\partial y} } &= 0
\end{align}
$$
将公式 (6)-(11) 代入公式(3)-(4), (79)-(81) 得扰动方程组
$$
\begin{align}
\bar u\frac{ {\partial u'} }{ {\partial x} } - fv' + \frac{ {\partial \phi'} }{ {\partial x} } = 0\\\\
fu' + \bar u\frac{ {\partial v'} }{ {\partial x} } + \frac{ {\partial \phi'} }{ {\partial y} } = 0\\\\
\bar u\frac{ { {\partial ^2}\phi'} }{ {\partial x\partial p} } + \sigma \omega' = 0\\\\
\frac{ {\partial u'} }{ {\partial x} } + \frac{ {\partial v'} }{ {\partial y} } + \frac{ {\partial \omega'} }{ {\partial p} } = 0
\end{align}
$$

### 经向输送

公式 (82) 整理得
$$
\begin{align}
\frac{ {\partial \bar uu' + \phi'} }{ {\partial x} } = fv'
\end{align}
$$
两边同乘 ${\bar uu' + \phi'}$ 并纬向平均得
$$
\begin{align}
0 &= \overline {(\bar uu' + \phi')fv'} \\\\
\overline {\phi'v'}  &=  - \bar u\overline {u'v'} 
\end{align}
$$

### 垂直输送



> 准地转近似下没推导出来(ಥ﹏ಥ)