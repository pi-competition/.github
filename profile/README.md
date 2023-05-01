# TEAM PANIC

![image](https://avatars.githubusercontent.com/u/116845337?s=200&v=4)

## Introduction

For society to adopt sustainable technologies, we must solve the biggest problems facing them, and make them more desirable. In the context of electric vehicles, we considered one issue in particular: range.

Our team name, PANIC, stands for Pathfinding Automobile Network of Induction Charging. The idea involves the use of wireless charging to transfer power to vehicles, which reduces the hours spent stationary using normal charging points. Initially, we’ll introduce wireless capability at common stopping points like traffic lights or parking spaces. However, this could eventually be expanded to entire motorways - dedicated EV lanes, providing constant power, would allow cars to travel across entire countries without a single stop.

The advantage of creating a smart network is that many technologies can be integrated together, including self-driving systems and traffic management. Staying within budget, our system utilises a single car navigating a dynamically mapped track. New tracks are taped onto the floor, which are seamlessly detected by the control pi’s camera and used to update the car’s pathfinding. The control pi identifies the car’s position, so it can send it commands. Tracks can start/end at “traffic lights” (a wireless charging pad), or the pad can be used externally as a “parking space”. This model could expand to an entire fleet of cars on a whole road network. On larger scales, GPS and OpenStreetMaps would substitute for the camera, a network of toggleable powered zones for the charging pad.

The car uses a small lithium ion battery connected to a TP4056 charge controller to allow the qi-based wireless coil to supply power. The onboard Pi 3b or Zero needs regulated 5v power, ~3A/~1A respectively - to increase reliability, a Pi Sugar power module was retrofitted in the place of a DC/DC step-up converter. The entire car sits in a custom 3d-printed chassis. A tripod positions the Pi 4 and camera above the taped out track, allowing it to control the system from above.

We have created a range of tools for a versatile system. One tool, ‘radar’, searches for the presence of devices on a network and assigns unique identifiers. The controller takes an image with no cars, uses Aruco tags to find the track, and filters colours to determine roads/intersections. An event loop determines the position and direction of the car’s tag, decides which nodes it should travel to, and interfaces with it via RESTful http calls.

The car knows where it is, where it should go, and its orientation. It can thus establish an angle correction, and updates the speeds of the motors. Collisions are avoided by the controller, which splits up the nodes cars can visit into zones. Only one car can occupy a zone at once, so the controller instructs cars to stop and wait if the zone ahead is blocked. An admin page on [teampanic.eu.org](https://teampanic.eu.org) can remap the track, reboot, start or stop the car(s), and view data from them.

## Useful Links

- [Website](https://teampanic.eu.org)
- [Website (beta)](https://staging.teampanic.eu.org)
- [Grafana](https://grafana-pi01.ben-services.eu.org/d/tUwKjoiRz/dev-stuff?orgId=1&search=open&query=folder:current) (only available when system is online)
