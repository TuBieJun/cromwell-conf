# cromwell-conf
**my.cromwell.examples.conf**  
Local backbend support docker soft-link.  
The import points are "docker.allow-soft-links" set to "true" and mount the dictory as need to the container in "submit-docker".
```
docker.allow-soft-links = true # set "docker.allow-soft-links" as "true"
localization = [ "soft-link"]
submit-docker = """
        docker run \
          --rm -i \
          ${"--user " + docker_user} \
          --entrypoint ${job_shell} \
          -v ${cwd}:${docker_cwd} \
          -v /data/liteng/:/data/liteng/:ro \ # mount the dictory to the container
          ${docker} ${docker_script}
        """
glob-link-command = "ln -sL GLOB_PATTERN GLOB_DIRECTORY"
```
Usage
```
java -Dconfig.file=my.cromwell.examples.conf -jar cromwell.jar run my.wdl -i my.inputs.json
```
**volcano.conf**  
support k8s+volcano+oss(alibaba)+nas(alibaba)
