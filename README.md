# Introduction
The provided code is for a Question Generator tool that takes a PDF document as input and generates a list of questions based on the document's content. This tool can generate both subjective and objective questions. The number of questions this tool generates is also user-defined, i.e., users can define how many questions they want.

# Installation
## Create a Python Virtual Environment
A Python virtual environment is recommended to isolate your project's dependencies. Follow these steps to create and activate a virtual environment:

### On Windows:
```bash
# Install virtualenv (if not already installed)
pip install virtualenv

# Create a virtual environment (replace 'myenv' with your preferred environment name)
virtualenv myenv

# Activate the virtual environment
myenv\Scripts\activate
```
### On macOS and Linux:
```bash
# Create a virtual environment (replace 'myenv' with your preferred environment name)
python3 -m venv myenv

# Activate the virtual environment
source myenv/bin/activate
```
Your virtual environment is now active, and you can install the required libraries within it.

## Install Required Libraries
### Using requirements.txt file
To install the libraries from the `requirements.txt` file, use the following command:
```bash
pip install -r requirements.txt
```
This command will install all the libraries specified in the `requirements.txt` file into your virtual environment, but we have to install the `en_core_web_sm` and `s2v reddit` model separately.

For the installation of the `en_core_web_sm` model.
```bash
pip install spacy-model-manager
spacy-model install en_core_web_sm
```
For the `s2v reddit` model.
```bash
wget https://github.com/explosion/sense2vec/releases/download/v1.0.0/s2v_reddit_2015_md.tar.gz
tar -xvf  s2v_reddit_2015_md.tar.gz
```

### Using the independent installation of the libraries (Recommended way)
In case the above `requirements.txt` installation is not working
```bash
pip install PyPDF2
pip install transformers
pip install spacy-model-manager
spacy-model install en_core_web_sm
pip install transformers[sentencepiece]
pip install sentencepiece

wget https://github.com/explosion/sense2vec/releases/download/v1.0.0/s2v_reddit_2015_md.tar.gz
tar -xvf  s2v_reddit_2015_md.tar.gz

pip install sense2vec==2.0.0
pip install strsim==0.0.3
pip install sentence-transformers==2.2.2
```

# Usage Guide
Now that your virtual environment is set up and the required libraries are installed, you can use the Question Generator. Remember to activate your virtual environment every time you work on the project.


## PDF File Path
In the end of the main.py file, enter the path of the PDF file
```bash
pdf_path = 'Path of the File'
```
## Number of Questions
In the end of the main.py file, enter the desired number of questions in the `num_questions=`
```bash
qa_list = qg.generate(
    text,
    num_questions=10,
    use_evaluator=True,
    answer_style='multiple_choice'
)
```
If the chosen number of questions is too large, then the model may not be able to generate enough. The maximum number of questions will depend on the length of the input text, or more specifically the number of sentences and named entities contained within the text. Note that the quality of some of the outputs will decrease for larger numbers of questions, as the QA Evaluator ranks generated questions and returns the best ones.

## Answer styles
This tool can generate both multiple-choice and subject questions and answers. In the end of the main.py file, enter the type of the question in the `answer_style=`
```bash
qa_list = qg.generate(
    text,
    num_questions=10,
    use_evaluator=True,
    answer_style='multiple_choice'
)
```
For subjective questions and answers  `answer_style='sentences'` and for the multiple choice questions and answers `answer_style='multiple_choice'`

## QA Evaluator
By utilizing the QA Evaluator it gives us the top k questions and answers. In the end of the main.py file `use_evaluator=` , enter `True` for utilizing the QA Evaluator for random question-answer pairs put `False`.
```bash
qa_list = qg.generate(
    text,
    num_questions=10,
    use_evaluator=True,
    answer_style='multiple_choice'
)
```
### After checking all the above-mentioned arguments, you can run the main.py file in the terminal
```bash
python main.py
```
