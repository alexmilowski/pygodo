# Converting OWL to OBO via Robot

Ontologies expressed in an OWL format can be converted to OBO format with
a [tool called robot](http://robot.obolibrary.org/convert). While you can
download the Java-based application, this directory contains a simply
containerized version that avoids installing any of the Java or Robot
toolchain.

## Preparing the image

You can build the docker image for robot by
```sh
cd robot
docker build -t robot .
```

## Using the image

The command can be invoked with a simple docker run command:

```sh
docker run -it --rm robot
```

You should map your local directory containing your files to the `/home`
directory for processing:

```sh
docker run -it --rm -v /home:`pwd` robot
```

## Converting OWL to OBO

1. Download the OWL formatted ontology to your machine:

    ```sh
    curl -O https://raw.githubusercontent.com/CIDO-ontology/cido/master/src/ontology/cido.owl
    ```

1. Run the robot convert command, ensuring you map the correct directory:

    ```sh
    docker run -it --rm -v `pwd`:/home robot convert --check false --input cido.owl --output cido.obo
    ```

    Note: The `--check` option may or may not be necessary. See the robot documentation for more information.