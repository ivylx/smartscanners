# Smart Scanners for Cards and Documents
Repository for my CIS581 Final Project with Professor Jianbo Shi, Fall 2023.

Ivy L. Xie (Individual)

### Description of Code and Layout
* Report: `CIS_581_Final_Project_Report_Ivy_L_Xie.pdf`
* Video Presentation Slides: `CIS_581_Final_Project_Video_Presentation_Ivy_Luxen_Xie.pptx`
* Video Presentation: Google Drive link can be directly accessed here: https://drive.google.com/file/d/1YJLgB6vf7OrsZPGN372j9vpN9bdgMwTl/view?usp=sharing

The root directory has the `requirements.txt` for required libraries and packages to install. `Standardized_Test_Answer_Scanner.ipynb` contains intermediate results, explanations, and visualizations for the code to scan standardized test answer sheets, as well grade the answers. The `Bank_Card_Scanner.ipynb` contains intermediate results, explanations, and visualizations for the code to scan bank cards, as well display the card information to the screen.

The `IM/` folder contains all the input images including OCR-A reference image and sample test sheets and bank cards to be scanned.

Finally, the `imageutils.py` is the helper function for ImageUtils.

### Installation and Setting Up
1. `pip install -r requirements.txt` in a `Python3.10.12` virtual environment
- Note: some packages might have to be manually installed/removed depending on Operating System
- Pay special attention to OCR-A reference image and imageutils
2. `Standardized_Test_Answer_Scanner.ipynb` will run on `IM/scannedanswers.png` and output the graded results to the screen.
- this Jupyter notebook will run contour detection, four-point perspective warping, Otsu's thresholding and masking multiple times.
  - the first step is to map the question number, to locate the paper by sorting contours in the edge map that correspond to the sheet and to binarize the warped paper.
  - the second step is to compute the bounding box of the contours that correspond to the questions and sort the total number of correct answers.
  - the third section is to mask the filled-in answer, examine it to decide if it is correct and calculate the grade accordingly.
  - the fourth section is to display the final grade with circled correct answers in green(correct) or red(wrong) on the test sheet to the screen.
3. `Bank_Card_Scanner.ipynb` will run on `IM/number_reference.png` and any debit card image in the `IM/` folder, outputting the card information to the screen.
- this Jupyter notebook will run contour detection, whitehat morphological operator, Otsu's thresholding and convolution kernel multiple times.
  - the first step is to map the first digit of a card number to the card type, to threshold the OCR-A reference image and map digit name to the ROI.
  - the second step is to loop over the OCR-A reference contours and populate an array with all digits.
  - the third step is to initialize a rectangular and square structuring kernel and apply a whitehat morphological operator to isolate card numbers.
  - the fourth step is to compute the Scharr gradient of the tophat image, and then scale the rest back into the range [0, 255].
  - the fifth step is to close gaps in between credit card number digits, then apply Otsu's thresholding method to binarize the image.
  - the sixth step is to find contours in the thresholded image, then populate a list with digit locations of digits.
  - the seventh section is to loop over the digit contours and apply correlation-based template matching to take the score and update the scores list.
  - the eighth section is to display the output credit card information to the screen.

---

## Acknowledgments
* CIS581 Instructors, TA's, and Ed
