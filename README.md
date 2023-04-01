# Todo App manage with Docker
Setting up and using docker on a node.js todoapp

Create a file named Dockerfile in the same folder as the file package.json with the following contents.

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]

Please check that the file Dockerfile has no file extension like .txt. Some editors may append this file extension automatically and this would result in an error in the next step.

If you haven't already done so, open a terminal and go to the app directory with the Dockerfile. Now build the container image using the docker build command.

docker build -t getting-started .

This command used the Dockerfile to build a new container image. You might have noticed that a lot of "layers" were downloaded. This is because we instructed the builder that we wanted to start from the node:18-alpine image. But, since we didn't have that on our machine, that image needed to be downloaded.

After the image was downloaded, we copied in our application and used yarn to install our application's dependencies. The CMD directive specifies the default command to run when starting a container from this image.

Finally, the -t flag tags our image. Think of this simply as a human-readable name for the final image. Since we named the image getting-started, we can refer to that image when we run a container.

The . at the end of the docker build command tells that Docker should look for the Dockerfile in the current directory.

# Starting an App Container

Now that we have an image, let's run the application! To do so, we will use the docker run command (remember that from earlier?).

Start your container using the docker run command and specify the name of the image we just created:

docker run -dp 3000:3000 getting-started

Remember the -d and -p flags? We're running the new container in "detached" mode (in the background) and creating a mapping between the host's port 3000 to the container's port 3000. Without the port mapping, we wouldn't be able to access the application.

After a few seconds, open your web browser to http://localhost:3000. You should see our app!