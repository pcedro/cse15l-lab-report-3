# CSE15L Lab Report 3
---
## Part 1: Bugs
A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
```
# code block of two failed tests from ArrayTests.java
@Test
  public void testReversedOddLength() {
    int[] input1 = { 1, 2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3, 2, 1 }, input1);
  }
   @Test
   public void testReversedEvenLength() {
     int[] input1 = { 2, 3, 6, 7 };
     ArrayExamples.reverseInPlace(input1);
     assertArrayEquals(new int[]{ 7, 6, 3, 2 }, input1); 
    }
```
*An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)*
```
# code block of JUnit test that passes
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
*The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)*
![Image](arraySymptom.png)
- In this screenshot, the symptoms in testReversedOddLength and testReversedEvenLength reveal that an element in the array has caused the failure due to a mismatch in expected vs the actual output.
*The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)*
```
# code block of bug
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}
```
- The bug is in the for loop as it forgets to copy the first half of the array to place it in the back half.
```
# code block of bug fixed
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = arr[i];
      arr[i] = temp;
    }
  }
```
- First, I changed the for loop to iterate until arr.length/2 since it will swap elements only up to the halfpoint. Furthermore, by making a temp variable, it is set to temporarily store the back half of the array and then overwrites it with the front half.
---
# Part 2: Researching Commands

For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

*I found all of the grep command-line option information from [Link](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)*
1. grep -n:
```
# first example of grep -n
grep -n "referral" ./technical/government/Alcohol_Problems/Session2-PDF.txt
19:outcomes through referral and counseling. Identification is only
99:use would more likely prompt referral or counseling, but past use
129:referral as needed.
348:lead naturally to referral and treatment. Others may not promote
349:referral and treatment. Much of the screening literature is
409:referral services. The impact of screening should be demonstrated
413:benefits of screening: increased referrals, more patients receiving
426:of screening on referral and intervention, as well as outcomes such
```
In this command, grep -n is printing out the lines with their line numbers that contain the string "referral" within the Session2-PDF.txt. The command grep -n is useful as if you're searching for a specific phrase but can only remember a certain string phrase, grep -n can help you find the phrase more easily as it even provides the line number and the line.
```
# second example of grep -n
grep -n "nonprofit" ./technical/government/Media/Advocate_for_Poor.txt
15:attorney who grew up in East New York, started a nonprofit practice
25:all the paperwork. We got the nonprofit status from the feds. We
29:Already recognized as a federal nonprofit, the agency is awaiting
```
In this command, grep -n is printing the lines and line number that matched the string keyword "nonprofit" within the file Advocate_for_Poor.txt, which is useful as it helps me locate which lines contain the word rather than searching for it myself.
2. grep -v:
```
# first example of grep -v
grep -v "re" ./technical/government/Media/Barnes_Volunteers.txt    
Barnes Volunteers as Lawyer to Poor
Wednesday, December 18, 2002
Tuesday that he will spend his first six months out of office as an
"One day I'll probably do some legal work that I will charge a
"But for now, I think it is important to fulfill my duty as a
lawyer to help those who need it the most, to speak for those who
cannot speak for themselves and to defend those whose life and
livelihoods depend on it," he said.
Emory University political science professor Merle Black said.
say what it is.
Atlanta Legal Aid provides civil services to poor people in five
metro Atlanta counties.
Mr. Barnes said he was hoping to send a message to other
lawyers.
"This privilege to practice law is just that - it's a privilege.
And it comes with a cost and it comes with a bill . . . We as
profession," he said.
can't imagine anything that could be better than to have the
governor of the state, in his first act as a private citizen,
just astounding to me."
Mr. Barnes did not necessarily need to seek a top-salaried job
million.
```
In this code block, grep -v prints out the lines in the file Barnes_Volunteers.txt that do not contain the string "re". The command grep -v can be useful as it helps block out certain words that are irrelevant when searching for something different within the text file.
```
# second example of grep -v
grep -v "t" ./technical/government/Media/Barnes_Volunteers.txt
Wednesday, December 18, 2002
lawyers.
profession," he said.
million.
```
In this code block, grep -v prints out the lines that do not have the string "t" in the Barnes_Volunteers.txt.
3. grep -c:
```
# first example of grep -c
grep -c "referral" ./technical/government/Alcohol_Problems/*.txt
./technical/government/Alcohol_Problems/DraftRecom-PDF.txt:10
./technical/government/Alcohol_Problems/Session2-PDF.txt:8
./technical/government/Alcohol_Problems/Session3-PDF.txt:20
./technical/government/Alcohol_Problems/Session4-PDF.txt:11
```
In this command, grep -c is printing all of the counted lines in the text files within the Alcohol_Problem folder that matches the string "referral". This command is helpful for showing where a certain string may appear instead of command+f each file for the keyword.
```
# second example of grep -c
grep -c "diversity" ./technical/government/About_LSC/diversity_priorities.txt
44
```
In this command, grep -c printed out the counted lines in diversity_priorities.txt that matched the string "diversity", which was 44 lines.
4. grep -l 
```
# first example of grep -l
grep -l "Emory" ./technical/government/Media/*.txt 
./technical/government/Media/Barnes_Volunteers.txt
```
In this code block, grep -l listed the text file that contained the string "Emory". The command grep -l is useful for searching for text files that contain a topic that is relevant to what you're looking for.
```
# second example of grep -l
grep -l "joined" ./technical/government/Media/*.txt
./technical/government/Media/5_Legal_Groups.txt
./technical/government/Media/Assuring_Underprivileged.txt
./technical/government/Media/Barnes_Volunteers.txt
./technical/government/Media/IOLTA_INTEREST_RATE.txt
./technical/government/Media/Legal-aid_chief.txt
./technical/government/Media/Program_Lodges.txt
./technical/government/Media/RoanokeTimes.txt
./technical/government/Media/The_State_of_Pro_Bono.txt
./technical/government/Media/Too_Crucial_to_Take_Cut.txt
```
In this code block, grep -l printed out all of the text files that contain the string "word".
