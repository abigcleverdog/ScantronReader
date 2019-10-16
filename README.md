# ScantronReader
take a multi-page .pdf file and some parameters (areas of interest, #of items, # of options per item); generate grading result  Use case: preprint the scantrons for an exam; collect filled scantrons; scan scantrons with an office scanner to get scan.pdf file; ** use Scantron Reader to obtain grading result

### 2019/10/16

* the App
  - at current stage, the scantron is built in openCV. so the ROIs are fixed with small variation due to scanning;
  - break pdf into images using pdf2image package;
  - align/rotate each image by finding corners (smaller circle at bottom right); assert alignment failed < 5
  - read ROIs for results; highlight images with abnormal response (choice == 0 or >1)
  - generate report from images to form result pdf, generate csv report; sort entries by ID.
  
* the Web App
  - Flask App with call another python script to run the App via subprocess; There are two reasons behind this:
    1. the App was developed in Python 3 while the Flask App was in Python 2.7
    2. the Flask App needs to keep running regardless the status of the grading App (extended running time, errors, assertions, etc.)
  - Currently Flask App takes max 30 mb pdf input (listed 20 on UI)
  - the App consumes much more Memory than the Flask App. As a result, a 4G swap was step up at the ubuntu server
  
* thoughts on future dev
  - provide spontaneous feedback to user while grading instead just a long pause on the page
  - use database to orgnize user input/output and secure the files
  - add the donation page
  - UI for customized scantron and grading
  - autograding with Key input
