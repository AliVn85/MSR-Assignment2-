## Note
This is a reproduction project as part of the MSR course 2022 at UniKo, CS department, SoftLang Team.

## Names of team/students

This is team **ZULU**.
- Ali Vahdatnia
- Danoosh Peachkah
- Soroush Mozooni

## Objective of reproduction
### Description
The client-libraries duets of Java maven projects was aimed to be reproduced.
### Input data
A python argument (`docker run --rm -v ‘pwd‘:/results castorsoftware/duets:latest compile --repository https://github.com/radsz/jacop --commit 8f09fd977a`) is inserted in [main.py](https://github.com/castor-software/Duets/blob/master/runner/main.py) to fetch the needed data.
### Output data
The final output is a [JSON file](https://github.com/castor-software/Duets#format), for further analysis in the paper.

fetched data ([original dataset](https://github.com/castor-software/Duets/tree/master/dataset)) is used to output.
## Findings of reproduction
### Process delta:
First of all, the paper stated that:
> All those tasks are simplified into the following command line.

In the middle of the process, we noticed that this was far from the truth as not only the code did not work in the stated Docker environment, but also the arguments in the command line were different than the scripts. These findings came at the expensive cost of losing our time.
In fact, after noticing Docker failing to start, we tried to "simulate" it in a VMWare using Ubuntu. We then tried to dismiss Docker altogether after getting an unsuccessful result from both Linux and Windows environments.
Next, we "extract" what they did to Docker and run their scripts in a Windows environment directly. And at this step, we noticed some errors that they have done in their paper. e.g., The *--URL* argument was mistakenly written *--Repository*. And none of the JS files were used in their Python scripts. We tried to fix the issues, though unable to connect to the JS files with the Python codes. However, this resulted in shifting our focus to only work on this part of the paper, as without resolving this issue, working on the next steps is not possible due to the nature of DUET - which is what the paper is all about.
Ultimately, we could run the python code without errors. However, the result is a JSON file which is structurally different than the one paper expected.

### Output delta:
As stated above, due to the nature of DUET we had to recreate/crawl the GitHub again at this time to gain an output, thus we had to fix the crawler part and the [achieved output](https://github.com/AliVn85/MSR-Assignment2-/blob/main/runner/output.json) was gained. However, the output does not include sufficient data for further analysis. [The output from the paper](https://github.com/castor-software/Duets#format) includes features like "groupId", "artifactId", "commit", etc., whereas the one we received from the Runner script consists of one Entry that has "commit", and "test_results" in the JSON file.

For more details, we provided the below image. As you can see, the docker code unfortunately and unexpectedly has critical errors which we tried to resolve as described above; The syntax had a critical error (1), the 1st argument was totally different (2), and the unknown unsolved error of Docker (3) using the Compile keyword that wasted an enormous amount of our time.
![enter image description here](https://github.com/AliVn85/MSR-Assignment2-/blob/main/Some%20paper%20errors.png?raw=true)
### 2nd Output:
Fixing the errors from the paper led to abandoning the Docker option and directly using Python in windows using VS Code, which made it possible to get [the other output](https://github.com/AliVn85/MSR-Assignment2-/blob/main/runner/output.txt) from JaCOP- a Python framework mentioned in the paper.
Speaking of VS Code, we were able to get more details in the terminal as well - image below.
![enter image description here](https://github.com/AliVn85/MSR-Assignment2-/blob/main/VS%20Code%20output.jpg?raw=true)

## Implementation of reproduction
### Hardware requirements:
-   1.6 GHz or faster processor
-   1 GB of RAM
### Software requirements:
-   OS X El Capitan (10.11+)
-   Windows 8.0, 8.1 and 10, 11 (32-bit and 64-bit)
-   Linux (Debian): Ubuntu Desktop 16.04, Debian 9
-   Linux (Red Hat): Red Hat Enterprise Linux 7, CentOS 7, Fedora 34
-	VS Code
-	Python
	-	PyGithub
	-	Path
-	Java Development Kit 18
-	Maven
-	Active Internet Connection
### Validation:
The intended code from the paper authors seems to execute a search pattern via Jacop to get the needed data. the data then will be passed to some python functions to get filtered. This, however, was not realizable for unknown reasons in the code that they provided. We suspect the key argument they provided is either wrong or no longer matches a pattern for Jacop. As a consequence DUET is unable to fetch the needed dataset to work with. So it correctly sends a message stating that it can not find Git projects using the argument provided in the paper - for more details see the orange rectangle in the last image.
### Data: 
***Inputs:***
"<span>https:</span><span>//</span>github<span>.</span>com/radsz/jacop" , "8f09fd977a"

***Output:***
The temporary output data is saved in the "D:/GiTmp" location which is a result of the Jacop Processor downloading data for searching.
And two more files - Output.JSON and Output.log - which were discussed before.