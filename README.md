# planetary-simulation
from vpython import *

def gforce(pla,sta):
    
    G=1
    r_vec = pla.pos - sta.pos
    r_mag = mag(r_vec)
    r_hat = r_vec/r_mag
    F_mag = (G*pla.mass*sta.mass)/(r_mag**2)
    F_vec = -F_mag*r_hat
    
    return F_vec

sun = sphere(pos=vector(0,0,0),radius=0.2,momentum=vector(0,0,0),
             color=color.white,mass=2*900,make_trail = True)

earth = sphere(pos=vector(1,0,0),radius=0.05,momentum=vector(0,50,0),
                color=color.green,mass=1,make_trail=True)

mars = sphere(pos=vector(-2,0,0),radius=0.04,momentum=vector(0,30,0),
              color=color.red,mass=0.87,make_trail = True)

comet = sphere(pos=vector(3,-3,0),radius=0.05,momentum=vector(1,1,0),
               mass=0.05,make_trail = True,color=color.yellow)

def sim():
    t=0
    
    while True:
        rate(500)
    
        sun.force=gforce(sun,earth)+gforce(sun,mars)+gforce(sun,comet)
        earth.force=gforce(earth,sun)+gforce(earth,mars)+gforce(earth,comet)
        mars.force=gforce(mars,sun)+gforce(mars,earth)+gforce(mars,comet)
        comet.force=gforce(comet,sun)+gforce(comet,earth)+gforce(comet,mars)
    
        sun.momentun=sun.momentum+sun.force*0.0001
        earth.momentum=earth.momentum+earth.force*0.0001
        mars.momentum=mars.momentum+mars.force*0.0001
        comet.momentum=comet.momentum+comet.force*0.0001
    
        sun.pos=sun.pos+((sun.momentum)/sun.mass)*0.0001
        earth.pos=earth.pos+((earth.momentum)/earth.mass)*0.0001
        mars.pos=mars.pos+((mars.momentum)/mars.mass)*0.0001
        comet.pos=comet.pos+((comet.momentum)/comet.mass)*0.0001
        
        m=earth.pos
       # f=open('C:/Users/rithu/Desktop/positione.txt',"w")
       # print(str(m))
        #f.write(str(m))
       # f.write("\n")
        
        t=t+0.0001
    
#f.close()
sim()
