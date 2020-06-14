# Lab 2 Data cleaning and manipulation

The shark attacks dataset used in the project is the unholiest dataset ever to be produced.
My efforts at cleaning it were only partially successfull. It is definitely better than it was in the beginning, but there's still a lot that's messy and I wouldn't use it if my life depended on it.

Many of the problems I found were fixable, but others required more information than was available in the data. 
The major problem and frustration was the sheer variety of errors in each column. I sincerely hope this was fabricated as a teaching material; I can't begin to imagine how someone could possibly mess things up so magnificently if it wasn't on purpose. 



## Workflow

### 1. Loaded the dataset (with Pandas)
### 2. Examined the data
### 3. Removed whitespace from some of the column names 
### 4. Removed duplicate rows and rows containing only NAs
### 5. Cleaning column by colum

#### 5.1 Case Number, Case Number.1 and Case Number.2
These columns were practically identical, with only a few rows with different values in each column. Since these differences affected a *very* small percentage of the data, I removed columns Case Number.1 and Case Number.2.
A few rows had only zeroes or xx in column Case Number, with all other columns containing NAs, so I also removed these rows.

#### 5.2 Date
Converted all the entries I could into a %d-%m-%Y format, including some that had problems with special characters/separators. 

#### 5.3 Type
This one was simple, all I had to do was change a few misspelled entries and voilá.

#### 5.4 Country, Area and Location
These were reasonably clean. All I did was change the capitalization and remove leading/trailing whitespace.

#### 5.5 Name
This column was quite messy, but a kind of messy that I couldn't deal with easily. Many rows had sex information rather than names; for those, I checked if the Sex column contained anything and if it didn't I filled it with the information from the Name column. I then replaced the "male" or "female" entries in the Name column with NAs. There was still plenty of mess left behind, but I didn't know how to distinguish garbage text from names, so I left it like that.

#### 5.6 Sex column
After removing whitespace and standardizing a few misspelled entries, I replaced all entries that were not "M" or "F" with NA.

#### 5.7 Age
Another very messy column. Many of the values were ambiguous or not convertible to a numeric value (like "teens", or "40s"). I replaced anything that wasn't only a one or two-digit number with NA.

#### 5.8 Injury
I didn't touch this column aside from removing whitespace. 

#### 5.9 Fatal (Y/N)
Thank God for this column. It's so tidy now, Marie Kondo would be proud. I replaced a couple of entries with no real information with NA and standardized the others to "Y" or "N".

#### 5.10 Time
I converted what I could into a 14h00 format, replaced the rest with NA.

#### 5.11 Species
Probably the worst column in this whole dataset. 
I looked for the most common species names in this column. Then, for each species, I grouped all entries that contained that species name into one, leaving out any that also included words indicanting uncertainty ("possibly", "allegedly", "?"). I also grouped a few similar categories that were worded differently. I kept the 35 most common categories/species; everything else I lumped into a "Unidentified, unclear or other" category. Around 60% of the valid values were succesfully categorized, with the other 40% being part of the Unidentified... category. I didn't replace the original column, as it contained potentially useful information; this way, if the user is interested in a specific entry that is categorized as Unidentified..., they can alway refer to the original column.

#### 5.12 Investigator or Source
I didn't do anything to this column. It looked ok-ish.

#### 5.13 pdf
I found quite a few pdf file names with errors at the end of the file name, including whitespace where it shouldn't be, wrong characters, and no .pdf extension. I fixed those where I could.
I also found a lot of errors at the start of the pdf file name. Most pdf file names started with the Case number for that row; however, for quite a few file names the beginning of the name was different from the Case number; this isn't something I could correct, as I don't know which one is correct, the file name or the Case number. I left it as it was.

#### href and href formula
These two columns were practically the same. Where they differed, it was usually because of errors in the entry in the href column, where part of the URL was duplicated. Therefore, I removed the href column.
I tried to fix the broken URLs I found. Many I could fix, especially the ones with wrong endings; others I couldn't.

#### Original order
This seemed ok. 

#### Unnamed: 22 and Unnamed: 23
These columns were empty, aside from one record in each that didn't look like anything. I removed them.

### 6. Writing to a new csv file
