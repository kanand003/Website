---
title: "RayTracer in One Weekend"
date: 2025-06-11
draft: false
url: "/projects/raytracer"
image: "/Website/images/Image_Final.JPG"
description: "A simple implementation of a Ray Tracer"
summary: ""
tags: []
ShowReadingTime: true
ShowWordCount: true    
---

## Introduction

Made a ray tracer over a weekend. Was quite happy with the final results.

## Project Preview

<!-- Main project image with styling -->
<div style="max-width: 800px; margin: 20px auto;">
    <img src="/Website/images/Image_Final.JPG" alt="Ray Tracer Result Preview" style="width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
</div>

## Implementation Details

### Core Ray Tracing Logic
```cpp
class ray {
    public:
        ray() {}
        ray(const vec3& origin, const vec3& direction) 
            : orig(origin), dir(direction) {}
        
        vec3 origin() const { return orig; }
        vec3 direction() const { return dir; }
        vec3 point_at_parameter(float t) const { return orig + t*dir; }

        vec3 orig;
        vec3 dir;
};

vec3 color(const ray& r, hitable *world, int depth) {
    hit_record rec;
    if (world->hit(r, 0.001, MAXFLOAT, rec)) {
        ray scattered;
        vec3 attenuation;
        if (depth < 50 && rec.mat_ptr->scatter(r, rec, attenuation, scattered)) {
            return attenuation * color(scattered, world, depth + 1);
        }
        else {
            return vec3(0, 0, 0);
        }
    }
    else {
        vec3 unit_direction = unit_vector(r.direction());
        float t = 0.5 * (unit_direction.y() + 1.0);
        return (1.0-t)*vec3(1.0, 1.0, 1.0) + t*vec3(0.5, 0.7, 1.0);
    }
}
```

### Material System
```cpp
class material {
    public:
        virtual bool scatter(const ray& r_in, const hit_record& rec, 
            vec3& attenuation, ray& scattered) const = 0;
};

class lambertian : public material {
    public:
        lambertian(const vec3& a) : albedo(a) {}
        
        virtual bool scatter(const ray& r_in, const hit_record& rec, 
            vec3& attenuation, ray& scattered) const {
            vec3 target = rec.p + rec.normal + random_in_unit_sphere();
            scattered = ray(rec.p, target-rec.p);
            attenuation = albedo;
            return true;
        }

        vec3 albedo;
};

class metal : public material {
    public:
        metal(const vec3& a, float f) : albedo(a) { 
            if (f < 1) fuzz = f; else fuzz = 1;
        }

        virtual bool scatter(const ray& r_in, const hit_record& rec, 
            vec3& attenuation, ray& scattered) const {
            vec3 reflected = reflect(unit_vector(r_in.direction()), rec.normal);
            scattered = ray(rec.p, reflected + fuzz*random_in_unit_sphere());
            attenuation = albedo;
            return (dot(scattered.direction(), rec.normal) > 0);
        }

        vec3 albedo;
        float fuzz;
};
```

### Scene Setup
```cpp
hitable *random_scene() {
    int n = 500;
    hitable **list = new hitable*[n+1];
    list[0] = new sphere(vec3(0,-1000,0), 1000, new lambertian(vec3(0.5, 0.5, 0.5)));
    int i = 1;
    for (int a = -11; a < 11; a++) {
        for (int b = -11; b < 11; b++) {
            float choose_mat = random_double();
            vec3 center(a+0.9*random_double(),0.2,b+0.9*random_double());
            if ((center-vec3(4,0.2,0)).length() > 0.9) {
                if (choose_mat < 0.8) {  // diffuse
                    list[i++] = new sphere(
                        center, 0.2,
                        new lambertian(vec3(random_double()*random_double(),
                                          random_double()*random_double(),
                                          random_double()*random_double()))
                    );
                }
                else if (choose_mat < 0.95) { // metal
                    list[i++] = new sphere(
                        center, 0.2,
                        new metal(vec3(0.5*(1 + random_double()),
                                     0.5*(1 + random_double()),
                                     0.5*(1 + random_double())),
                                0.5*random_double())
                    );
                }
                else {  // glass
                    list[i++] = new sphere(center, 0.2, new dielectric(1.5));
                }
            }
        }
    }

    list[i++] = new sphere(vec3(0, 1, 0), 1.0, new dielectric(1.5));
    list[i++] = new sphere(vec3(-4, 1, 0), 1.0, new lambertian(vec3(0.4, 0.2, 0.1)));
    list[i++] = new sphere(vec3(4, 1, 0), 1.0, new metal(vec3(0.7, 0.6, 0.5), 0.0));

    return new hitable_list(list,i);
}
```

## Demo Video

<!-- YouTube video embed with responsive container -->
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; border-radius: 8px; margin: 20px auto;">
    <!-- Replace VIDEO_ID with your actual YouTube video ID -->
    <iframe 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);" 
        src="https://www.youtube.com/embed/YOUR_VIDEO_ID" 
        title="Ray Tracer Demo"
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
    </iframe>
</div>

## Features
- Path tracing with multiple bounces
- Support for different materials (Lambertian, Metal, Dielectric)
- Anti-aliasing
- Defocus blur (depth of field)
- Motion blur
- Hierarchical bounding volume optimization

## GitHub Repository

Check out the code: [RayTracer on GitHub](https://github.com/kanand003/RayTracerWeekend)
