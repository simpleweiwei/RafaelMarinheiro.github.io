---
layout: default
---

<figure>
	<img width="30%" src="/projects/photometric_stereo/img/calibrated_buddha_albedo.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/calibrated_buddha_normal.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/calibrated_buddha_depth.png"></img>
</figure>

# Photometric Stereo

This project was developed as part of an assignment of [CS6644 - Modelling the World](http://www.cs.cornell.edu/courses/CS6644/2014fa/).

## Code

The code will be available after the deadline.

## The basics

Given a set of images taken from the same point of view but with a different light setting, we can try to infer something about the surface.

<figure>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.11.png"></img>
	<figcaption>Photos with varying light configuration</figcaption>
</figure>

Let us assume that the object that we are trying to reconstruct has a diffuse surface. Also, let us ignore self-occlusion. If that is the case, then we can calculate the intensity of a certain point in the object using the following formula:

$$I = l\cdot k_s \cdot L^\top N$$

Where $$L$$ is the Light direction vector, $$N$$ is the Normal vector, $$l$$ is the light intensity and $$k_s$$ is the albedo of the material.

## Calibrated Light

If we have $$m$$ measurements of an object and if we know the light directions and intensities, then we have the following linear system for each pixel:

$$
\overbrace{
\begin{pmatrix}
	I^p_0\\
	\vdots\\
	I^p_{m-1}
\end{pmatrix}
}^{I \in \mathbb{R}^{m\times 1}}
=

k_s^p
\overbrace{
\begin{pmatrix}
l_0L_0^\top\\
\vdots\\
l_{m-1}L_{m-1}^\top
\end{pmatrix}
}^{L \in \mathbb{R}^{m\times 3}}
N^p
$$

Since $$N^p$$ is a unitary vector, we can simply solve the linear system to obtain $$N$$. Since the linear system is probably overconstrained, we can instead solve the Linear Least Squares problem to obtain the solution:

$$
\bar{N} = (L^\top L)^{-1}L^\top I
$$

$$
N = \frac{\bar{N}}{|\bar{N}|}
$$

If we possess the Light intensities, the Light Matrix and also the Normals, we obtain $$k_s$$, by using:

$$
k_s = \frac{I^\top (LN)}{(LN)^\top (LN)}
$$

Notice that this formula is should give exactly the same answer as $$k_s = \|\bar{N}\|$$. However, we do this because it is simpler to reuse the normals that we have to compute the albedo for different channels ($$k_r$$, $$k_g$$ and $$k_b$$).

### Implementation

We have used Python, PIL (Python Imaging Library) and Scipy in our implementation. Given some RGB images, we first convert them to grayscale using the ITU-R 601-2 luma transform:

$$L = \frac{299R + 587G + 114B}{1000}$$

After that, we run the algorithm in the grayscale image to obtain the normals. With those normals, we compute the albedo for each channel using the method described above.

### Results

#### Buddha
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/buddha/buddha.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="80%" src="/projects/photometric_stereo/img/calibrated_buddha_normal.png"></img>
	<figcaption>Normal Map</figcaption>
</figure>
<figure>
	<img width="80%" src="/projects/photometric_stereo/img/calibrated_buddha_albedo.png"></img>
	<figcaption>Albedo Map</figcaption>
</figure>

You can all the results [here](/projects/photometric_stereo/calibrated_results).

The normal maps generated by this method are quite good (we will see this when we try to compute the depth map). However, we can see some flaws in it. Notice that this object violates the assumption that we made about self-occlusion. Because of this, notice that there exists some "shadows" in the normal map near the neck. This also affects the albedo map.

## Uncalibrated Light

So far, we have assumed that we knew the Light Matrix $$L$$. However, this may not be always true. However, we can still exploit our assumptions to try to come up with a good approximation for $$L$$ and $$N$$. Lets assume that the equation $$l\cdot k_s \cdot L^\top N$$ holds (it is, the object is diffuse and there do not exist self-intersections). If that is the case, then we can write the following equation:

$$
\overbrace{
\begin{pmatrix}
	i^0_0 & \ldots & i^{p-1}_0\\
	\vdots & \ddots & \vdots \\
	i^0_{m-1} & \ldots & i^{p-1}_{m-1}
\end{pmatrix}
}^{M \in \mathbb{R}^{m \times p}}
= 
\overbrace{
\begin{pmatrix}
	L_0^\top\\
	\vdots\\
	L_{m-1}^\top
\end{pmatrix}
}^{L \in \mathbb{R}^{m \times 3}}
\overbrace{
\begin{pmatrix}
	N^0 & \ldots & N^{p-1}_0\\
\end{pmatrix}
}^{N \in \mathbb{R}^{3 \times p}}
$$

In this equation, $$m$$ is the number of measurements and $$p$$ is the number of pixels in the image. Notice, however, that this means that the measurement matrix $$M$$, which is known, is rank 3. If we calculate the SVD of $$M = U\Sigma V^\top$$, we can consider only the 3 biggest singular values such that the matrices. If we do so, we will have the following rank 3 approximation:

$$
M = \bar{U}\bar{\Sigma}\bar{V}^\top
$$

If we do this, we can try to approximate the Light and the Normal matrix:

$$
\bar{L} = \bar{U}\sqrt{\bar{\Sigma}}
$$

$$
\bar{N} = \sqrt{\bar{\Sigma}}\bar{V}^\top
$$

However, the solution is not unique. In fact, any solution of the form $$\hat{L} = \bar{L}A$$ and $$\hat{N} = A^{-1}\bar{N}$$ would also be valid. To try to reduce the degree of freedom of $$A$$, we can try to enforce the constraint that every light has exactly the same intensity (this is true for our data set):

$$\forall_{i\in [0, m)}(A\bar{L}_i)^\top (A\bar{L}_i) = 1 \Rightarrow \forall_{i\in [0, m)}\bar{L}_i^\top B \bar{L}_i = 1 $$

Since $$B = A^TA$$ is symmetric, we can write $$B = \begin{pmatrix} a & b & c \\ b & d & e \\ c & e & f \end{pmatrix}$$. Also, we can write the condition above as matrix equation:

$$ 
\left(\begin{smallmatrix}
	\bar{L}_0^x\cdot \bar{L}_0^x & \bar{L}_0^x\cdot \bar{L}_0^y & \bar{L}_0^x\cdot \bar{L}_0^z & \bar{L}_0^y\cdot \bar{L}_0^y & \bar{L}_0^y\cdot \bar{L}_0^z & \bar{L}_0^z\cdot \bar{L}_0^z\\
	\vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
	\bar{L}_{m-1}^x\cdot \bar{L}_{m-1}^x & \bar{L}_{m-1}^x\cdot \bar{L}_{m-1}^y & \bar{L}_{m-1}^x\cdot \bar{L}_{m-1}^z & \bar{L}_{m-1}^y\cdot \bar{L}_{m-1}^y & \bar{L}_{m-1}^y\cdot \bar{L}_{m-1}^z & \bar{L}_{m-1}^z\cdot \bar{L}_{m-1}^z
\end{smallmatrix}
\right)
\left(
\begin{smallmatrix}
a\\b\\c\\d\\e\\f
\end{smallmatrix}
\right)
=
\left(
\begin{smallmatrix}
1\\ \vdots \\1
\end{smallmatrix}
\right)
$$

We can use Linear Least Squares to solve this overconstrained problem. After that, we form the $$B$$ matrix, then we compute its SVD $$B = U\Sigma V^\top$$ and then we set $$A = U\sqrt{\Sigma}$$. Notice that we could still apply any rotation to $$A$$ and it would still be valid. In our implementation, use $$A = U\sqrt{\Sigma}\left(\begin{smallmatrix} 0 & 0 & 1 \\ 0 & -1 & 0 \\ -1 & 0 & 0\end{smallmatrix}\right)$$ just because it looks good in the buddha test case. After computing the light matrix and the normals, we compute the albedo by using the same method that we have used in the calibrated setting.

### Results

#### Buddha
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_normal.png"></img>
	<figcaption>Normal Map - Left: Uncalibrated, Right: Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_albedo.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_albedo.png"></img>
	<figcaption>Albedo Map - Left: Uncalibrated, Right: Calibrated</figcaption>
</figure>

You can all the results [here](/projects/photometric_stereo/uncalibrated_results).

## Computing Depth

Given a normal map, we can estimate the depth by enforcing the following constraint for each pixel:

$$
\begin{cases}
	\begin{pmatrix}1\\0\\z_{x+1,y} - z_{x,y}\end{pmatrix}^\top N_{x,y} = 0\\
	\begin{pmatrix}0\\1\\z_{x,y+1} - z_{x,y}\end{pmatrix}^\top N_{x,y} = 0\\
\end{cases}
$$

We do not enforce those constraints at the boundary and we do not enforce those constraints if $$\|N^z_{x,y}\| \le 0.01$$. We use a sparse linear least square solver to compute the solution of this huge linear system, trying to obtain the $$z$$ map (the depth map)

### Results

#### Buddha
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_depth.png"></img>
	<figcaption>Normal Map and Depth Map- Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_depth.png"></img>
	<figcaption>Normal Map and Depth Map- Unalibrated</figcaption>
</figure>


You can all the results [here](/projects/photometric_stereo/depth_map).

