# face-recognition-pca-ann
This project implements a facial recognition system using Principal Component Analysis (PCA) and an Artificial Neural Network (ANN) for classification. It combines the concept of **Eigenfaces** with a neural network to recognize known and unknown individuals.

## Objective

Our goal is to:
- Extract dominant face features using PCA (Eigenfaces)
- Reduce dimensionality of the face data
- Train an ANN to classify faces based on these features
- Evaluate the effect of different numbers of principal components `k`
- Identify imposters not present in the training set

Paper reference on Eigenfaces:  
[https://sites.cs.ucsb.edu/~mturk/Papers/mturk-CVPR91.pdf](https://sites.cs.ucsb.edu/~mturk/Papers/mturk-CVPR91.pdf)

## Dataset

The dataset used is available at:
[https://github.com/robaita/introduction_to_machine_learning/blob/main/dataset.zip](https://github.com/robaita/introduction_to_machine_learning/blob/main/dataset.zip)

- Each person has their own folder.
- Each folder contains multiple grayscale face images.
- All images are resized and flattened into vectors before processing.

## Tasks Performed

1. **Dataset Preparation**
   - Load and flatten grayscale face images
   - Organize them into a matrix of shape `(mn × p)` where:
     - `m × n` = image resolution
     - `p` = number of images

2. **Mean Calculation**
   - Calculate the average of all faces to obtain a mean face vector.

3. **Mean Zeroing**
   - Subtract the mean face from each image to center the data.

4. **Covariance Matrix Calculation**
   - Compute **surrogate covariance matrix** to reduce complexity (`p × p` instead of `mn × mn`).

5. **Eigen Decomposition**
   - Extract eigenvalues and eigenvectors.
   - Sort eigenvectors based on largest eigenvalues.

6. **Feature Space Generation**
   - Select top `k` eigenvectors to create eigenface space.
   - Project mean-zero faces into this space.

7. **Signature Generation**
   - Project each face image into `k`-dimensional feature space to get signature vectors.

8. **Train ANN Classifier**
   - Use the generated signature vectors as input to a backpropagation ANN.
   - Train using 60% of the data; test on remaining 40%.

9. **Evaluate the Model**
   - Change `k` values and observe classification accuracy.
   - Plot graph: **accuracy vs k**
   - Test recognition with **imposters** (unknown individuals).

## PCA Implementation Steps

1. **Standardize the Data**  
   Ensure each pixel feature has zero mean (mean-zeroed images).

2. **Covariance Matrix Calculation**  
   Use surrogate matrix for efficient eigen decomposition.

3. **Eigenvector Computation**  
   Compute top `k` eigenfaces that capture highest variance.

4. **Projection**  
   Project both training and testing images onto eigenface space.

---

## Image Reconstruction from Eigenfaces (Optional)

1. Load and flatten the target image  
2. Mean-zero the image  
3. Project it to the top `k` eigenfaces  
4. Reconstruct it using:
