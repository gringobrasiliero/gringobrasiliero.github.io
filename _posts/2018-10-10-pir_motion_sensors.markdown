---
layout: post
title:      "PIR Motion Sensors"
date:       2018-10-10 14:09:53 +0000
permalink:  pir_motion_sensors
---



This week, I created software for a door greeter that is now being used at the Coder School, to greet our students when they come into the door. I have to say that I am very proud of what I was able to accomplish, and I am now seeing the software that I have developed being used on a day to day basis. Seeing my software put into action is an amazing feeling.

The software that I did develop was in Python, and I used the gpiozero module, as well as pygame. I used the gpiozero module to respond to changes from the motion detector, which was connected to a Raspberry Pi. 


![I want my data now](https://maker.pro/storage/xO4cooX/xO4cooX8woFXbeNrsRGK4U0cBbvLJgZxKWwrJrOX.jpeg)

When you supply power to the motion detector from the breadboard, the motion detector looks for emmitted infared energy. As soon as it does, it supplies 5V of power through the output, which you connect to GPIO pin 4. 

When you are using the GPIO pins in your program, you have to assign the pin number to a variable.

```
from gpiozero import MotionSensor

pir = MotionSensor(4)

```

After you import the module, and assign a pin number to the motion sensor, you are able to use it in the code. 

```
                if pir.motion_detected:
                    pygame.mixer.music.play()
                    print('Coder Detected. Greeting Coder.')
                 
	```


I also used the Pygame module in order to display the Coder School Logo, and have it spin on the screen when the sound is playing. 

```
  if pygame.mixer.music.get_busy() == True:
            image = pygame.transform.rotate(image_orig, angle)
            angle+=2.25
	```
	
	If the pygame music mixer is playing, the image will transform, and change the angle of the picture at each iteration of the loop. 
	
	Seeing this project in action at the Coder School is a wonderful experience, and seeing it in action, I am inspired to release updates on it to further improve the functionality of the program. 
	
	If you would like to take a look at the repo, or even use the software yourself, feel free! 
	
	
https://github.com/gringobrasiliero/CoderSchoolMonitor




