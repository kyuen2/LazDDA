# LazDDA: The Velocity Decomposition Algorithm
The source code for the Velocity Decomposition Algorithm (Yuen et.al ApJ 910, 161 2021). 

## What is the physics?

We aim to separate the non-density similar fluctuations in spectroscopic channel maps. Therefore we developed a very simple similarity algorithm, supported by our paper with turbulence theory and MHD simulations, that the $p_v$ computed according to our formula might correspond to something called "velocity caustics" predicted by theory (Lazarian & Pogosyan 2000).

## Computationally what is it about?

The code allows you to compute the $p_d$ and $p_v$ based on the cross-correlation of two images $p$ and $I$. By the definition of Eq.(20) of Yuen et.al (2021), 

$$
\begin{aligned}
  p_v &= p - \left( \langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{I-\langle I\rangle}{\sigma_I^2}\\
  p_d &= \left( \langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{I-\langle I\rangle}{\sigma_I^2}
\end{aligned}
$$
where $\langle ... \rangle$ is the averaging operator. Notice that $\langle p_d p_v \rangle$ is mathematiclly guaranteed to be zero, regardless of what $p$ and $I$ it is.

For example, suppose we allow
- $I$ to be a dog's figure from UC Berkerly (https://greatergood.berkeley.edu/article/item/the_science_backed_benefits_of_being_a_dog_owner).
- $p$ to be 0.5 * cat's figure that New York Times took (https://www.nytimes.com/2021/09/07/science/cat-stripes-genetics.html), and 0.5 of dog's figure

Below we trimmed these two figures so that they are in greyscale and have same dimensions. Here we show the $p$ and $I$ before our algorithm:

![The definition of p and I of our method](https://github.com/kyuen2/LazDDA/fig/pnI.png)

and the results of our algorithm

![p_d and p_v according to our method](https://github.com/kyuen2/LazDDA/fig/pdpv.png)

We have to remind our readers that, under our construction $\langle p_d p_v \rangle$ must be zero, no matter what $p$ and $I$ you are considering. Below shows no matter what fractions cats and dogs in your image

![mean(pd*pv)=0](https://github.com/kyuen2/LazDDA/fig/pdpv_dot.png)

This is guaranteed by the mathematics, regardless of what $p$ and $I$ one is considering (see our latest response in https://github.com/kyuen2/kalberla_2022)
$$
    \begin{align}
        &\langle p_d p_v \rangle \\
        &= \Big\langle \left(\left\langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{I-\langle I\rangle}{\sigma_I^2}\right) \left(p - \left( \langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{I-\langle I\rangle}{\sigma_I^2}\right)\Big\rangle \\
        &= \left(\langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{\langle pI-p\langle I\rangle\rangle}{\sigma_I^2}-\Big\langle \left(\left\langle pI\rangle-\langle p\rangle\langle I \rangle\right)\frac{I-\langle I\rangle}{\sigma_I^2}\right)^2\Big\rangle\\
        &= \frac{\left(\langle pI\rangle-\langle p\rangle\langle I \rangle\right)^2}{\sigma_I^2}-\frac{\left(\langle pI\rangle-\langle p\rangle\langle I \rangle\right)^2}{\sigma_I^2} = 0
    \end{align}
$$



