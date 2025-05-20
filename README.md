# DevOps

1-1 For which reason is it better to run the container with a flag -e to give the environment variables rather than put them directly in the Dockerfile?
Using the -e flag during docker run improves security and flexibility by allowing you to pass sensitive variables like passwords at runtime, instead of baking them into the image.

1-2 Why do we need a volume to be attached to our postgres container?
Docker containers are ephemeral and disappear after the container removal Mounting a volume ensures data persistence between container restarts or recreations by storing the database files on the host machine.

1-3 Document your database container essentials: commands and Dockerfile.
See dockerfile in the repository database. I built a database image and start a container with it

1-4 Why do we need a multistage build? And explain each step of this dockerfile.
We need a multistage build in order to reduce the size of the image and optimize it. Firstly we build a first version of image with JDK and after a new version with keeping only JRE and some files from the first version

1-5 Why do we need a reverse proxy?
The reverse proxy is used to manage client requests and forward them to the appropriate backend services.

1-6 Why is docker-compose so important?
Docker compose is important because it allows us to define and manage multiples container applications easily with a yml file.

1-7 Document docker-compose most important commands.
docker-compose build to build images docker compose -d up to start containers in detached mode

1-8 Document your docker-compose file.
See the document docker compose on the repository
