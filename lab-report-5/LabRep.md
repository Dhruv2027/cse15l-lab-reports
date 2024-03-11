# Week 9 - Putting it all Together

# Part 1 - Debugging Scenario

### Stephen Strange (Student)
Hi, I keep failing my `merge()` method. When I use the `test.sh` file to test my code, it says that my test `"timed out after 500 milliseconds"`. I have attached the screenshot of my JUnit output and the method I am currently using. Thank you for your help.
![Image](SS1.png)
![Image](SS2.png)

### TA
Hi Stephen, I think the error you are facing is in the while loop from lines 41-45. There, you check if `index2 < list2.size()`, add the the result in your arraylist, but then increment the value of `index1` rather than `index2`. For this reason, you may be in an infinite loop, with the value of `index2` always remaining less than the size of `list2`.

### Student
OH! I see now, I spent like 2 hours on that bug, with nothing working. Just CS things ig. Running the bash file gives me no more errors, thank you so much! 

![Image](SS3.png)

# Part 2 - Reflection
I have learnt a lot throughout the quarter, but specifically in the second half, it was interesting to learn that I can edit files through the command line itself. I always thought that I had to open VSCode to edit my code files. However, now if I want to make a quick edit, I just use vim and make my changes. Secondly, I found using JDB was extremely useful while debugging my PAs in CSE 12. Although it took time, it was easy to understand where exactly my code was going wrong as I could see all the references using the `locals` command. I think that command is one of the most useful commands in all of java. 
