## Reflection

### How does Docker differ from a virtual machine?
- docker is just a container where the application is packaged. a vr is a whole operating system (like linux) running inside your operating system. Its much larger and slower. Those could be used when the application only works with a certain system like OS or Linux. Its much easier to just setup docker, however it only packeges the application and its dependancies. 

### Why is containerization useful for a backend like Focus Bear’s?
- Then all developers get the same setup. Docker will define all the exact versions of for example node.js thats needed for developement. This will ensure consistency and reliability throughout all developers for the project. 

### How do containers help with dependency management?
- The containers hold all the needed dependancies, so the software is not running on the current installed software on your pc. So if the backend is using node.js 20, its using this exact version from the docker container

### What are the potential downsides of using Docker?
- the learning curve. Extra system resourses are used and debugging becomes longer and more complicated. it also increases the setup complexity and storage space