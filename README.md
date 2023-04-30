Download Link: https://assignmentchef.com/product/solved-homework-3-data-extraction-conversion-and-build-a-csv-file-output-cop3502-cs-1
<br>
As discussed in <em>Homework 1 </em>many ETL (extraction, transformation, and loading) problems parse data files wherein the data fields is separated by commas. This assignment is a continuation of that process – with an additional two steps. The first step is to convert the input file’s <em>latitude </em>and <em>longitude </em>from <em>sexagesimal (base 60) </em>degrees to decimal degrees. For example, the inputs are in the form: degrees, minutes and seconds, arcseconds and direction. The outputs are in the form: sign, degrees, and decimal fractions to represent the same value.

This assignment requires the data extraction, degree conversion, data formatting, and output. The file inputs are defined in the <em>Inputs</em>, as are the outputs.

The verification of the output data will be the plotting of the output file’s airport information in a <em>Javascript </em>enable web page.

<h1>1      Objectives</h1>

The objectives of this assignment are to demonstrate proficiency in file I/O, data structures, data transformation, and file output using C language resources.

<h2>1.1     Inputs</h2>

There are two basic inputs, the input file name, passed via the command line, and the input file data defined below.

1.1.1       Command Line arguments The input file name will be input as follows:

<ul>

 <li>hw3Export filename.ext</li>

 <li>In the event that the input file is not available or there is an error finding the file, an appropriate error message shall be displayed. Use the example below for guidance.</li>

 <li>hw3Export ERROR: File “bogusFilename” not found.</li>

</ul>

<h3>1.1.2      Input File fields</h3>

The CSV input file contains the following fields. Please note these fields may vary in size, content, and validity of the data. Also note that some of the data formats are a <em>melange </em>of types. Specifically, note that both latitude and longitude contain numbers, punctuation, and text. Likewise, the FAA Site number contains digits, letters, and punctuation. (<em>This assignment will treat all input data as character data.</em>)

Table 1: Airports Data Fields

<table width="432">

 <tbody>

  <tr>

   <td width="136">Field Title</td>

   <td width="167">Description</td>

   <td width="129">Size</td>

  </tr>

  <tr>

   <td width="136">FAA Site Number</td>

   <td width="167">Contains leading digits followed by a decimal point and short text</td>

   <td width="129">Leading digits followed by a decimal point and zero to two digits and a letter</td>

  </tr>

  <tr>

   <td width="136">Loc ID</td>

   <td width="167">The airport’s short name, i.e.MCO for Orlando</td>

   <td width="129">4 characters</td>

  </tr>

  <tr>

   <td width="136">Airport Name</td>

   <td width="167">The airport’s full name, i.e.Orlando International</td>

   <td width="129">~30 characters</td>

  </tr>

  <tr>

   <td width="136">Associated City</td>

   <td width="167">The nearest city</td>

   <td width="129">~25 characters</td>

  </tr>

  <tr>

   <td width="136">State</td>

   <td width="167">State</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Region</td>

   <td width="167">FAA Region</td>

   <td width="129">3 characters</td>

  </tr>

  <tr>

   <td width="136">ADO</td>

   <td width="167">Airline Dispatch Office</td>

   <td width="129">3 characters</td>

  </tr>

  <tr>

   <td width="136">Use</td>

   <td width="167">Public or Private</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Latitude</td>

   <td width="167">DD-MM-SS.MASDirection</td>

   <td width="129">Degrees, minutes, seconds,                milliarcseconds followed by either N or S.</td>

  </tr>

  <tr>

   <td width="136">Longitude</td>

   <td width="167">DD-MM-SS.MASDirection</td>

   <td width="129">Degrees, minutes, seconds, milliarcseconds followed by either E or W.</td>

  </tr>

  <tr>

   <td width="136">Airport Ownership</td>

   <td width="167">Public or Private</td>

   <td width="129">2 characters</td>

  </tr>

  <tr>

   <td width="136">Part 139</td>

   <td width="167">FAA Regulation</td>

   <td width="129">No data</td>

  </tr>

  <tr>

   <td width="136">NPIAS Service Level</td>

   <td width="167">National     Plan  IntegratedAirport Systems Descriptor</td>

   <td width="129">~10 characters</td>

  </tr>

  <tr>

   <td width="136">NPIAS Hub Type</td>

   <td width="167">Intentionally left blank</td>

   <td width="129">n/a</td>

  </tr>

  <tr>

   <td width="136">Airport Control Tower</td>

   <td width="167">Y/N</td>

   <td width="129">one character</td>

  </tr>

  <tr>

   <td width="136">Fuel</td>

   <td width="167">Fuel types available</td>

   <td width="129">up to 6 characters</td>

  </tr>

  <tr>

   <td width="136">Other Services</td>

   <td width="167">Collections of tag indicating INSTRuction, etc.</td>

   <td width="129">12 characters</td>

  </tr>

  <tr>

   <td width="136">Based Aircraft Total</td>

   <td width="167">Number of aircraft (may be blank)</td>

   <td width="129">Integer number</td>

  </tr>

  <tr>

   <td width="136">Total Operations</td>

   <td width="167">Takeoffs/Landings/etc (may be blank)</td>

   <td width="129">Integer number</td>

  </tr>

 </tbody>

</table>

<h1>2      Outputs</h1>

The outputs of the program will be populated Struct airPdata data. This data will be formatted so as to provide output as defined in the following sections.

<h2>2.1     Data Structure</h2>

The structure struct airPdata is described below. Please note the correlation with the data file’s <em>Field Names </em>refer to Table 1 on page 3 for more information. <em>NB The Javascript APIs for plotting geographic data REQUIRES that longitude is before latitude.</em>

typedef struct airPdata{

char *LocID;        //Airport’s ‘‘Short Name’’, ie MCO char *fieldName; //Airport Name char *city;                //Associated City float longitude; //Longitude float latitude; //Latitude

} airPdata;

<h2>2.2     File output</h2>

The file output for this assignment is <em>stdout</em>, aka the console. Make sure there is a headline that names each column. For example:

code,name,city,lat,lon

DAB,DAYTONA BEACH INTL,DAYTONA BEACH,29.1797,-81.0581

FLL,FORT LAUDERDALE/HOLLYWOOD INTL,FORT LAUDERDALE,26.0717,-80.1494

GNV,GAINESVILLE RGNL,GAINESVILLE,29.6900,-82.2717

JAX,JACKSONVILLE INTL,JACKSONVILLE,30.4939,-81.6878

EYW,KEY WEST INTL,KEY WEST,24.5561,-81.7594

LAL,LAKELAND LINDER RGNL,LAKELAND,27.9889,-82.0183

MLB,MELBOURNE INTL,MELBOURNE,28.1025,-80.6450

MIA,MIAMI INTL,MIAMI,25.7953,-80.2900

APF,NAPLES MUNI,NAPLES,26.1522,-81.7756

SGJ,NORTHEAST FLORIDA RGNL,ST AUGUSTINE,29.9592,-81.3397

ECP,NORTHWEST FLORIDA BEACHES INTL,PANAMA CITY,30.3581,-85.7956

OCF,OCALA INTL-JIM TAYLOR FIELD,OCALA,29.1717,-82.2239 MCO,ORLANDO INTL,ORLANDO,28.4292,-81.3089

Things to note:

<ul>

 <li>Digital degrees are expressed as floating point numbers of varying digits of precision. This is an artifact of <em>Javascript</em>. In this exercise 4 digits to the right of the decimal point is sufficient.</li>

 <li>The first line of the file identifies the field names. This is a material fact and will adversely impact the output of the data in the webpage. <em>Capitalization and spelling matter – and must match the first line above.</em></li>

 <li>The text shown above has been converted to uppercase as a piece of information to help debugging. String case conversion is not required for this exercise.</li>

</ul>

Once the output has been verified, redirect the <em>stdout </em>to a file named myTestAirports.csv. Move this file to the unpacked HW3 directory for testing. <em>Yes, validation of the correct output will occur on a browser enabled PC. </em>Make sure that all code, inputs, and outputs are built, tested, and the output file is exported from <em>Eustis</em>.

<h1>3      Processing</h1>

The primary goal is to provide programmatic access to the data from the input CSV file. This must be accomplished using standard C file IO techniques. Also note that it is vital to utilize the <em>stuct airPdata </em>for all data retrieval/extraction and conversion. Likewise, use of the <em>stuct airPdata </em>is required for the file output.

<h2>3.1     Reading the input</h2>

There are several approaches to read the input. Perhaps the most important consideration is reading the line in for each airport. Please note that there is one line per airport. Also note, that once the line is read into the input buffer it might be advantageous to parse the input buffer based on the <em>comma </em>delimiter.

There are several approaches possible. Make sure to test on <em>Eustis </em>as line termination characters/behaviors vary amongst operating systems.

<em>Make sure that the output file is formatted with decimal degrees.</em>

<h2>3.2     Processing the data structure</h2>

The data conversions for this assignment, specified below, require a certain degree of parsing and calculation. Initially reading the input is to your advantage to deal with all data elements as <em>character data</em>. And then process the <em>latitude </em>and <em>longitude</em>, hereinafter referred to as <em>degrees</em>. The <em>degrees </em>are expressed as <em>sexagesimal (base 60) </em>numbers. Their respective value is defined in the two tables below.

<h3>3.2.1       Latitude/Longitude Input</h3>

The <em>latitude </em>and <em>longitude </em>are both degrees, expressed as shown in the table below.

Table 2: Degrees

<table width="416">

 <tbody>

  <tr>

   <td width="79">Placeholder</td>

   <td width="154">Name</td>

   <td width="92">Value</td>

   <td width="92">Decimal</td>

  </tr>

  <tr>

   <td width="79">DD</td>

   <td width="154">Degrees</td>

   <td width="92">180</td>

   <td width="92">0-180</td>

  </tr>

  <tr>

   <td width="79">MM</td>

   <td width="154">Minutes</td>

   <td width="92">0-59</td>

   <td width="92"><em><u>value </u></em>60</td>

  </tr>

  <tr>

   <td width="79">SS.MAS</td>

   <td width="154">Seconds.MilliArcSeconds</td>

   <td width="92">0-59.0-9999</td>

   <td width="92"><em><u>value </u></em>60<sup>2</sup></td>

  </tr>

  <tr>

   <td width="79">D</td>

   <td width="154">Direction</td>

   <td width="92">N,S,E,W</td>

   <td width="92">See Table 3</td>

  </tr>

 </tbody>

</table>

Table 3: Direction

<table width="207">

 <tbody>

  <tr>

   <td width="71">Unit</td>

   <td width="48">Name</td>

   <td width="89">Decimal Sign</td>

  </tr>

  <tr>

   <td width="71">Latitude</td>

   <td width="48">NS</td>

   <td width="89">+–</td>

  </tr>

  <tr>

   <td width="71">Longitude</td>

   <td width="48">EW</td>

   <td width="89">+–</td>

  </tr>

 </tbody>

</table>

The conversion of the DDD-MM-SS.MASD string is shown in Table 2 above. The formula to convert a <em>sexagesimal </em>degree measurement to a digital degree measurement is shown below.

<em>degrees<sup>decimal </sup></em>=±<em>DDD </em>+ <em>MM/</em>60+ <em>SS.MAS/</em>60<sup>2</sup>

Note that the ± is derived from the information in Table 3 above.

3.2.2 Function float sexag2decimal(char *degreeString);

Description: Convert the <em>sexagesimal </em>input string of <em>chars </em>to a decimal degree based on the formula in Tables 2 and 3.

Special Cases: If a NULL pointer is passed to this function, simply return 0.0. Similarly, if the DD-MM-SS.MASD fields have invalid or out-of-range data, return

0.0.

Caveat: Even though the <em>valid </em>range of Degrees is from 0 to 180, the data files for the Continental US and Florida are from 0 to 99. Make sure that the conversion can handle all valid cases correctly.

Hint: Take care to make sure the values for each numeric component are within their valid ranges. Refer to Table 2 for the ranges.

Returns: A floating point representation of the calculated <em>decimal degrees </em>or 0.0 in the special cases mentioned above.

<h2>3.3     Testing</h2>

There will be two files provided for program testing. They are described below. The program’s output will be to <em>stdout</em>. Redirect the output to the test named <em>myAirports.csv</em>. This specifically named file can then be copied to the <em>HW3 </em>folder for testing with the webpage named <em>plotFlorida.html </em>in that folder.

The input file used in <em>Homework 1 </em>will be used as an additional testing file. Errors will induced for the <em>degrees</em>.

Table 4: Test Files

<table width="376">

 <tbody>

  <tr>

   <td width="134">Filename</td>

   <td width="243">Description</td>

  </tr>

  <tr>

   <td width="134">FL-RAW-airports.csv</td>

   <td width="243">A list of the 25 public Florida airports, wherein all the data is formatted as defined in the Input Specfication.</td>

  </tr>

  <tr>

   <td width="134">FL-airports-PLOT.csv</td>

   <td width="243">All 25 airports’ data formatted as defined in the Output Specification.</td>

  </tr>

 </tbody>

</table>

<h1></h1>