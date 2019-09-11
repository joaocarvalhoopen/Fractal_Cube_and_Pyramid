# Fractal Cube and Fractal Pyramid

Programs that draw in 3D the fractal cube and the fractal pyramid.

## Description
Those two programs use VPython for Anaconda Python 3.7 to draw in a simple way in 3D inside a Jupyter notebook the fractal cube [Menger sponge]( https://en.wikipedia.org/wiki/Menger_sponge)  and the fractal pyramid [Sierpiński triangle]( https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle). <br>
Note: The Jupyter notebooks with VPython don’t open correctly inside GitHub, but they work well on the PC with VPython installed for Anaconda. The images are from the local version. <br>

## Images and code
[Fractal cube source code](./Fractal_Cube.ipynb) <br>

![fractal cube image](./fractal_cube_image.png?raw=true "fractal cube image") <br>

```
from vpython import *

def draw_cube(box_list, xi, yi, zi, side_len, deep):
    part_side_len = side_len / 3.0
    for x in range(0, 3):
        for y in range(0, 3):
            for z in range(0, 3):
                if (x==1 and y==1) or (x==1 and z==1) or (y==1 and z==1):
                    continue
                x0 = xi + x * part_side_len
                y0 = yi + y * part_side_len
                z0 = zi + z * part_side_len
                if (deep == 0):
                    mybox = box(pos=vector(x0,y0,z0), length=part_side_len, height=part_side_len, width=part_side_len)
                    box_list.append(mybox)
                    #print((x0,y0,z0))
                else:
                    draw_cube(box_list, x0, y0, z0, part_side_len, deep-1)
                    
box_list = []
draw_cube(box_list, xi=0.0, yi=0.0, zi=0.0, side_len=1.0, deep=2)

```

[Fractal cube source code](./Fractal_Pyramid.ipynb) <br>

![fractal pyramid image](./fractal_pyramid_image.png?raw=true "fractal pyramid image") <br>

```
from vpython import *

def draw_pyramid_inner(pyramid_list, x0, y0, z0, part_side_len, deep):
    if (deep == 0):
        my_pyramid = pyramid(pos=vector(x0,y0,z0),
                             size=vector(part_side_len, part_side_len, part_side_len),
                             up=vector(-1,0,0),
                             shininess=(0.6))
        pyramid_list.append(my_pyramid)
        #print((x0,y0,z0))
    else:
        draw_pyramid(pyramid_list, x0, y0, z0, part_side_len, deep-1)

def draw_pyramid(pyramid_list, xi, yi, zi, side_len, deep):
    part_side_len = side_len / 2.0
    # Four lower pyramids.                         
    for x in range(0, 2):
        for z in range(0, 2):
            x0 = xi + x * part_side_len
            y0 = yi 
            z0 = zi + z * part_side_len                 
            draw_pyramid_inner(pyramid_list, x0, y0, z0, part_side_len, deep)
    # One upper pyramid. 
    part_side_len_upper = side_len / 4.0 
    x0 = xi + part_side_len_upper
    y0 = yi + part_side_len 
    z0 = zi + part_side_len_upper                 
    draw_pyramid_inner(pyramid_list, x0, y0, z0, part_side_len, deep)
    
pyramid_list = []
draw_pyramid(pyramid_list, xi=0.0, yi=0.0, zi=0.0, side_len=1.0, deep=4)
```



## License
MIT Open Source License

## Have fun!
Best regards, <br>
Joao Nuno Carvalho <br>

