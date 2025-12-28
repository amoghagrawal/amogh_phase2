# Day 14: Containers - DoorDasher's Demise

> It seemed as the sun rose this morning, it had already been decided that today would be another day of chaos in Wareville. At least that’s the feeling all the folks at “DoorDasher” got. DoorDasher is Warevilles local food delivery site, a favourite of the workers in The Best Festival Company, especially on long days when they get home from work and just can’t bring themself to make dinner. We’ve all been there, I’m sure. 

## Solution

- In the machine, we run `docker ps` to see the containers
- To interact with the deployer container we run the command `docker exec -it deployer bash`
- We recover the app by running the recovery script from `sudo /recovery_script.sh` in the app directory
- We can use the cat command to directly get the flag from `/flag.txt`
- For the bonus question, the flag is directly hidden in plain site in red colour on the news website

## Objectives

### What exact command lists running Docker containers?
> docker ps

### What file is used to define the instructions for building a Docker image?
> Dockerfile

### What's the flag?
> THM{DOCKER_ESCAPE_SUCCESS}

### Bonus Question: There is a secret code contained within the news site running on port 5002; this code also happens to be the password for the deployer user! They should definitely change their password. Can you find it?
> DeployMaster2025!

## Concepts learnt:

- Learn how containers and Docker work, including images, layers, and the container engine
- Explore Docker runtime concepts (sockets, daemon API) and common container escape/privilege-escalation vectors