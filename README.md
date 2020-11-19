# DataMining-FiveTask
## This Project has 5 tasks. See "Your 5 Tasks" below

In ATNT50 directory we have

trainDataXY.txt   

It contains 45 images. image 1-9 from class 1. image 10-18 from class 2. etc.
Each image is a column. 1st row are class labels.

testDataXY.txt     

It contain 5 images. 
Each image is a column. 1st row are class labels.

------------------------------------------------------------------------------------
You train the classifier using training data. Once classifier is trained,
you classifier the data in testData, and compare the obtained class labels 
to the ground-truth label provided there. 

These two data are simple training and testing data.
They are warm-up data, so you can see how your classifier work on this simple data. 

-------------------------------------------------------------------------------------


data set: ATNT-face-image400.txt  :

Text file. 
1st row is cluster labels. 
2nd-end rows: each column is a feature vectors (vector length=28x23).

Total 40 classes. each class has 10 images. Total 40*10=400 images

----------------------------------------------------------------------------------------

data set: Hand-written-26-letters.txt :

Text file. 
1st row is cluster labels. 
2nd-end rows: each column is a feature vectors (vector length=20x16).

Total 26 classes. each class has 39 images. Total 26*39=1014 images.


-------------------------------------------------------------------------------------
Once you are confident that your classifier works correctly,
you are to use 5-fold cross-validation (CV) assess/evaluate the classifier.
You do CV using the following two full datasets.

ATNT face images data are generally easier, i.e., you get high classification accuracy.

You run classifier on ATNT data first, to make sure you get correct results.

Hand-written-letters data are harder to classify, i.e., you get lower classification accuracy.

You run classifier on hand-written-letter data only after you are confident 
that your classifier works correctly.

## %%%%%%%%%%%%%%%%%%%%    Your 5 tasks A, B, C, D, E  %%%%%%%%%%%%%%%%%%%%%%%%%
Purpose:
(1)  Implement Centroid methods by yourself.
(2)  Learn to use Linear Regression £¨this is optional).
(3) Learn to use Support Vector Machine (SVM) in Matlab or Python.
(4) Learn to use cross-validation related subroutine/functions in Matlab or Python.
(5) Implement the data handler of Task E.



(A£©
Use the data-handler to select "A,B,C,D,E" classes from the hand-written-letter data. 
From this smaller dataset, Generate a training and test data: for each class
using the first 30 images for training and the remaining 9 images for test.
Do classification on the generated data using the four classifers.


(B)
On ATNT data, run 5-fold cross-validation (CV) using  each of the 
four classifiers: KNN, centroid, Linear Regression and SVM.

If you don't know how to partition the data for CV, you can use the data-handler to do that.


Report the classification accuracy on each classifier.
Remember, each of the 5-fold CV gives one accuracy. You need to present all 5 accuracy numbers
for each classifier. Also, the average of these 5 accuracy numbers.



(C) On handwritten letter data, fix on 10 classes. Use the data handler to generate training and test data files.
    Do this for seven different splits:  (train=5 test=34), (train=10 test=29),  (train=15 test=24) , 
       (train=20 test=19), (train=25 test=24) , (train=30 test=9) ,  (train=35 test=4). 
    On these seven different cases, run the centroid classifier to compute average test image classification
    accuracy. Plot these 7 average accuracy on one curve in a figure. What trend can you observe?
    When do this task, the training data and test data do not need be written into files.


(D) Repeat task (D) for another different 10 classes.  You get another 7 average accuracy. 
    Plot them on one curve in the same figure as in task (D). Do you see some trend?

(E) write data handler.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%   Data handler  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

Data handler will help you to "extract a small part of a input data" and
generate training data and test data as input to feed into a classifier.


Example 1: from AT&T image data, you use pickDataClass subroutine explained below
to select 5 class (50 images) and store the results in an data array or a data file.

Example 2: from AT&T all data, or subset of it as the result of Example 1, generate a 
training data using the first 9 images of a class and the test data using the class 1 image of the class. 
This is done for all class in the input file. Suppose, we use entire AT&T data. Then the training data contains 
9*40=360 images and the list of corresponding class labels. The test data contains 1*40=40 images
and the list of corresponding class labels.
(The data in ATNT50 are generated in this way)

Example 3. Generate a 2-class data as the input to the 2-class SVM classifier.
  From the hand-written-letter data, you first use "pickDataClass" subroutine and pick 
  "C" and "F" classes and store them in a file or an array.
  Then you use ¡°splitData2TestTrain" split the data: using the first 30 images in "C" and in "F" 
  to form the training data, and using the remaining 9 images in each class to form the 
  test data. Thus the training data contains 30*2 images, the test data contains 9*2 images.

You need to write:

subroutine-1: pickDataClass(filename, class_ids)
 
  filename: char_string specifying the data file to read. For example, 'ATNT_face_image.txt'
  class_ids:  array that contains the classes to be pick. For example: (3, 5, 8, 9)
  Returns: an multi-dimension array or a file, containing the data (both attribute vectors and class labels) 
           of the selected classes
  We use this subroutine to pick a small part of the data to do experiments. For example for handwrittenletter data,
  we can pick classes "C" and "F" for a 2-class experiment. Or we pick "A,B,C,D,E" for a 5-class experiment. 


  test_instances: the data instances in each class to be used as test data.
  We assume that the remaining data instances in each class (after the test data instances are taken out) will be
  training_instances


subroutine-2: splitData2TestTrain(filename, number_per_class,  test_instances)
  filename: char_string specifying the data file to read. This can also be an array containing input data.
  number_per_class: number of data instances in each class (we assume every class has the same number of data instances)
  test_instances: the data instances in each class to be used as test data.
                  We assume that the remaining data instances in each class (after the test data instances are taken out) 
                  will be training_instances 
  Return/output: Training_attributeVector(trainX), Training_labels(trainY), Test_attributeVectors(testX), Test_labels(testY)
  The data should easily feed into a classifier.

  Example: splitData2TestTrain('Handwrittenletters.txt', 39, 1:20) 
           Use entire 26-class handwrittenletters data. Each class has 39 instances.
           In every class, first 20 images for testing, remaining 19 images for training

subroutine-3:
   This routine will store (trainX,trainY) into a training data file, 
   and store (testX,testY) into a test data file. The format of these files is determined by 
   student's choice: could be a Matlab file, a text file, or a file convenient for Python.  
   These file should allow the data to be easily read and feed into a classifier.
   During a COMPUTER QUIZ, you use this routine to save the files and submit them as part of the quiz results.


Subroutine-4: "letter_2_digit_convert" that converts a character string to an integer array. 
   For example ,letter_2_digit_convert('ACFG') returns array (1, 3, 6, 7). 
   A COMPUTER QUIZ problem could be: Pick 5 classes with letters 'great' from the hand-written-letter data, and 
     generate training and testing data using first 20 images of each class for training and the rest 19 images for test.
     You will need to use  letter_2_digit_convert('GREAT') to convert to numbers and then subroutine-1 to pick the subset
     of the needed data.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
