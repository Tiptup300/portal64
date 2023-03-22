# Portal64

A demake of Portal for the Nintendo 64.

## How to build

First, you will need to setup [Modern SDK](https://crashoveride95.github.io/n64hbrew/modernsdk/startoff.html).

After installing modern sdk you will want to also install

```
sudo apt install libnustd
```

Next, you will need to download Blender 3.0 or higher. Then set the environment variable `BLENDER_3_0` to be the absolute path where the Blender executable is located on your system.

<br />

You will need to install Python `vpk`.
```
pip install vpk
```

<br />

Install `vtf2png`, `sfz2n64`, and setup `skeletool64`.
```sh
echo "deb [trusted=yes] https://lambertjamesd.github.io/apt/ ./" \
    | sudo tee /etc/apt/sources.list.d/lambertjamesd.list
sudo apt update
sudo apt install vtf2png sfz2n64 mpg123 sox imagemagick
```

<br />

Setup and build skelatool64

```
cd skelatool64
./setup_dependencies.sh
make
```

<br />

You will need to install nodejs. You can use apt for this

```
sudo apt install nodejs
```

<br />

You then need to add the following files from where Portal is installed to the folder `vpk`.
```
portal_pak_000.vpk  
portal_pak_001.vpk  
portal_pak_002.vpk  
portal_pak_003.vpk  
portal_pak_004.vpk  
portal_pak_005.vpk  
portal_pak_dir.vpk
```

Finally, run `make` to build the project.

<br />


## Build with Docker


Build the Docker image.
```
docker build . -t portal64
```

<br />

Then build.
```sh
# Set the environment variable
BLENDER_3_0=/blender/blender

# Build using docker
docker run \
    -v /home/james/Blender/blender-2.93.1-linux-x64:/blender \
    -e BLENDER_3_0 -v /home/james/portal/portal64/vpk:/usr/src/app/vpk \
    -t -v /home/james/portal/portal64/docker-output:/usr/src/app/build portal64
```

<br />

Where `/home/james/Blender/blender-2.93.1-linux-x64` is the folder where Blender is located.

`/home/james/portal/portal64/vpk` is the folder where the portal `*.vpk` files are located.

`/home/james/portal/portal64/docker-output` is where you want the output of the build to locate `portal.z64` will be put into this folder.

<br />

## Current TODO list

- [ ] force placing auto portals when there is a conflict
- [ ] fix chell animation problem (fixed itself, investigate)
- [ ] rotate auto uv
- [ ] disable portal surfaces manually on some surfaces
- [ ] Portal not rending recursively sometimes
- [ ] Passing into a ceiling portal can sometimes mess with the player rotation
- [ ] Correct elevator timing
- [ ] Presort portal gun polygon order
- [ ] Camera shake
- [x] Elevator and door sounds
- [?] Skips audio sometimes
- [x] Signage should not always be on
- [x] sound effects for ball (portal_pak_dir/scripts/npc_sounds_energy_ball.txt)
- [x] first portal wall
- [x] the cube bounces the player
- [x] break constraint after large distance
- [x] prevent objects from pushing the player around
- [x] Stop looping sounds betwen levels
- [x] red light district
- [x] burn marks
- [x] close portal in elevator
- [x] keep stationary portal with fizzle grids
- [x] add more fizzle grids
- [x] checkpoint in elevator
- [x] preserve gun between test chambers
- [x] Finish up animation pieces (collider/portable surface/culling logic)
- [x] Implement pedestal button
- [x] Create piston animaiton test
- [x] Refactor physics to allow swept collision between two dynamic objects
- [x] Move constaints to be applied right before contact solving
