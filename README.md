# Data-Manipulation-with-Bash
A Bash script which extracts and manipulates data from the web. 

Script #1 ("Extract and Format URLs Data"):
This script expects as an argument the name of a text file.
Returns the extracted data from the URLs in the following format:
 <Date> : <Category (Kategorie)> : <Ranking (Platz)> : <Name (Name, Vorname)> : <Nationality (DOK)> : <Call Sign (Call)> : <Finish Time (Laufzeit)> : <Number of Collected Transmitters (Fox)> : <Starting Number (StNr)>

A sample row:

05.09.2018 : M70 : 6 : Istvan Matrai : HUN : HA4XA : 134'14 : 3 : 178
  
Script #2 ("Statistical Report of Extracted Data"):
This script expects several arguments:
  - First arg: the name of a file which contains data in the format specified by Script #1
  - Second arg: the name of a subcommand (subcommands are explained below)
  - Extra args depending on the particularities of the subcommand
  
Subcommand #1:
Calling format: "./StatisticalReportOfExtractedData data.txt top_places <category> <m> <n>"
  
Description:
  - "data.txt" - txt file containing formatted data
  - "top_places" - the name of this subcommand
  - "<category>" - category name (Example: W19)
  - "<m>" - particular ranking (Example: 4)
  - "<n>" - number of participants
  
  First, the script sorts all participants depending on how many times they have ranked within the first <m> places of a particular <category>. Then, only the first <n> contenders from this list are considered. Finally, a ranking is returned which shows the participant with the most rankings fulfilling the criteria and their <n-1> follow-ups.
  
  Example input (Note: This is just example output. It will not return the same result if tested.):
  ./ardf_stats.sh /tmp/ardf top_places W19 3 4
  
  Example output:
  4 Andrea Diaksova
  2 Evangelina Diaksova
  1 Ziyu Huang
  1 Yuanzheng Qiu
  
  Meaning: Andrea Diaksova has ranked 4 times among the top 3 in the W19 category.
  
  Subcommand #2:
  Calling format: "./StatisticalReportOfExtractedData data.txt parts <name>"
  
  Description:
    - "data.txt" - txt file containing formatted data
    - "parts" - the name of this subcommand
    - "<name>" - the first and last name of a competitor
  
  For each category in which <name> has participated in, the script returns a row containg the category's name and all the respective competition dates.
  
  Sample input:
  ./ardf_stats.sh /tmp/ardf parts 'Oleg Fursa'
  
  Sample output:
  M60 04.09.2016
  M70 04.09.2018, 05.09.2018, 05.09.2019, 03.09.2019
