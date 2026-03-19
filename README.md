# Reverse Index using Hadoop Streaming

## Project Overview
This project implements a Reverse Index using Hadoop Streaming and Python scripts (`mapper.py` and `reducer.py`).  
The reverse index maps each word to the list of documents in which it appears, along with its frequency in each document.

### Output Format
word --> document1.txt:count, document2.txt:count, ...

Example:
hadoop --> book1.txt:12, book3.txt:5


## Files Included
- `mapper.py` → Mapper program
- `reducer.py` → Reducer program
- `run_reverse_index.sh` → Driver/execution script
- `stopwords.txt` → Stop-word list
- `README.md` → Instructions
- `Performance_Report.pdf` → Final report


## Preprocessing Implemented
The mapper performs:
1. Lowercasing all text
2. Removing punctuation
3. Tokenizing words
4. Removing stopwords using `stopwords.txt`


## Requirements
- Hadoop 3.2.1
- Hadoop Streaming JAR
- Python 3 installed in the execution environment
- HDFS input dataset stored in:

/user/hduser/library


## Running the Job

### Step 1: Upload books to HDFS
```bash
hdfs dfs -mkdir -p /user/hduser/library
hdfs dfs -put -f /shared/book_*.txt /user/hduser/library/

###Step 2
./run_reverse_index.sh /user/hduser/reverse_index_output

###Step 3
hdfs dfs -cat /user/hduser/reverse_index_output/part-* | head -20
