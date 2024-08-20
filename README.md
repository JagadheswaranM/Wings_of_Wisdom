# Wings_of_Wisdom

## Approach to Bird Species Classification
### Objective
Develop a multi-class classifier to identify various bird species from images. The model should handle both training and test data, which includes optional bounding box coordinates for image cropping.

## Workflow
### 1. Data Preparation
#### Training Data
&emsp;**CSV File (train.csv)**: Contains:<br/>
&emsp;**path**: Relative path to the training image.<br/>
&emsp;**class**: Class label of the bird species.<br/>
&emsp;**bbox**: Optional bounding box coordinates in the format left top right bottom.<br/>
      
**Image Processing:**
&emsp;**Loading Images**: Use the PIL library to load images from the file paths specified in the CSV file.<br/>
&emsp;**Bounding Box Handling**: If bounding boxes are provided, crop the images based on these coordinates to focus on the bird. Ensure that coordinates are in the correct order (i.e., left < right and top < bottom).<br/>
&emsp;**Transformation**: Apply transformations such as resizing to 224x224 pixels, normalization, and conversion to tensors.<br/>
    
**Test Data**
&emsp;**CSV File (test.csv)**: Contains:<br/>
&emsp;**path**: Relative path to the test image.<br/>
&emsp;**bbox**: Optional bounding box coordinates.<br/>
&emsp;**Image Processing**: Similar to training data, but without class labels since they are not provided for test images.<br/>

### 2. Dataset Class Implementation
**Custom Dataset Class (BirdDataset):**<br/>
&emsp;1. Handles reading images and their corresponding labels or bounding boxes from the CSV files.<br/>
&emsp;2. Applies transformations to the images.<br/>
&emsp;3. Differentiates between training and test data to handle labels and bounding boxes appropriately.<br/>
    
### 3. Model Selection and Modification
&emsp;**Pretrained Model**: Use ResNet-50, a widely used convolutional neural network known for its strong performance in image classification tasks.<br/>
&emsp;**Weights**: Load pretrained weights.<br/>
&emsp;**Modification**: Replace the final fully connected layer to match the number of bird species (200 classes).<br/>
    
### 4. Training the Model
&emsp;**Loss Function**: Use CrossEntropyLoss for multi-class classification, which combines softmax activation and negative log-likelihood loss.<br/>
&emsp;**Optimizer**: Use Adam optimizer with a learning rate of 0.001 to update model weights.<br/>
&emsp;**Training Loop**:<br/>
&emsp;&emsp;&emsp;1. Iterate through the training dataset for a specified number of epochs.<br/>
&emsp;&emsp;&emsp;2. Compute loss for each batch, backpropagate the errors, and update weights.<br/>
&emsp;&emsp;&emsp;3. Print loss after each epoch to monitor the training process.<br/>
          
### 5. Model Evaluation
**Validation Loop:**
&emsp; 1. Set the model to evaluation mode.<br/>
&emsp; 2. Perform inference on the validation/test dataset without updating model weights.<br/>
&emsp; 3. Calculate accuracy by comparing predicted labels with true labels (for validation data).<br/>
&emsp; 4. Print accuracy to evaluate model performance.<br/>
      
### 6. Inference and Results Preparation
**Inference**:
&emsp; 1. Use the trained model to predict labels for the test dataset.<br/>
&emsp; 2. Extract predicted labels and confidence scores from the model’s output probabilities.<br/>
      
**Save Results:**
&emsp; 1. Format predictions into a CSV file with columns: path, predicted_label, and confidence_score.<br/>
