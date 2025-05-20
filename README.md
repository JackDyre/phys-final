# Modeling the Magnus Force

---

Oftentimes in physics we choose to ignore air resistance. It makes computations much simpler, while in most cases the error is negligible. But what if we want to account for air interactions in our model?

In this paper we will look at three different models, starting with the most basic model of motion, and build our way to the Magnus effect, adding an element of interaction with air at each step.


---
#### Constant Acceleration

The simplest model of motions is the constant acceleration model. It is the model we used at the beginning of physics one, which completely ignores air resistance, and assumes a constant acceleration over time.

It can be modeled quite simply with the following differential equation

$$x'' = a$$

which trivially solves to:

$$x' = v_0 + at$$
$$x = x_0 + tv_0 + \frac{1}{2}at^2$$

This is the formula provided on the physics one formula sheet, meaning our calculations were correct.

This model is simply a parabola, which makes using it in calculations quite straightforward.

---
#### Linear Drag

The obvious next step is to account for drag force. Before modeling it with equations, I think it is important to get an intuitive understanding first.

The simplest model of drag is known as linear drag or Stokes' drag. Linear drag asserts that the magnitude of the drag force ($F_D$) is linearly related to magnitude of velocity and is in the opposite direction as velocity.

As the ball moves through space it is displacing air. It is ramming into the particles in front of it and leaving empty space behind it. The collisions enacts a third-law force along with the low pressure behind creating a "negative" force (caused by the constant atmospheric everywhere else). The volume of air displaced varies linearly with speed, which motivates the linear relationship between velocity and drag force

The magnitudes are related by the drag coefficient $b$, which is affected by characteristics of the air/fluid such as viscosity and by characteristics of the object such as roughness or surface area.

This is quite simple to add to the existing model of motion. Assuming it is still experiencing constant acceleration, we can model linear drag with the following differential equation:

$$x'' = a - \frac{bx'}{m}$$

Letting the constant term $\frac{b}{m} = \beta$, it simplifies to:

$$x'' = a - \beta x'$$

This is not as trivial to solve. To find $x'$, we can treat it as a first order differential equation of $v$ rather than $x$. Using the integrating factor method, we can show that:

$$x' = \frac a \beta + C_1e^{-\beta t}$$

Simply integrating again gives us that:

$$x = \frac{a}{\beta}t - \frac{C_1}{\beta}e^{-\beta t}+C_2$$
We can use the initial condition $x(0) = x_0$ and $x'(0) = v_0$ and a little algebraic manipulation to get that:

$$x=x_0+\frac{a}{\beta}\,t+\frac{v_0-\frac{a}{\beta}}{\beta}\,\bigl(1-e^{-\beta t}\bigr)$$

This graph has some interesting properties. Assuming $\beta\ne 0$, the graph always asymptotically approaches a linear shape as $t$ tends towards infinity. The slope of the asymptote is determined by the value of the constant acceleration $a$. This demonstrates the concept of terminal velocity, as when the velocity increases so does the amount of drag force counteracting the acceleration until they cancel each other out.

Another interesting property is as we take the $\lim_{\beta \rightarrow 0}$ of our derivation for $x$, it can be shown using Taylor series' that the limit approaches our constant acceleration derivation. This makes logical sense considering the initial models of $x''$ of the two scenarios, as the linear drag model approaches the constant acceleration model as $\beta$ approaches $0$.

---
#### Quadratic Drag

There is another model for drag known as quadratic drag.  This model of drag asserts that $F_D$ varies in proportion to $v^2$. The quadratic drag model is more accurate in turbulent scenarios opposed to linear drag which is more accurate in laminar scenarios.

It is left as an exercise to the reader to solve this model.

---
#### Magnus Force

It is finally time to move into two dimensions.

The Magnus force is the force that causes rotating balls to curve. It is the force behind the viral youtube videos of dropping basketballs off of dams. It is the force that allows baseball players to throw curveballs. It is the force that lets tennis players hit serves without being 7 feet tall.

To understand the Magnus force, it is easiest to take a frame of reference moving with the ball, but not rotating with it. In this frame of reference, air is blowing past the stationary rotating ball.

One side of the ball is moving in the same direction as the air and the other is opposing the air. The side of the ball rotating with the air, due friction will pull some amount of air through its curvature. The side of the ball rotating against the air will divert the stream of air, and force some air perpendicular, in the same direction as the other side. Newton's third law tells us that forcing the air perpendicularly in one direction must cause the ball to be forced in the other perpendicular direction.

Modeling this can get very nasty, so we will make some assumptions. Firstly we will assume that the angular velocity of the ball stays constant over time and does not decrease due to friction.

The vector-quantity Magnus force ($\vec{F_M}$) is defined as $c (\vec{\omega} \times \vec{v})$ where $c$ is the scalar Magnus coefficient, $\vec{\omega}$ is the 3-dimensional vector quantity $(0, 0, \omega)$ with magnitude $\omega$ , the rotational velocity, (used for extending 3-dimensional cross product down to 2 dimensions), $\vec{v}$ is the 2-dimensional quantity extended to 3-dimensions: $(x', y', 0)$, and $\times$ is the cross product.

To form a differential model of this system, one just needs to break it into components. Assuming the ball is undergoing constant acceleration and linear drag, we can add our Magnus acceleration to our linear drag differential model. Let the constant $\sigma = \frac {c\omega} m$

$$x'' = a_x - \beta x' - \sigma y'$$
$$y'' = a_y - \beta y' + \sigma x'$$

This coupled second-order differential system is quite complicated, as solving it requires complex-number math that surpasses me. The solution involves decoupling the system into a single complex differential equation. The solution steps are left as an exercise to the reader.

Using an online calculator yields the following solution:

$$
x = \frac{a_x\beta - a_y\sigma}{\beta^2 + \sigma^2} t + C_1 + e^{-\beta t}(\mathrm{D}_1\cos\sigma t - \mathrm{D}_2\sin\sigma t),
$$
$$
y = \frac{a_x\sigma + a_y\beta}{\beta^2 + \sigma^2} t + C_2 + e^{-\beta t}(\mathrm{D}_1\sin\sigma t + \mathrm{D}_2\cos\sigma t),
$$

This formula is honestly quite complicated, and almost impossible to get any insights from it purely numerically. Additionally, due to the assumptions and simplifications, when we take the limit as the drag coefficient and magnus coefficient go to zero, it does not approach our original constant acceleration model. On top of that, as the model is in 3 dimensions (x, y, and time), it can't be put into demos to analyze graphically.

---
#### Reflection

In this paper, we represented three different models of motion of a ball through space, building towards modeling the Magnus force. We built up from the absolute basics from Physics 1 kinematics to complex analysis well above my abilities. While we weren't able to glean much from the numeric Magnus solution, we still gained an understanding of how it works.


