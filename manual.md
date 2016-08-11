---
layout: default
title: Usage Instructions
category: info
tags: manual
---

## Table of Contents

* [Running Shapeworks Studio](#running-shapeworks-studio)
    * [Data](#data)
    * [Groom](#groom)
    * [Optimize](#optimize)
        * [Optimize](#optimize-1)
        * [Reconstruction](#reconstruction)
    * [Rendering Window](#rendering-window)
    * [Analysis](#analysis)
    * [Preferences](#preferences)
    * [File Menu](#file-menu)
* [Known Issues](#known-issues)
* [Contact and Bug Reports](#contact-and-bug-reports)

# Running Shapeworks Studio
Studio runs with no command-line arguments. 
<br/><br/>
You Should have a Qt window that looks similar to the one below.
<br/><br/>
<img src="https://sciinstitute.github.io/shapeworks.pages/images/Application.png" width=300px>
<br/><br/>
The application has tools on the left, the rendering window, 
view options on the lower bar, a small file menu, and a
preferences dialog.

## Data
<img src="https://sciinstitute.github.io/shapeworks.pages/images/DataPanel.png" align="right" hspace="20">
This tool tab displays the images (volume files in NRRD format) that have been loaded. 
You can select the image files to load by either clicking the blue "+" button at the bottom, 
or going to *File -> Import Images...* <br/> Your images will appear on the display once loaded.
<br/><br/>
You can delete images by selecting the image of choice and clicking the red "x" button at the bottom. If only one image 
is loaded, it may still display when it is deleted. It will be replaced by the next image load. 
<br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Groom 
<img src="https://sciinstitute.github.io/shapeworks.pages/images/Groom.png" align="right" hspace="20">
Once more than 1 image is loaded, the preprocessing step, "groom" is next. You can select several options for grooming.
<br/><br/>
*Center* This option attempts to allign the segmentations to a common center if they aren't the same sizes.
<br/><br/>
*Isolate* This option isolates the foreground.
<br/><br/>
*Fill Holes* This option fills any existing holes in the segmentations.
<br/><br/>
*Pad* This option adds a padding around the shapes. This can help when a larger number of correspondance points are needed.
You can select what amount is appropriate for the optimization step.
<br/><br/>
*Antialias* This option antialiases the binary segmentation. You can select the number of antialias iterations.
<br/><br/>
*Blur* This option blurs the distance transform to get rid of high-frequency artifacts. You can choose an appropriate sigma
for the blurring.
<br/><br/>
*Fastmarching* This option computes a distance transform of the surface using the fastmarching method.
<br/><br/>
*Run Groom* Click this when you are ready for grooming. This step takes some time. Output is put into a 
ShapeWorksStudioTools.log file next to the executable. A progress indicator shows the tool is working.
<br/><br/>
*Skip* Click this if you believe your data to already be pre-processed to your liking.
<br/><br/>
*Restore Defaults* Click this to restore all values to their program defaults.
<br/><br/>

## Optimize

### Optimize
<img src="https://sciinstitute.github.io/shapeworks.pages/images/Optimize.png" align="right" hspace="20">
Once the grooming step is complete, you can run the optimize step. The Optimize table has 5 parameters per split.
<br/><br/>
*Number of Particles* Specifies the number of particles to be used to represent each shape in the ensemble.
Keep in mind that the actual particle count will be a power of "2" >= the provided number.
<br/><br/>
*Relative Weighting* The relative weighting of terms in the two-term cost function used for the optimization.  
<br/><br/>
*Starting/Ending Regularization* These options determines the regularizations on the covariance matrix for the shape-space 
entropy estimation.
<br/><br/>
*Iterations per Level* Specifies the number of iterations to run between successive particle splits during an 
initialization phase. This allows the particle system at a given granularity to converge to a stable state 
before more particles are added.
<br/><br/>
*Decay Span* The parameters RegStart, RegEnd, and DecaySpan define an "annealing" type optimization,
where the minimum variance starts at RegStart and exponentially decreases over DecaySpan to the      
RegEnd value.  This is usually the same number as iterations.
<br/><br/>
*Run Optimize* Click this when you are ready for optimizing. This step takes a while.
A progress indicator shows the tool is working.
<br/><br/>

### Reconstruction
*Max Angle* This is the greatest angle between particle normals (from respective samples)
permitted to label the particle "good", or useful for reconstruction.
<br/><br/>
*Mesh Decimation* The "PreView" library code can decimate the number of triangles to the value 
set here. The default is "0.30" or 30 percent.
<br/><br/>
*# Clusters* To help speed up reconstruction, you can define how many samples/Clusters
are used to warp data into mean space. "0" indicates to use all of the samples.
<br/><br/>
*Run Reconstruction* Click this to run the reconstruction step. If it fails, the VTK
triangles are used instead. You can re-run with different Optimizations as needed.
<br/><br/>
*Restore Defaults* Click this to restore all values to their program defaults.
<br/><br/>

### Analysis
<img src="https://sciinstitute.github.io/shapeworks.pages/images/Analysis.png" align="right" hspace="20">
Here is where all the statistical options are available to the user.
<br/><br/>
*All Samples* Display all of the image segmentation samples on the screen.
<br/><br/>
*Single Sample* Display only one sample. You can select a particular number, or click "median" to display the shape 
that is the computed median of all the shapes.
<br/><br/>
*Mean* Display the computed mean of the shapes.
<br/><br/>
*PCA* Display the computed shape from an eigen value and a standard deviation.
<br/><br/>
*Std.Dev.* Slide the slider back and forth to display the computed shape with various standard deviations.
<br/><br/>
*Animate* Check this box to watch the shape morph between various standard deviations automatically. Depending on 
the machine running the application, the number of samples, and the size of the samples, the animation may be 
slow at first while building and caching the meshes. You can select the caching, memory, and threading options
in the Preferences. Changing the number of neighbors, spacing, and smoothing options in preferences also affects
meshing time and quality.
<br/><br/>
*Mode* This selects the ordered eigen vector and eigen values from the statistical analysis. There are #samples - 1 modes.
The higher the mode, the less variance with the standard deviations. Usually the first two modes contain the most variance 
between shapes.
<br/><br/>
*Log Scale vs. Linear Scale* The bar graph can be plotted in either log or linear scaling. The graph shows the eigen values
in decreasing values to depict statistical relevancy.
<br/><br/>
*Regression* This option is not yet available.

## Rendering Window
The render window has a few shortcuts to viewing options.
<br/><br/>
<img src="https://sciinstitute.github.io/shapeworks.pages/images/Render.png" align="center">
<br/>
From left to right, here are the rendering options.
<br/><br/>
*Autoview* Reset the view to fit the samples. This only affects zoom and translation.
<br/><br/>
*Show Glyphs* Toggle whether to show the glyphs for the coorespondence points.
<br/><br/>
*Glyph Quality* This slider changes the quality of the coorespondance points glyphs. This is sync'd with the render window
shortcut option.
<br/><br/>
*Glyph Size* This slider changes the size of the coorespondance points glyphs. This is sync'd with the render window
shortcut option.
<br/><br/>
*Glyph options* Click the down arrow to resize the glyphs or select the quality of the glyphs.
<br/><br/>
*Show isosurface* Toggle whether to view the surface representing the shape. 
<br/><br/>
*View mode drop-down* This drop-down gives 3 options for view mode. Original is the binary segmentation. You must
have loaded images for this option to be available. Groomed is for the distance transform view. You must  
run the groom step for this to be available. Reconstructed is for the calculated shape based on the set of 
coorespondance points. You must run the optimize step for this to be available.
<br/><br/>
*Center* Center the samples automatically to align. This is useful if original samples aren't the same size.
<br/><br/>
*Zoom* This slider allows the user to zoom in or out to view more/less samples. This is mainly useful in the "All Samples"
mode of the analysis tool. Zoom is automatically selected as a user switches between analysis modes.

## Preferences
<img src="https://sciinstitute.github.io/shapeworks.pages/images/pref-general.png" align="right" hspace="20">
*Color Scheme* Select the color scheme for the rendering window.
<br/><br/>
*PCA Range* This is the amount of standard deviation to reach on the +/- ends of the PCA Slider.
<br/><br/>
*Number of PCA Steps* This determines how many steps between +/- PCA Range to take for visualization.
<br/><br/>
*Enable Caching* To speed up mesh animation, you can cache the meshes into system memory to load as needed.
<br/><br/>
*Caching Epsilon* How sensitive the caching is. The smaller the epsilon, the more meshes that will be cached, even if
they are very similar. If this is too high, large mesh differences might be ignored.
<br/><br/>
*Memory to Use* Select the amount of system memory to use for caching. Turn this down if your machine's memory 
is bogged down from the program.
<br/><br/>
*Parallel Reconstruction* Select the amount of threads to fire (up to system hardware core max) to run while 
building meshes. This speeds reconstruction, theoretically.
<br/><br/>
*Restore Defaults* Click this to restore all options to the program's default values. Options are saved and reloaded
between application runs for convenience.
<br/><br/>
*OK* Click this when you are done changing options.
<br/><br/>

## File Menu
* Start a new project
* Open and save projects
* Set the data directory for where generated images will be written when a project is saved.
* Load new images
* Export a mesh reconstructed for samples, the mean, or a variance from the mean.
* Export the Eigen values or Eigen vectors from the sample statistics.
* Export the Particles per shape to text files.
* Export an XML parameter file to run a command line too on more images
* Open recent projects
* Quit the application.
<br/><br/>

# Known Issues
* On OSX, full screen mode has a widget bug visualization problem for the left panel. Future Qt releases may fix this.

# Contact and Bug Reports
Please email any questions to <a href="mailto:shapeworks-users@sci.utah.edu">shapeworks-users@sci.utah.edu</a> . If there problems or bugs, please report them using the <a href= "https://github.com/SCIInstitute/ShapeWorksStudio/issues" >issue tracker on GitHub</a>. This includes feature requests. Feel free to add improvements using git pull requests. 
