# UNOS Registry Extraction
This repository is used for ETL code for medical transplant data from the UNOS Registry of transplants.

## Data Source
Data was downloaded from UNOS website after agreeing to Data Use Agreement. The data tables were in two formats:

- SAS
- DAT (Flat file)

Because SAS is an absolute pain to deal with, and luckily `pandas` in python has functions to deal with it, the first step is to convert it to SQLite for ease of manipulation.

Because these data files were so massive, I was unable to read the SAS files directly into memory for serialization. As a result, the SAS files needed to be 'chunked' into sizes of 10,000 rows. On each chunk, the columns were converted to string if they were written/saved as binary (If I ever have to work with SAS files again, I swear I am going to burst an aneurysm). Then, the rows were appended to a SQLite database for easy use.

## Files

### database.py
Used to convert SAS files to table in a local SQLite database.

### extractor.py
Used to extract all rows that correspond to the year 2010 from the database for initial visualization/exploration.
