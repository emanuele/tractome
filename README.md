tractome
========

Tractome is an interactive clustering-based 3D tool for exploration and segmentation of tractography data.

Tractome is an interactive tool for visualisation, exploration and segmentation of tractography data. It supports neuroanatomists and medical doctors in their study of white matter anatomical structures from diffusion magnetic resonance imaging (dMRI) data. Unlike previous systems for tractography segmentation, Tractome is a computer-assisted tool in which the user interacts with a summary of the tractography instead of the whole set of streamlines. The summary is generated by clustering the tractography into a desired number of clusters, usually in the order of tens or one hundred. The summary shows only one representative streamline for each cluster, so that it is easier to interact with them in the 3D scene. The user can then iteratively select the representative streamlines of interest and re-cluster the associated sets or streamlines into smaller ones in order to incrementally reveal details of the anatomical structure of interest. The interaction is powered by novel efficient algorithms for fast clustering.  Tractome is written in Python language and it supports the TrackVis format and the DiPy format for tractography files.


Dependencies
------------

* pyglet : http://www.pyglet.org , provides the Python bindings to OpenGL.
* fos : https://github.com/fos/fos.git , provides high-level OpenGL Actors for scientific visualisation
* PySide : http://qt-project.org/wiki/PySide , Python bindings for the Qt libraries.
* NiBabel : http://nipy.org/nibabel , provides read and write access to common medical and neuroimaging file formats.
* Dipy: http://www.dipy.org , provides tools for dMRI data analysis.
* scikit-learn : http://scikit-learn.org , provides the Mini-Batch K-means clustering algorithm.

The software is developed and tested on Ubuntu 12.04 LTS using the Neurodebian repositories. In Debian/Ubuntu systems the packages of the dependencies - with the exception of fos - can be installed with
```
apt-get install python-pyglet python-pyside python-nibabel python-dipy python-sklearn
```


To Run Tractome
---------------
```
ipython --gui=qt
run mainwindow.py
```

First of all load a structural image (```File -> Load Structural```). Then load a related tractography (```File -> Load Tractography```), either in TrackVis format or Dipy format. Tractome loads the file and then executes some pre-computations that may require some time - from seconds to a couple of minutes, depending on the size of the tractography. These pre-computations are saved in the same directory of the tractography, so the second time you load that tractography this step will be faster.

Tractome shows clusters of the whole tractography in the 3D scene by displaying the medoid streamline, called *representative*, of each cluster. You can interact with the clusters in several ways through their representatives:
1. Point one representative streamline with the mouse pointer and then press **P** to select/pick it. When selected it becomes white. You can select as many representatives/clusters as you like.
2. Expand the selected clusters in order to show their streamlines by pressing **E**. Press **E** again to toggle expansion.
3. When you are happy with your selection then press **Backspace** to remove all the clusters and streamlines not selected.
4. You can re-cluster the streamlines by clicking the button **Apply** in the bottom-left corner after choosing the desired number of cluster with the slider nearby.
5. Repeat the previous steps as many time as you want. If you want to step-back one step (undo) press **B**. To move one step forward (redo) press **F**.
6. You can save the steps done so far with ```File -> Save Segmentation```.
