# DOCKER CMD
The CMD instruction specifies the default command to run when a container is started from the Docker image. If no command is specified during the container startup (i.e., in the docker run command), this default is used. CMD can be overridden by supplying command-line arguments to docker run.

CMD is useful for setting default commands and easily overridden parameters. It is often used in images as a way of defining default run parameters and can be overridden from the command line when the container is run. 

For example, by default, you might want a web server to start, but users could override this to run a shell instead:

```bash
CMD ["apache2ctl", "-DFOREGROUND"]
```
Users can start the container with docker run -it <image> /bin/bash to get a Bash shell instead of starting Apache.  

# DOCKER ENTRYPOINT
The ENTRYPOINT instruction sets the default executable for the container. Any arguments supplied to the docker run command are appended to the ENTRYPOINT command.

Note: Use ENTRYPOINT when you need your container to always run the same base command, and you want to allow users to append additional commands at the end. One caveat is that ENTRYPOINT can be overridden on the docker run command line by supplying the --entrypoint flag.

ENTRYPOINT is particularly useful for turning a container into a standalone executable. For example, suppose you are packaging a custom script that requires arguments (e.g., “my_script extra_args”). In that case, you can use ENTRYPOINT to always run the script process (“my_script”) and then allow the image users to specify the “extra_args” on the docker run command line. You can do the following:

```bash
ENTRYPOINT ["my_script"]
```
Combining CMD and ENTRYPOINT
The CMD instruction can be used to provide default arguments to an ENTRYPOINT if it is specified in the exec form. This setup allows the entry point to be the main executable and CMD to specify additional arguments that can be overridden by the user.

For example, you might have a container that runs a Python application where you always want to use the same application file but allow users to specify different command-line arguments:

```bash
ENTRYPOINT ["python", "/app/my_script.py"]
CMD ["--default-arg"]
```
Running docker run myimage --user-arg executes python /app/my_script.py --user-arg.

