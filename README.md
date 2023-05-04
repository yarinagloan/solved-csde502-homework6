Download Link: https://assignmentchef.com/product/solved-csde502-homework6
<br>
<strong>Instructions: </strong>

<ol>

 <li>Fill in your name and UWNetID above.</li>

 <li>Put answers to the questions on this document, using the “00Answers” Word style so your answers are clearly distinguished from the questions.</li>

 <li>Create a PDF file from this document.</li>

 <li>Create a <strong>single zip</strong> file including this document as a PDF file, along with the RDS file and R code file.</li>

 <li>Upload the <strong>single zip file</strong> to Canvas.</li>

</ol>







<strong>Explanation:</strong>

For this assignment, you will be perusing some of the documentation for the Add Health Wave 1 data set. You will use the documentation to make some updates to a data frame containing some of the Add Health data, and then save the data frame as an RDS file. You will update a metadata table that partially describes the data set and changes you made to the variable names and variable labels.




To open a Stata version 13 file in R there are two main options:




<ol>

 <li>Use haven::read_dta(). To access variable labels in R use labelled::foreign_to_labelled(). To update variable labels, use the labelled::var_label()</li>

 <li>Use readstata13::read.dta13(). Variable labels for this format are available, e.g., for a data frame named dat as attributes(dat)$var.labels. This is a vector of text strings that can be updated by assigning a new value to the specified element, e.g.,attributes(dat)$var.labels[1] &lt;- “foo”.</li>

</ol>




To save the RDS file, use the base function saveRDS().




Here is a base R code snippet that will rename a single variable:




colnames(data_frame)[grep(“^original_variable_name$”, colnames(data_frame))] &lt;- new_variable_name




The grep() function finds the position of the named variable in the list of variables in the data frame. The characters ^ and $ are regular expressions to specify the start and end of the string to be matched (assuring that the pattern does not match multiple similar variable names).




It is much simpler with tidyverse and magrittr:




data_frame %&lt;&gt;% rename(new_variable_name = old_variable_name)




Additional hint for dealing with PDF documentation:

<ol>

 <li>Use pdfgrep (should be available in a Linux or Mac package manager; for Windows, search for a version or use Cygwin).</li>

 <li>Use the R pdftools This could be used in a loop over each PDF file to create a data frame with the name of the PDF file, page number, and text of each page. The str_match() function could be used to identify the file name and page number where specific text strings occur. For a minimal example, this shows that the string “h1gi1m” is found on page 1 of INH01PUB.PDF. Conversion of the PDF file’s text to lowercase simplifies the matching:</li>

</ol>




&gt; x &lt;- pdftools::pdf_text(pdf = “INH01PUB.PDF”)

&gt; str_match(string = x %&gt;% str_to_lower(), pattern = “h1gi1m”)

[,1]

[1,] “h1gi1m”

[2,] NA

[3,] NA

[4,] NA

[5,] NA

[6,] NA

[7,] NA

[8,] NA

[9,] NA

[10,] NA

[11,] NA

[12,] NA

[13,] NA

[14,] NA

[15,] NA







<strong>Questions:</strong>

<ol>

 <li>Explore the Add Health website (<a href="http://www.cpc.unc.edu/projects/addhealth">http://www.cpc.unc.edu/projects/addhealth</a>) and answer the following questions (making sure to cite as necessary):

  <ul>

   <li>What was the sampling frame for this study?</li>

  </ul></li>

</ol>




The sampling frame for the Add Health study was all high schools included in the Quality Education Database (QED). High school was defined as schools with an 11<sup>th</sup> grade and more than 30 students.




<ul>

 <li>What were the three kinds of respondents at Wave I?</li>

</ul>




<ul>

 <li>What was the instrument with the largest sample size?</li>

</ul>




<ul>

 <li>Is it possible for a respondent to be in Wave III without being in Wave II?</li>

</ul>




<ul>

 <li>What is the time span of the Add Health data collection (all waves)?</li>

</ul>




<ul>

 <li>What is the difference between the public and the restricted-use Add Health data?</li>

</ul>




<ul>

 <li>Describe a research question that you might be able to answer using the Add Health dataset.</li>

</ul>










<ol start="2">

 <li>Download the public-use Add Health documentation at <a href="https://canvas.uw.edu/courses/1434040/files">https://canvas.uw.edu/courses/1434040/files</a>. Answer the following questions:</li>

</ol>




<ul>

 <li>In what pdf document is the documentation for the race items for the Wave I In-Home questionnaire?</li>

</ul>




<ul>

 <li>How many respondents were of Hispanic/Latino origin?</li>

</ul>




<ul>

 <li>What is the “Knowledge Quiz” in the Wave I In-Home questionnaire?</li>

</ul>




<ul>

 <li>What is the unique identifier for the In-home data?</li>

</ul>










<ol start="3">

 <li>Download the Stata 13 format file AHwave1_v1.dta (<a href="https://staff.washington.edu/phurvitz/csde502_winter_2021/data/AHwave1_v1.dta">http://staff.washington.edu/phurvitz/csde502_winter_2021/data/AHwave1_v1.dta</a>).</li>

</ol>




<ul>

 <li>Fill in the grey missing cells in Table 1 below based on the data and/or documentation. Optimally, use the documentation to familiarize yourself with the structure of the code books.</li>

 <li>Using questions 6 and 8 in INH01PUB.PDF, create a new variable named “race” that uses recoded values (white = 1; black/African American = 2; American Indian = 3; Asian/Pacific Islander = 4; other = 5; unknown/missing = 9).</li>

 <li>Rename the variables, and update variable labels using Table 1 as a guide and save the data frame as the file as <strong>rds</strong>. Use a single R code file for your edits to the data file.</li>

 <li>Update the status in Table 1 as needed.</li>

</ul>




Table 1: Codebook for variables from Add Health Wave 1 data




<table width="776">

 <tbody>

  <tr>

   <td><strong>newvariablename</strong></td>

   <td><strong>originalvariablename</strong></td>

   <td><strong>status*</strong></td>

   <td width="60"><strong>datatype</strong></td>

   <td width="94"><strong>values</strong></td>

   <td width="273"><strong>newvariablelabel</strong></td>

   <td><strong>codebookfilename</strong></td>

  </tr>

  <tr>

   <td>aid</td>

   <td>aid</td>

   <td>unchanged</td>

   <td width="60">text</td>

   <td width="94">8 digit string</td>

   <td width="273">unique case (student) identifier</td>

   <td>SECTAPUB.PDF</td>

  </tr>

  <tr>

   <td>imonth</td>

   <td>imonth</td>

   <td>unchanged</td>

   <td width="60">integer</td>

   <td width="94">14 to 12</td>

   <td width="273">month interview completed</td>

   <td>SECTAPUB.PDF</td>

  </tr>

  <tr>

   <td>iday</td>

   <td>iday</td>

   <td>unchanged</td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">day interview completed</td>

   <td>SECTAPUB.PDF</td>

  </tr>

  <tr>

   <td>iyear</td>

   <td>iyear</td>

   <td>unchanged</td>

   <td width="60"> </td>

   <td width="94">94, 95</td>

   <td width="273"> </td>

   <td>SECTAPUB.PDF</td>

  </tr>

  <tr>

   <td>bio_sex</td>

   <td>bio_sex</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">interviewer confirmed sex</td>

   <td> </td>

  </tr>

  <tr>

   <td>bmonth</td>

   <td>h1gi1m</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">birth month</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>byear</td>

   <td>h1gi1y</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">birth year</td>

   <td> </td>

  </tr>

  <tr>

   <td>hispanic</td>

   <td>h1gi4</td>

   <td>renamed</td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">Hispanic/Latino</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>white</td>

   <td>h1gi6a</td>

   <td>renamed</td>

   <td width="60"> </td>

   <td width="94">0 = not marked1 = marked6 = refused8 = don’t know</td>

   <td width="273">   race white</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>black</td>

   <td> </td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">race black or African American</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>AI</td>

   <td>h1gi6c</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">race American Indian or Native American</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>asian</td>

   <td>h1gi6d</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">race Asian or Pacific Islander</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>raceother</td>

   <td>h1gi6e</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">race other</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>onerace</td>

   <td> </td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">one category best describes racial background</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>observedrace</td>

   <td>h1gi9</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">interviewer observed race</td>

   <td>INH01PUB.PDF</td>

  </tr>

  <tr>

   <td>health</td>

   <td>h1gh1</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">how is your health</td>

   <td> </td>

  </tr>

  <tr>

   <td>race</td>

   <td>not applicable</td>

   <td> </td>

   <td width="60"> </td>

   <td width="94"> </td>

   <td width="273">race recoded as white; black/African American; American Indian; Asian/Pacific Islander; other; unknown/missing</td>

   <td> </td>

  </tr>

 </tbody>

</table>

*status categories: unchanged, renamed, missing defined, derived


