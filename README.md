# TRELLIS2-on-RTX-5xxx
A quick setup guide on setting up TRELLIS.2 on Blackwell GPUs.

# Why?
Because I encountered a lot of erros during default install process on Debian 13. I solved them so you don't have to.

# A quick warning on RTX 5070 and other <16Gb GPUs
I was unable to run TRELLIS.2 on RTX 5070 due to lack of VRAM. Try TRELLIS instead (prev. version).

# How-to:
1. Get TRELLIS.2:
   ```
   git clone https://github.com/microsoft/TRELLIS.2.git
   ```
2. Modify following lines in setup.sh (lines 69-73):
   from
   ```
   if [ "$NEW_ENV" = true ] ; then
    conda create -n trellis2 python=3.10
    conda activate trellis2
    if [ "$PLATFORM" = "cuda" ] ; then
        pip install torch==2.6.0 torchvision==0.21.0 --index-url https://download.pytorch.org/whl/cu124
   ```
   to
   ```
   if [ "$NEW_ENV" = true ] ; then
    conda create -n trellis2 python=3.12
    conda activate trellis2
    if [ "$PLATFORM" = "cuda" ] ; then
        pip install torch==2.9.1 torchvision==0.24.1
   ```
3. Run installation script:
   ```
   . ./setup.sh --new-env --basic --flash-attn --nvdiffrast --nvdiffrec --cumesh --o-voxel --flexgemm
   ```
   You probably would encounter errors with following packages:
   ```
   flash-attn
   nvdiffrash
   nvdiffrec
   cumesh
   o-voxel
   flexgemm
   ```
   To solve them, you have to download Wheels for Python 3.12 from Releases tab on this repo manually and install them via 
   ```
   pip install /path/to/your/file.whl
   ```
4. Start the app in your TRELLIS.2 directory:
   ```
   python app.py
   ```
   If you see error about PIL and webp library, just run
   ```
   pip install Pillow=9.5.0
   ```
   
