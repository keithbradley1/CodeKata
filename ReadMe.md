The business
requirements were focused on the report output and made certain assumptions about the file usually
being well formatted so I focused on the integrity of the report. I made a design decision that if
anything in the file is wrong report integrity would be compromised so an error is thrown to prevent
a partial report. There didn't seem to be a reason to async/await so I avoided that complexity too.

Supporting both a file path and stream for input allowed test cases to be written without having to
manage many small files. Stream also offers an extension point if this is used in a larger project.

Code has in-line "design decision" and "code review" comments.

I chose not to use the following design options:

  TripProcessor
  IParser with string.Split or https://www.nuget.org/packages/CsvHelper implementations
  IFilter to handle the <5 or >100 mph logic
  IReportGenerator for report formatting


---

Use any .Net language; use any project type.  The goal of this exercise is to get a better glimpse into your thought process.  While this is a simple exercise, think of it as a large project, so put whatever patterns you think would be necessary.
Create a ReadMe file to explain any details.  Do what you think would help verify your work.

The code will process an input file.

Each line in the input file will start with a command. There are two possible commands.
The first command is Driver, which will register a new Driver in the app. Example:
Driver Dan
The second command is Trip, which will record a trip attributed to a driver. The line will be space delimited with the following fields: the command (Trip), driver name, start time, stop time, miles driven. Times will be given in the format of hours:minutes. We'll use a 24-hour clock and will assume that drivers never drive past midnight (the start time will always be before the end time). Example:
Trip Dan 07:15 07:45 17.3
Discard any trips that average a speed of less than 5 mph or greater than 100 mph.
Generate a report containing each driver with total miles driven and average speed. Sort the output by most miles driven to least. Round miles and miles per hour to the nearest integer.

Example input:
Driver Dan
Driver Alex
Driver Bob
Trip Dan 07:15 07:45 17.3
Trip Dan 06:12 06:32 21.8
Trip Alex 12:01 13:16 42.0
Expected output:
Alex: 42 miles @ 34 mph
Dan: 39 miles @ 47 mph
Bob: 0 miles
