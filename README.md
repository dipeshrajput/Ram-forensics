### Use any open source software to generate report to acquire and analyze the volatile data that is stored in Random Access Memory of your machine. 


Introduction:
- Objective of the Project
- Description of the project.
- Scope of the project.

System Description:
- Target  System Description
- Assumption and Dependencies.
- Functional and Non-functional dependencies.
- Data set used in support of your project (if any the paste the link)

Analysis Report
- System  Snapshots and Full Analysis Report

Reference / Bibilography
 

 
Used tools 
-> Microsoft AVML to dump memory. (to capture )
-> Volatility to analyze memory ( to analyze )

### Necessary Steps before Proceeding

1. create a folder called ram_forensics (pick whichever name you prefer).

sh
mkdir ram_forensics
cd ram_forensics


REMEMBER: will be doing all the operations from this folder only.

#### Use AVML for capturing volatile data in RAM.

Downloaded the release file of AVML from microsoft/avml repo. used chmod to make it executable. 

sh
.avml memory.dmp


It will create a memory dump.


#### Use Volatilty to analyze the memory dump.

1. From the same directory, git clone the volatity repo.

sh
git clone https://github.com/volatilityfoundation/volatility.git


2. cd into volaitity.

sh
cd volatility


3. Run the command.
sh
python3 setup.py install
