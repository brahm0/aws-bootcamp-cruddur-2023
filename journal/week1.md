# Week 1 — App Containerization
## Create a new GitHub repo.
i didn't create a new github repository since we are working in the 'main'.  

## Configure Gitpod.yml configuration, eg. I’m VSCode Extensions
I configured the file as shown in the video during the live stream. To be candid, i was just following the steps Andrew was taking. I didn't fully understood what i was doing.

## Clone the frontend and backend repo.

## Explore the codebases

## Ensure we can get the apps running locally
Again i was able to achieve this by following the video steps.

## Write a Dockerfile for each app.
Docker file was written for each app as shown in the video.

## Ensure we get the apps running via individual container.

## Create a docker-compose file.
Docker-compose file was made.

## Ensure we can orchestrate multiple containers to run side by side.

## Mount directories so we can make changes while we code

# HOMEWORK : Implement a health check in the Docker compose file.

##  i will implement and Configure the health check using our already set compose file byadding the lines below to our docker-compose file.

version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
        healthcheck:
      test: curl --fail -s http://localhost:4567/ || exit 1
      interval: 1m30s
      timeout: 10s
      retries: 3
    volumes:
      - ./backend-flask:/backend-flask
      
