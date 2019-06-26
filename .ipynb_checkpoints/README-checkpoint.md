![logo](docs/assets/images/logo_horizontal.png)

## About

TINerator is a tool for the fast creation of extruded and refined meshes from
DEM and GIS data, developed at Los Alamos National Laboratory to aid in
hydrogeological simulations.

TINerator allows a user to define a bounding box of latitude/longitude
coordinates, a shapefile, or a local DEM, and generate a surface or volume mesh.

The mesh will have the topology of the DEM, along with user-defined material IDs
and depths for stacked layers. Further, TINerator performs watershed delination
on the defined DEM and refines the mesh’s elements around the feature to a
user-defined length scale.

TINerator comes with a host of 2D and 3D visualization functions, allowing the
user to view the status of the mesh at every step in the workflow.
In addition, there are geometrical tools for removing triangles outside of a
polygon, generating quality analytics on the mesh, adding cell- and
node-based attributes to a mesh, and much more.

## Documentation


For installation instructions and API usage,
refer to the [documentation](https://raw.githack.com/lanl/LaGriT/tinerator/html/index.html) and [tutorials](https://raw.githack.com/lanl/LaGriT/tinerator/html/tutorials/index.html)
or by navigating to `docs/index.md`.

## Docker

A [Docker image](https://hub.docker.com/r/ees16/tinerator) can be pulled and run via:

- download the image

`docker pull ees16/tinerator`

- run it in docker. You can choose to mount your local volume to the image.

`docker run -v LOCAL_DIR:/home/jovyan/work -p 8888:8888 ees16/tinerator:latest`

the default is running in Jupyter notebook, but you can launch Jupyter lab instead:

`docker run -v LOCAL_DIR:/home/jovyan/work -p 8888:8888 ees16/tinerator:latest jupyter lab`

If the notebook does not open, try to paste one of the links (similar) to the browser:

`http://(a65d926e15ba or 127.0.0.1):8888/?token=44dbc7fd4da2598a8797ff0657721b74589e9444315f5802`

![final attribute](docs/assets/images/examples/attribute_final.png)

## run jupyter notebook using Shifter on NERSC

Run docker image on [Shifter](https://docs.nersc.gov/programming/shifter/overview/)

- download docker image 

    ```
    shifterimg -v pull docker:ees16/tinerator:latest
    ```

- create kernel spec file `kernel.json` and put it under `~/.local/share/jupyter/kernels/shifter-jupyter/kernel.json`

```
{
    "argv": [
        "shifter",
        "--image=ees16/tinerator:latest",
        "/opt/conda/bin/python",
        "-m",
        "ipykernel_launcher",
        "-f",
        "{connection_file}"
    ],
    "display_name": "shifter-jupyter",
    "language": "python"
}
```

note: python path here being the location in the container

- go to Jupyterhub and choose `shifter-jupyter` from the kernels
