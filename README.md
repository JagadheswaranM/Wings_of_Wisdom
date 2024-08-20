# Wings_of_Wisdom

## Approach to Bird Species Classification
### Objective
Develop a multi-class classifier to identify various bird species from images. The model should handle both training and test data, which includes optional bounding box coordinates for image cropping.

## Workflow
### 1. Data Preparation
#### Training Data
**CSV File (train.csv)**: Contains:
**path**: Relative path to the training image.
**class**: Class label of the bird species.
**bbox**: Optional bounding box coordinates in the format left top right bottom.
      
**Image Processing:**
**Loading Images**: Use the PIL library to load images from the file paths specified in the CSV file.
**Bounding Box Handling**: If bounding boxes are provided, crop the images based on these coordinates to focus on the bird. Ensure that coordinates are in the correct order (i.e., left < right and top < bottom).
**Transformation**: Apply transformations such as resizing to 224x224 pixels, normalization, and conversion to tensors.
    
**Test Data**
**CSV File (test.csv)**: Contains:
**path**: Relative path to the test image.
**bbox**: Optional bounding box coordinates.
**Image Processing**: Similar to training data, but without class labels since they are not provided for test images.

### 2. Dataset Class Implementation
**Custom Dataset Class (BirdDataset):**
1. Handles reading images and their corresponding labels or bounding boxes from the CSV files.
2. Applies transformations to the images.
3. Differentiates between training and test data to handle labels and bounding boxes appropriately.
    
### 3. Model Selection and Modification
**Pretrained Model**: Use ResNet-50, a widely used convolutional neural network known for its strong performance in image classification tasks.
**Weights**: Load pretrained weights.
**Modification**: Replace the final fully connected layer to match the number of bird species (200 classes).
    
### 4. Training the Model
**Loss Function**: Use CrossEntropyLoss for multi-class classification, which combines softmax activation and negative log-likelihood loss.
**Optimizer**: Use Adam optimizer with a learning rate of 0.001 to update model weights.
**Training Loop**:
1. Iterate through the training dataset for a specified number of epochs.
2. Compute loss for each batch, backpropagate the errors, and update weights.
3. Print loss after each epoch to monitor the training process.
          
### 5. Model Evaluation
**Validation Loop:**
 1. Set the model to evaluation mode.
 2. Perform inference on the validation/test dataset without updating model weights.
 3. Calculate accuracy by comparing predicted labels with true labels (for validation data).
 4. Print accuracy to evaluate model performance.
      
### 6. Inference and Results Preparation
**Inference**:
 1. Use the trained model to predict labels for the test dataset.
 2. Extract predicted labels and confidence scores from the model’s output probabilities.
      
**Save Results:**
 1. Format predictions into a CSV file with columns: path, predicted_label, and confidence_score.
