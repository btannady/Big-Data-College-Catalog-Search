# Big Data College Course Catalog Search Program 
This is my Big Data College Course Catalog Search Program !



Hi,

This is my Diablo Valley College Course Catalog Search Program!
It is coded in C++, the DvcScheduleSearch.cpp file reads off of the dvc-schedule.txt file, so make sure you have them BOTH in the same file directory when you compile the DvcScheduleSearch.cpp program.


ALSO NOTE:
If you are on Xcode, you may need to go to Product > Scheme > Edit Scheme > Run test (on the right) > Options (middle top).
Down under Options check “Use custom working directory” and set it to the directory where your .txt file is located.
Sometimes Xcode has trouble locating the .txt file even though it is correctly in the same directory as the .cpp file. 

------------------------------------------------------------------------------------------------------------------------------
How the program works is:

  1. The program will print a message to console, asking for an input regarding what course the user would like to know about.
  
  2. The user inputs then inputs a course name (like, COMSC-210) back to the program. 
  
  3. The program will then quickly and efficiently parse the dvc-schedule.txt file, searching and collecting data regarding the user's input.
  
  4. If the user inputs a course name that is not found in the system, then the program will simply prompt the user that the course was not found as far back as the year 2000. However, if the course IS found within the dvc-schedule.txt file, then the program will then output a message back to the user regarding the year when the course was first ever offered, as well as when the course was last offered.
  
  5. The program will then loop again (to step 1.) and ask the user for a course they'd like to know about. The program will keep looping and won't end until the user inputs the character 'X' or 'x' back into the program.
 
