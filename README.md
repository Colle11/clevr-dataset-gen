# CLEVR dataset generation

## Michele Collevati

This repo is a fork and rework of [CLEVR Dataset Generation](https://github.com/facebookresearch/clevr-dataset-gen) (viewed online on Thursday, 12/10/2023).  

This is the code to generate the CLEVR dataset.  

You can use this code to render synthetic images like this:  

<div align="center">
  <img src="images/example1080.png" width="800px">
</div>

All CLEVR dataset generation code was originally developed and tested on OSX and Ubuntu 16.04. We have modified some parts of CLEVR code according to our needs in Ubuntu 22.04.3 LTS.


## Dataset generation

We render synthetic images using [Blender](https://www.blender.org), outputting both rendered images as well as a JSON file containing ground-truth scene information for each image.

1. Install [Blender 3.6.4](https://download.blender.org/release/Blender3.6/).  

   Add Blender to the environment `PATH`. Add the following command to `~/.bashrc` pointing to the directory with Blender’s binary:  

   ```
   # Blender
   export PATH="/path/to/blender/directory:$PATH"
   ```

   Blender ships with its own installation of Python which is used to execute scripts that interact with Blender; you'll need to add the `image_generation` directory to Python path of Blender's bundled Python. The easiest way to do this is by adding a `.pth` file to the `site-packages` directory of Blender's Python, like this:  

   ```
   echo $PWD/image_generation >> $BLENDER/$VERSION/python/lib/python3.5/site-packages/clevr.pth
   ```

   where `$BLENDER` is the directory where Blender is installed and `$VERSION` is your Blender version.
2. You can then render some images like this:

   ```bash
   cd image_generation
   blender --background --python render_images.py -- --num_images 10
   ```

   If you have an NVIDIA GPU with CUDA installed then you can use the GPU to accelerate rendering like this:

   ```bash
   blender --background --python render_images.py -- --num_images 10 --use_gpu 1
   ```

   The results are saved in the `output` folder. After this command terminates you should have ten freshly rendered images stored in `output/images` like these:

   <div align="center">
     <img src="images/img1.png" width="260px">
     <img src="images/img2.png" width="260px">
     <img src="images/img3.png" width="260px">
     <br>
     <img src="images/img4.png" width="260px">
     <img src="images/img5.png" width="260px">
     <img src="images/img6.png" width="260px">
   </div>

   The file `output/CLEVR_scenes.json` will contain ground-truth scene information for all newly rendered images.

   You can find [more details about image rendering here](image_generation/README.md).


## Additional notes

1. Dataset scene files contain object bounding boxes.
