# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Library/tool to read Data from csv file for analysis
3. PDF report generator
4. Notify machanism


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | It involves other tool to write data into file 
Counting the breaches       | Yes           | It is needed to check whether functionality is working fine
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | No            | Use mock functionality to test notification service

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Count the no of breaches based on the cvs 
4. Write the count to the PDF based on csv
5. Record trends based on csv data
6. Write "inaccessible server" to the PDF when not able to access to server for csv file.
7. Send notification when new report is available

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | email / sms alert           | mock the notifier
Report inaccessible server | csv path     | file not found              | Fake the server store
Find minimum and maximum   | csv data     | min and max                 | None - it's a pure function
Detect trend               | csv data     | date and time from csv data | None - it's a pure function
Write to PDF               | analysis data| PDF file                    | mock the pdf
