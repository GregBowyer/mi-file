# MI-File

This is a mirror of http://code.google.com/p/mi-file/

## Introduction
MI-File allows you to perform approximate similarity search on huge datasets.

The technique is based on the use of a space transformation where data objects are represented by ordered sequences of reference objects. The sequence of reference objects that represent a data object is ordered according to the distance of the reference objects from the data object being represented. Distance between two data objects is measured by computing the spearmann footrule distance between the two sequence of reference objects that represent them. The closer the two data objects the most similar the two sequence of reference objects. The index is based on the use of inverted files.

More details on the technique can be found in the paper "MI-File: using inverted files for scalable approximate similarity search", by Giuseppe Amato, Claudio Gennaro, and Pasquale Savino, published on Multimedia Tools and Applications:http://dx.doi.org/10.1007/s11042-012-1271-1 and "Approximate Similarity Search in Metric Spaces Using Inverted Files", by Giuseppe Amato and Pasquale Savino, presented at Infoscale 2008: [http://mi-file.isti.cnr.it/CophirSearch/MI-file.pdf]

## How to use the MI-File library
MI-File is entirely written in java and does not depends on any other library. In order to use it compile the source code with your preferred compiler then perform the following preliminary steps (see JavaDoc embedded in source code for additional details):

You have to create a class that extends the abstract class Dataset.DatasetObject that encapsulate your data objects.
Create a set of reference objects. To do that you have to use the class ReferenceObjects. The size of the set of reference objects can be estimated as 2*sqrt(dataset size).
Decide the number ki of reference objects to use to represent data objects (parameter p_ki of the MI_File constructors). Data objects are represented by the ki closest reference objects. This number is typically much smaller than the total number of reference objects. A good value is typically the inthrinsical dimensionality of the dataset. In case this value is not available you can use the dimensionality (in case of vector data).
Create an instance of MI_File, using the set of reference objects above.
IMPORTANT: Once an MI_File has been created with a certain set of reference objects, the set of reference objects should not be changed. An MI_File MUST be open always with the same set of reference objects, elsewhere unpredictable results will be obtained.
Start inserting data objects to be indexed.
From now on, you can open the MI_File, using always the same set of Reference objects, insert new data objects or use the search methods (kNN, kNNRetrieve, and kNNRetrieveAndSort).
Note that there are other parameters you can use to play with.

ks determines the number of reference objects to be used to represent the query; it should be smaller than ki.
MaxPosDiff can be used to access just a portion of the posting lists; if MaxPosDiff is 10 just the portion of the posting lists corresponding to objects having reference objects in position +/- 10, with respect to those of the query, is accessed.
The package Example contains source code examples of the above steps.
