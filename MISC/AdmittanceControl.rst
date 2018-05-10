Admittance Control
==================

Basic Equation
--------------

.. math ::

    M\ddot{x}+B\dot{x}+Kx=F


:math:`F\in\mathbb R^N`
    input, external force
:math:`x,\dot{x},\ddot{x}\in\mathbb R^N`
    output, controled movement variables
:math:`M\in\mathbb R`
    mass
:math:`B\in\mathbb R^{N\times N}`
    damp
:math:`K\in\mathbb R^{N\times N}`
    stiffness

State-space Model
-----------------

.. math ::
    \begin{split}
    A&=\begin{bmatrix} -\frac BM & -\frac KM \\ 1 & 0 \end{bmatrix}\\
    B&=\begin{bmatrix} 1 \\ 0 \end{bmatrix}\\
    C&=\begin{bmatrix} 0 & \frac 1M \end{bmatrix}\\
    D&=\begin{bmatrix} 0 \end{bmatrix}
    \end{split}

let :math:`T_s\ll T` and convert it to discrete form,

.. math ::
    \begin{split}
    A&=\begin{bmatrix} 1-\frac BMT_s & -\frac KMT_s \\ T_s & 1 \end{bmatrix}\\
    B&=\begin{bmatrix} T_s \\ 0 \end{bmatrix}\\
    C&=\begin{bmatrix} 0 & \frac 1M \end{bmatrix}\\
    D&=\begin{bmatrix} 0 \end{bmatrix}
    \end{split}