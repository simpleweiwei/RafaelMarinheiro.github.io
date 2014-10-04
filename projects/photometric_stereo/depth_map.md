---
layout: default
title: Photometric Stereo

---
# Photometric Stereo - Depth Map

## Results

### Buddha
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
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_buddha_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_buddha_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>

Notice that the depth maps are quite different. This is happening due to the fact the the normals at the uncalibrated setting are only equal up to a rotation matrix.

### Cat
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/cat/cat.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_cat_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_cat_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_cat_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_cat_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>

### Gray
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/gray/gray.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_gray_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_gray_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_gray_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_gray_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>

In this case we have some holes in the uncalibrated setting. This is happening because $$\|N^z_{x,y}\| \le 0.01$$ at those regions, so the depth is unconstrained. The linear least squares algorithm that I am using is probably setting them to 0.

### Horse
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/horse/horse.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_horse_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_horse_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_horse_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_horse_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>

Here we notice that the depth map is "inverted. This is happening because the normals themselves are inverted, so it looks like we are seeing a hollow horse.

### Owl
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/owl/owl.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_owl_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_owl_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_owl_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_owl_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>

Here we notice that the depth map is "inverted. This is happening because the normals themselves are inverted, so it looks like we are seeing a hollow owl.


### Rock
<figure class="polaroid">
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.0.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.1.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.2.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.3.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.4.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.5.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.6.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.7.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.8.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.9.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.10.png"></img>
	<img width="30%" src="/projects/photometric_stereo/img/data/rock/rock.11.png"></img>
	<figcaption>Source images</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_rock_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/calibrated_rock_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Calibrated</figcaption>
</figure>
<figure>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_rock_normal.png"></img>
	<img width="40%" src="/projects/photometric_stereo/img/uncalibrated_rock_depth.png"></img>
	<figcaption>Normal Map and Depth Map - Uncalibrated</figcaption>
</figure>