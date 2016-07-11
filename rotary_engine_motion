"""
Rotary Engine Motion Animation using Matplotlib.
Animation designed to run on Raspberry Pi 2

Author: Peter D. Kazarinoff, 2016
Tribilium Engineering Solutions   www.tribilium.com

For animated shapes See: https://nickcharlton.net/posts/drawing-animating-shapes-matplotlib.html
For rotary equations See: http://www.personal.utulsa.edu/~kenneth-weston/chapter7.pdf

"""

#import necessary packages
import numpy as np
from numpy import pi, sin, cos
import matplotlib.pyplot as plt
import matplotlib.animation as animation

#input parameters
R = 6  # rotor center to tip distance
e = 1  # eccentricity   #note: 0 < e/R < 0.25
rot_num = 2 # number of crank rotations
increment = 0.1 # angle incremement


#create the angle array, where the last angle is the number of rotations*2*pi
angle_minus_last = np.arange(0,rot_num*2*pi,increment)
R_Angle = np.append(angle_minus_last, rot_num*2*pi)

#set up empty arrays to hold the animation points
X_housing=np.zeros(len(R_Angle)) # x-cooridnate of rotor housing
Y_housing=np.zeros(len(R_Angle)) # y-cooridnate of rotor housing

X1=np.zeros(len(R_Angle)) # array of rotor x-positions: Point 1
Y1=np.zeros(len(R_Angle)) # array of rotor y-positions: Point 1
X2=np.zeros(len(R_Angle)) # array of rotot x-positions: Point 2
Y2=np.zeros(len(R_Angle)) # array of rotor y-positions: Point 2
X3=np.zeros(len(R_Angle)) # array of rotor x-positions: Point 3
Y3=np.zeros(len(R_Angle)) # array of rotor y-positions: Point 3

#find the crank and rocker arm positions for each angle
for index,R_Angle in enumerate(R_Angle, start=0):
    theta = R_Angle
    x_housing = (e)*cos(3*theta) + (R)*cos(theta) # x-cooridnate of rotor tip 
    y_housing = (e)*sin(3*theta) + (R)*sin(theta) # y-cooridnate of rotor tip

    X_housing[index]=x_housing #grab the housing ouline point
    Y_housing[index]=y_housing #grab the housing outline point


    x1 = e*cos(3*theta) + R*cos(theta) #rotor point 1
    y1 = e*sin(3*theta) + R*sin(theta) #rotor point 1

    x2 = e*cos(3*theta) + R*cos(theta + 2*pi/3) #rotor point 2
    y2 = e*sin(3*theta) + R*sin(theta + 2*pi/3) #rotor point 2

    x3 = e*cos(3*theta) + R*cos(theta + 2*(2*pi/3)) #rotor point 3
    y3 = e*sin(3*theta) + R*sin(theta + 2*(2*pi/3)) #rotor point 3

    #grab the rotor points and add them to the corresponding array
    X1[index]=x1 
    Y1[index]=y1
    X2[index]=x2
    Y2[index]=y2
    X3[index]=x3
    Y3[index]=y3



# set up the figure and subplot
fig = plt.figure()
ax = fig.add_subplot(111, aspect='equal', autoscale_on=False, xlim=(-10,10), ylim=(-10,10))
ax.set_title('Rotary Engine Animation')
ax.grid()
ax.axes.xaxis.set_ticklabels([])
ax.axes.yaxis.set_ticklabels([])

ax.plot(X_housing,Y_housing, lw=2, color='k') #draw the rotor housing



# initialization function
def init():
    points = [[x1, y1], [x2, y2], [x3, y3]]
    triangle = plt.Polygon(points)
    ax.add_patch(triangle)
    return triangle,

# animation function
def animate(i):
        points = [[X1[i], Y1[i]], [X2[i], Y2[i]], [X3[i], Y3[i]]]
        triangle = plt.Polygon(points, facecolor='darkred', alpha=0.5, linewidth=2, edgecolor='firebrick')
        ax.add_patch(triangle)
        return triangle,

# call the animation
ani = animation.FuncAnimation(fig, animate, init_func=init, frames=len(Y1), interval=40, blit=True, repeat=False)
## to save animation, uncomment the line below. Ensure ffmpeg is installed:
## ani.save('rotary_engine_animation.mp4', fps=30, extra_args=['-vcodec', 'libx264'])

#show the animation
plt.show()

