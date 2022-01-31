# R-CNN

(Image with multiple objects) --> (bbox and class label for all the objects belonging to the classes of interest in that image)
* Chalanges:
  1. Input image can be of variable sizes
  2. Input images will have variable number of objects in it so output will also be of variable length.
  3. bbox of objects within an image will be of varity of sizes and aspect ratio.

To Simplify some of the problems we uses region proposals (Not comming from neural network):
* Given input image with multiple objects we generate a fixed number of region proposals. (much larger than the number of object in any of the image of interst)
* Now each proposals tries to capture one object.
* So, Now our task is simplified.
  * (Reason proposal with one object) --> (bbox and class lable corresponding to that object)
  * (H' x W' x C) --|CNN|--> Feature Vector --|FC Layer|--> "softmax over class labels" && "bbox coordinates"
  * **Assumption:** Reason Proposal contains the object entirly.

## Three stages of R_CNN:
1. Generates category independent region proposals for potential objects.
  * H x W x C --> R x 4
    * Where R is the number of region proposals for that image.
    * 4 corresponding to each reason is the bbox coordinates of the region.
      * **(xmin, ymin, xmax, ymax)**
      * **(xmin, ymin, h, w)**
      * (h, w, xctr, yctr)

2. CNN that extracts a **fixed-length** feature vector from each region.
  * Regardless of the size and aspect ratio of the region proposal, it is warped into fixes size image.
  * Then that wraped image is fed into CNN.

3. Classifying the regions and refining the region proposals.

