# Low-Data-Spiral-CT-Reconstruction
This spiral CT slice reconstruction program with low data amount is based on MATLAB. Realized CT image reconstruction of specific slice with only 1/10 of the data by increasing the pitch and the maximum range of the projection angle of neighboring slices.
## Dataset
The dataset is the sinograms of 190 axial locations. For simplicity only the 140th slice will be considered in this practice. Dataset is too large to upload.  
Link to dataset 1: 链接：https://pan.quark.cn/s/4e9b368109f3 提取码：fBcN  
Link to dataset 2: https://drive.google.com/file/d/104Qdl05H9oZic1PdJv16raogalg0fLLN/view?usp=drive_link  
Contact me via accesses in homepage to get dataset if these links are expired. 
## Demonstration
### Test 1
**Using the raw data in ‘CT projections.mat’, preview the sinogram for 140th axial slice. The sinogram will have dimensions 380 (projection coordinate) x 180 (projection angle). For the double for loop shown in the script fill in the missing line to form the 140th sinogram and save the image as ‘TASK_1_CT_SINOGRAM.png’. Alternatively you can delete the for loop and directly index the data you need from within the projections. Complete a filtered and an unfiltered backprojection and save the images as 'TASK_1_CT_FILTERED_BP.png' and 'TASK_1_CT_UNFILTERED_BP.png' respectively.**
#### Result of test 1
![Image](https://github.com/weiyi-li/Low-Data-Spiral-CT-Reconstruction/blob/main/Image/Test1.png)  
The sinogram for 140th axial slice is directly fetched from the projection data with 180° projection
angle. Unfiltered backprojection is obtained by performing inverse radon transform on the 140th slice
of the sinogram with linear interpolation. The content of unfiltered backprojection is glowing and the
halo blurs the display of organ structure. By removing the interpolation, the backprojection can be
filtered and the organ structure is clearly shown with detailed features including the colour,shape and
textile of every section.

### Test 2
**Calculate the sinogram, filtered and unfiltered backprojections for the 140th slice using only 1/10th of the projection data such that only neighbouring angles are used, i.e. a wedge shaped range of projection angles. Save your three images with similar names as for Task 1, substituting '1' for '2' in the file names.**
#### Result of test 2
![Image](https://github.com/weiyi-li/Low-Data-Spiral-CT-Reconstruction/blob/main/Image/Test2.png)  
Since only 1/10 projection data and neighbouring projection angles are used, the sinogram for 140th
axial slice covers a 18°projection angle ranging from 1°to 18°, which is only 1/10 the length on angle
axis. Same as Task 1, unfiltered backprojection is obtained by performing inverse radon transform on
the 140th slice of the sinogram with linear interpolation, but only for the first 18°compared to Task 1.
By filtering the backprojection, the glow can be reduced. Unfiltered and filtered backprojections give
little clear information since the projection angle is quite limited for CT reconstruction of the whole
image.

### Test 3
**Calculate the sinogram, filtered and unfiltered backprojections for the 140th slice using only 1/10th of the projection data such that these angles are equally spaced over the available projections. Save your three images as above.**
#### Result of test 3
![Image](https://github.com/weiyi-li/Low-Data-Spiral-CT-Reconstruction/blob/main/Image/Test3.png)  
The CT reconstruction for 140th axial slice is briefly achieved using 1/10 of the projection data by
equally spacing the angles. Compared to Task 2, the lines in sinogram show that 18 angles are
distributed equally with interval of 10°, spanning from 1°to 171°, which is nearly the full range of the
180° projection angle. Backprojections are obtained by rotating on 18 equally distributed angles
spanning over a full range, which covers much more information than backprojections in Task 2.
Backprojections briefly show the structure, but the rays still indicate the limitation of using only 1/10
of data.

### Test 4
**Simulate the acquisition of a spiral CT dataset and reconstruct the sinogram, filtered and unfiltered backprojections for the 140th slice. You should use a pitch of 18, i.e. there are 18 neighbouring projection angles acquired for each axial position. Due to the axial translation of the scan bed the next 18 angles will be acquired for the neighbouring axial position, i.e. only 10th of the available data is used for the reconstruction of the 140th slice, but over different axial positions. Save your images as above. Explain your approach to this task in the Word document as well as commenting on the result.**
#### Result of test 4
![Image](https://github.com/weiyi-li/Low-Data-Spiral-CT-Reconstruction/blob/main/Image/Test4.png)  
The translation axis is defined as k and should be considered in spiral CT reconstruction. To reconstruct
the 140th slice using only 1/10 of data in spiral CT, the 140th slice should be reconstructed by the actual
data acquired from the rotating 18°angles on the 140th slice and other 9 neighbouring slices. Following
this procedure, 10 slices from 135th slice to 144th slice are involved in the reconstruction of 140th slice
and each slice contributes to 1/10 of reconstructed data, which is 18°.  
Therefore, I defined a loop with axes i, j and k representing the angles, distance and the slice number.
Angle i has an initial range of 1 to 10°, and it increases by a progressive value p_plus, which adds 18°
per slice. When it reaches 180°, all ten slices are covered, which enables the reconstruction of the
140th slice using just 1/10 of data.  
It can be found that the sinogram of reconstructed 140th slice is evenly combined by 10 partial
sinograms from different slices, each one takes up 1/10 of data. The quality of backprojection is fine
but the discontinuity at the junction of neighbouring partial sinogram may resulted in some shadow
points
