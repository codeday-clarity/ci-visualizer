# Deployment

## Build the Docker images and run the containers locally

- Build and start with `./deployment/dockerStart.sh`
- Check running containers with `docker ps`. There is a column in the default output for the name(s) of containers.
- Stop with `./deployment/dockerStop.sh`
- Check with Docker images are created with `docker image ls`
- Look at Docker container logs with `docker logs <container name>`. For example, `docker logs flask-backend`.

## Push Docker images to the DockerHub registry

- Build production images and push them to DockerHub `./deployment/deployToDockerhub.sh`

## Run the production app on EC2

- Run `./deployment/ec2/deployToEC2.sh`, which puts the installation script onto the box.
- SSH into the ci-visualizer machine with `ssh -i deployment/ec2_key.pem ubuntu@app.ci-visualizer.com` and run
`./dockerStartEC2.sh`

## Notes on infrastructure

- `app.ci-visualizer.com` points to the same IP address as `builds.ci-visualizer.com`.
- Having everything run on the same host works because Jenkins runs on host port 8080, whereas the app runs on host port
  80, which makes the app accessible in the browser from the url https://app.ci-visualizer.com.