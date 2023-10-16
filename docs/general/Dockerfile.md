---
share: "true"
---

A dockerfile is a file that defines the steps needed to create an image and run it. 

Each instruction in the [[Dockerfile|Dockerfile]] creates a "layer" in the image. 
Therefore, when some changes are made, only the relevant "layers" are rebuilt. 

The [[Dockerfile|Dockerfile]] is **NOT** the [[Docker Image|Docker Image]]. It is just a set of instructions to build and run the [[Docker Image|Docker Image]]. 

`docker build` created the [[Docker Image|Docker Image]] from the [[Dockerfile|Dockerfile]]