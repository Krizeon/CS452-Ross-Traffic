# CS452-Ross-Traffic
Team H's CS452 final project: Ross Traffic Jam-Cam! Find out when Ross Dining hall has really long lines...

Harrison Govan, Kevin Hernandez (Team Hernandez)

CSCI 452

Professor Vaccari

November 29, 2018

##### Acknowledgments
  We would like to thank Professor Vaccari as well as Joey Hernandez for all their help on this assignment.

## Semester Long Project draft Report
  As we were coming up with ideas for our CS452 semester-long project, we had a variety of broad suggestions from our professor. However, we wanted to take on a task that would be more relatable to the average Middlebury student. And we thought, “What does every Middlebury student deal with on a daily basis outside of academics?” We quickly came to our answer: Nobody likes dealing with long lines in Ross Dining Hall! Thus, we decided to take on the task of using image processing to find out when the lines in Ross Dining Hall were the longest during lunch hours. 
  
  As Middlebury students ourselves, we already have an intuitive sense of when lines form to be the longest in Ross. The line builds quite commonly around what we will call the “primary” station, which usually serves fresh cooked meats, sandwiches, fries, veggie patties, etc.  We figured that we would need to take video of this line from a high angle to be able to capture enough of the line to do our processing. We did just that  Monday through Friday for two weeks from 11am-2pm. Then, we created an algorithm that takes this format of video as input and will output the data necessary to create a graph that outlines when the best times to go eat are.
  
  To get to that point, however, we first had to find out if we were allowed to even conduct this project.  We conntacted many professors and were eventually told about the [Institutional Reveiw Board](http://www.middlebury.edu/academics/resources/irb).  The IRB is responcible for handling any reasurch based projects that involve human participence.  We quickly found out that because our project was not in the general scope and the results would not be published, we would be able to conduct our project.  We then had to get approval from the dinning hall staff, human resorcues and public saftey, to make sure that if there were any issues in conducting this experiment we were not at fult.  With that all squared away we could now focuse on how to acctually aquire the neccecary data (film) for the experiment.  We reached out to media services to get a video camera to start gathering our data.  The camera that we got, We quickly found out, was shooting in to high of quality making the the file sizes too large to work with as well as the file that we receved was a .mts
  
  Due to some unfortunate events, we have been forced to adapt our project, which was initially to identify timeframes when the line in Ross dining hall is short. Now it is to be able to accurately guess how many people make up a “blob” in ross dining hall line at a specific moment. The “blob” is a group of students, depending on how many students there are the “blob” shall change in size.   To define this “blob” we will extract data from the videos that we have taken by utilizing different image processing techniques from OpenCV and Skimage to focus on the group of people that create the “blob”.  We will place the information in a go/link (a shortcut to web pages that students can access when connected to middlebury wifi. -- Eg. go/menu)  that will be connected to our Github page.
#### Methods:
  To create the “blob” we have created an algorithm which process the video that we have obtained from two weeks of filming in Ross Dining Hall.  This algorithm utilizes an OpenCV2 method, cv2.createBackgroundSubtractorKNN(). We found this specific background subtractor to be most useful for the dimmer lighting conditions that we have to adjust to in our videos. We found that most of our videos' bottom half was irrelevant, so we discarded the bottom half of our background-subtracted frame. We then begin to read in every 150 frames, or 5 seconds in our 30 frame-per-second video, and begin our processing. For every selected frame, we run a median filter to get rid of salt and pepper noise that will appear in our initial background subtraction. We then run other morphological filters to our mask to try to achieve a solid “blob”. Afterwards, we use region finding to find the largest “blob” of people that appears in mask and focus on the size in pixels of that “blob”. After our morphological filters, we end up with the following:
  
![alt text](https://github.com/Krizeon/CS452-Ross-Traffic/blob/master/bgsubtraction%20example.png "Logo Title Text 1")
    
  Since not all blobs will signify lines, we also needed a way to find out when the largest blob was at the primary station. Luckily, the left-most portion of our videos cut off where the primary station begins. To make this experiment more conducive to our mission, we will implement a check at the primary station to see if a line has been formed. This check will be based around the largest “blob” in the frame, however, if the “blob” is not by the Primary station(x amount of pixels from the left side) then we will not account for it.  We will then store this data along with the current frame number in a text file to use to create a graph afterwards.  This information then will be trained in a machine learning algorithm to predict the number of students in the frame given the size of the “blob”. Once we get a sense of how many pixels form a full-sized person in the video, we can roughly estimate the number of people in line, and thus determine if the line is either “long” or “not long”.
  

#### What we accomplished: 
1.    Gained approval to film in the dining halls.
2.    Acquired a camera to film data 
3.    Developed a functional Background Subtraction Algorithm Using Open CV2
 
#### What we are doing now:
1.    Trying to optimize the Algorithm to yield the best result for our purpose (~12/2)
2.    Creating a dynamic graph to visually represent the data that we produce (~12/5)
3.    Researching and experimenting with different machine learning processes to be trained with the processed images that we create (~12/7)
4.    Be finished training the machine learning (~12/12)
 
#### Issues that we have faced:
  Throughout the whole project we have had many issues, starting with acquiring the necessary permission to conduct this study. We first had to contact the Institutional Review Board to understand how to proceed, to which they directed us to the appropriate departments to consult. From there we then contacted the Dining Hall Staff, Human Resources, and Public Safety.  Once we got the go ahead we also had to find the proper technology to capture our raw data.  The largest hurdle that we have had to face, however, was losing one of our group members due to unforeseen circumstances. This severely set us back and forced us to change our approach in what the outcome of our study would be.  
  
#### Future work:
Future work would include creating more accurate model within the machine learning algorithm as well as establish thresholds in which we can determine the fullness of ross dining hall and to be able to chart that change everyday from 11-2 (which was our initial experiment).
 
#### References:
 
https://docs.opencv.org/3.4/index.html
http://scikit-image.org/docs/dev/api/skimage.html
https://stackoverflow.com/questions/18632276/how-to-draw-a-line-on-an-image-in-opencv 
https://www.toptal.com/machine-learning/supervised-machine-learning-algorithms 


