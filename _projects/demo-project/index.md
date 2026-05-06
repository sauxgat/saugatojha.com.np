---
layout: post
title: Otto Cycle Visualization In Python With Matplotlib
description:  This is a small coding project to bring my theoretical knowledge into practice with coding. 
    Developing the visualization project involves knowing fundamentals of Python and some Matplotlib. 
skills: 
  - Python
  - Data Structures
  - IC Engines Working Principles

main-image: /project2.png
---

---
<!-- # Header 1 
## Header 2  
Use this for the header of each section
### Header 3 
Use this to have subsection if needed


## Embedding images 
### External images
{% include image-gallery.html images="https://live.staticflickr.com/65535/52821641477_d397e56bc4_k.jpg, https://live.staticflickr.com/65535/52822650673_f074b20d90_k.jpg" height="400"%}
<span style="font-size: 10px">"Starship Test Flight Mission" from https://www.flickr.com/photos/spacex/52821641477/</span>  
You can put in multiple entries. All images will be at a fixed height in the same row. With smaller window, they will switch to columns.  

### Embeed images
{% include image-gallery.html images="project2.jpg" height="400" %} 
place the images in project folder/images then update the file path.   


## Embedding youtube video
The second video has the autoplay on. copy and paste the 11-digit id found in the url link. <br>
*Example* : https://www.youtube.com/watch?v={**MhVw-MHGv4s**}&ab_channel=engineerguy
{% include youtube-video.html id="MhVw-MHGv4s" autoplay= "false"%}
{% include youtube-video.html id="XGC31lmdS6s" autoplay = "true" %}

you can also set up custom size by specifying the width (the aspect ratio has been set to 16/9). The default size is 560 pixels x 315 pixels.  

The width of the video below. Regardless of initial width, all the videos is responsive and will fit within the smaller screen.
{% include youtube-video.html id="tGCdLEQzde0" autoplay = "false" width= "900px" %}  

<br>

## Adding a hozontal line
---

## Starting a new line
leave two spaces "  " at the end or enter <br>

## Adding bold text
this is how you input **bold text**

## Adding italic text
Italicized text is the *cat's meow*.
-->
## Steps Involved :
1. Define engine parameters from the engine kinematic equation.
2. Define your inputs.
3. Calculate the values of Pressure and Volume for each state point.
4. Plot the graph using Matplotlib library.
<!-- 
Adding unordered list
- First item
- Second item
- Third item
- Fourth item -->

# Python Code Used :
```python
import math
import matplotlib.pyplot as plt
gamma = 1.4
num_value = 50
#engine kinematics function
def engine_parameters(bore,stroke,con_rod,cr,start_crank,end_crank,v_s,v_c):
    a = stroke/2
    R = con_rod/a
    sc=math.radians(start_crank)
    ec=math.radians(end_crank)
    dtheta = (ec-sc)/(num_value-1)
    V = []
    for i in range(0,num_value):
        theta = sc+ i*dtheta
        term1 = 0.5*(cr-1)
        term2 = R+1-math.cos(theta)
        term3 = pow(R,2) - pow(math.sin(theta),2)
        term3 = pow(term3,0.5)
        V.append((1+term1*(term2-term3))*v_c)
    return V
#graph function
def graph_plot():
    plt.figure(1)
    plt.plot(V_compression,P_compression,label='Adiabatic Compression')
    plt.plot([v2,v3],[p2,p3],label='Constant Volume Head Addition')
    plt.plot(V_expansion,P_expansion,label='Adiabatic Expansion')
    plt.plot([v4,v1],[p4,p1],label='Constant Volume Heat Rejection')
    plt.xlabel('Volume')
    plt.ylabel('Pressure')
    plt.legend()
    plt.title('Otto Cycle PV Diagram')
    plt.savefig('otto_cycle_pv_diagram.png')
    plt.show()
#Define Inputs 
p1 = float(input("Type the value for P1: (Pa) \t"))  
t1 = float(input("Type the value for T1: (K) \t"))
t3 = float(input("Type the value for T3: (K) \t"))
bore = float(input("Type the value for bore diameter: (m) \t"))
stroke = float(input("Type the value for length of stroke: (m)\t"))
con_rod = float(input("Type the value for length of connecting rod:(m) \t"))
cr = int(input("Type the value for Compression Ratio:\t"))
# Calculate Volumes
v_s = (math.pi/4)*pow(bore,2)*stroke
v_c=v_s/(cr-1)
v1=v_s+v_c
v2=v_c
#calculate state point 2
p2 = p1*pow(v1,gamma)/pow(v2,gamma)
rhs =p1 *v1/t1
t2 =p2*v2/rhs
#compression process
V_compression =engine_parameters(bore,stroke,con_rod,cr,180,0,v_s,v_c)
constant =p1*pow(v1,gamma)
P_compression=[constant/pow(v,gamma) for v in V_compression]
#calculate state point 3
v3=v2
rhs=p2*v2/t2
p3=rhs*t3/v3
expansion process
V_expansion=engine_parameters(bore,stroke,con_rod,cr,0,180,v_s,v_c)
constant =p3*pow(v3,gamma)
P_expansion =[constant/pow(v,gamma) for v in V_expansion]
#state point 4
v4 = v1
p4 =p3*pow(v3,gamma)/pow(v4,gamma)
rhs=p3*v3/t3
t4=p4*v4/rhs
eff = 1 - (1 / pow(cr, (gamma - 1)))
eff_percent = eff * 100
print(f'Thermal Efficiency: {eff_percent:.2f}%') 
graph_plot()
```

<!--
## Adding external links


## Adding block quote
> A blockquote would look great if you need to highlight something


## Adding table 

| Header 1 | Header 2 |
|----------|----------|
| Row 1, Col 1 | Row 1, Col 2 |
| Row 2, Col 1 | Row 2, Col 2 |

make sure to leave aline betwen the table and the header -->


