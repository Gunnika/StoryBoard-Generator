# Story Visualization Generator

## Overview

This project introduces an innovative approach to generating visualizations from extensive text narratives. While existing models like Stable Diffusion and DALL-E-2 show promise in text-to-image synthesis, their word constraints limit their effectiveness for detailed content such as film scripts or educational materials. In response to this, we present an unsupervised, fully automatic pipeline that segments longer stories into meaningful scenes, then summarizes them to serve as prompts for image generation.

## Project Structure

The high-level project structure is organized as follows:

- **data:** [Data](https://github.com/aditi098/CSE_291_GenAI/tree/main/data)
  
- **generated_images:** Directory for storing generated images.

- **src:** Source code directory.

  - **eval.ipynb:** code for clip score and image coherency evaluation.

  - **generate_test_images.ipynb:** Jupyter notebook for generating some test images.
    
  - **image_generation.py:** Python script for image generation using text2img diffusion models.
    
  - **main.py:** Main Python script for project execution.

  - **prepare_baseline_data.ipynb:** Jupyter notebook for preparing baseline data.

  - **scrapper.ipynb:** code for scraping dataset from the source website(americanliterature.com).

  - **segmentation.py:** Python script for segmentation of stories.

  - **story_cleaner.py:** Python script for preprocessing text in stories.

  - **utils.py:** Utility functions for the project.
    
  - **install.sh** Script to install all requirements for this project.

## Architecture
![arch4](https://github.com/Gunnika/StoryBoard-Generator/assets/34855465/11cb2f48-845b-427c-8f1b-a40711926638)


The above diagram is an end-end pipeline for our final architecture. The raw story text is segmented into multiple segments using the TextTiling Segmentor, each of these segments are summarised into a one line summary by DistillBART-xsum. For the first summary, an image is generated using Text-to-image Stable Diffusion. The second image is conditioned on the first image to maintain some consistency in the theme. From thereon, the generated image is conditioned on the image with highest prompt similarity. Finally, two evaluations scores are calculated, one based on the text-image similarity using CLIP to evaluate if the images correspond to the prompts. The second score is used to evaluate the coherency in the storyboard, by doing a pairwise-cosine similarity evaluation on the image embeddings and averaging over them

To run the project

1. Clone the github repo 
```
   git clone https://github.com/aditi098/CSE_291_GenAI.git
```
2. Set up requirements
    ```
    cd src
    ```
   Give permission to your shell script.
   ```
   chmod +x install.sh
   ```
  Run the shell script
   ```
   ./install.sh
   ```

4. Run
   ```
   python src/main.py
   ```
