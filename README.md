# IDS 706: Python Template (Week 1)

## Project Description
In this repository, I created a Python template to be used for future projects, as part of my first assignment with IDS 706: Data Engineering Systems. 

## Features
- `.devcontainer`: Provides a standardized environment for code to run in; ensures that all developers in a project are using the same tools, libraries, dependencies, etc. 
- `.github`: A directory that contains GitHub-specific configuration files and settings. 
- `.vscode`: A directory that contains VSCode-specific configuration settings. 
- `.gitignore`: A special file used to specify which files/folders should be ignored by Git when tracking changes. 
- `Makefile`: A special file used to simplify common tasks with short commands (for example, make test, make install, etc.)
- `README.md`: A markdown file that provides an overview of the project. 
- `hello.py`: The main Python module that contains the main source code of the application.
- `requirements.txt`: A file that lists all of the Python dependencies required for the project to run. 
- `test_hello.py`: Contains tests that verify whether the main source code (in this case, `hello.py`) works as expected. 

## Setup Instructions
To set up this repository, I set up a local Python environment. The steps I took were: 

### 1. Create a new GitHub repository. 
On GitHub, I created a new repository, toggled "on" for adding a README, and included `.gitignore`. 

### 2. Clone the repository. 
Open the terminal and input the following: 
```
git clone [Web URL; in my case, it was: https://github.com/ammylin/IDS_706_python_temp.git]
```

### 3. Create new files in the repository. 
Input the following code into the terminal: 
``` 
touch Makefile
touch hello.py
touch test_hello.py
touch requirements.txt 
```

### 4. Create a Makefile. 
In Makefile, add: 
```
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

format:
	black *.py

lint:
	flake8 hello.py

test:
	python -m pytest -vv --cov=hello test_hello.py

clean:
    rm -rf __pycache__ .pytest_cache .coverage

all: install format lint test
```
This includes the `make install`, `make format`, `make lint`, `make test`, and `make clean` features; more on them below: 
- `make install`:  used to install the necessary dependencies or set up the project environment. This installs packages listed in `requirements.txt`, including tools like `pylint`, `flake8`, `pytest`, `click`, `black`, and `pytest-cov`.
- `make format`: formats the code according to preferred style guidelines. We format using `black`. 
- `make lint`: runs a linting tool, which analyzes the code for potential errors, stylistic issues, and bugs. We use `flake8` as our linting tool. 
- `make test`: runs the project's test suite using `pytest`, which allows us to write and execute tests to verify that the code behaves as expected.
- `make clean`: used to remove any generated files or artifacts from the build process to ensure that the next build does not have any leftovers from previous builds. 

### 5. Create a requirements.txt file. 
In requirements.txt, add the following, which is a list of all the external Python packages that this project depends on: 
```
pylint
flake8
pytest
click
black 
pytest-cov
```

### 6. Create a Python script. 
In `hello.py`, I created a simple Python script: 
```
def say_hello(name: str) -> str:
    """Return a greeting message to students in the IDS class."""
    return f"Hello, {name}, welcome to Data Engineering Systems (IDS 706)!"


def add(a: int, b: int) -> int:
    """Return the sum of two numbers."""
    return a + b
```

### 7. Create a test file. 
Then, to test `hello.py`, I added the following in `test_hello.py`: 
```
from hello import say_hello, add

def test_say_hello():
    assert (
        say_hello("Annie")
        == "Hello, Annie, welcome to Data Engineering Systems (IDS 706)!"
    )

def test_add():
    assert add(2, 3) == 5
```

### 8. Run the tests. 
Input ```make test``` into the terminal. 

### 9. Format and lint the code. 
Input ```make format``` and ```make lint``` into the terminal. 

### 10. Clean up the environment. 
Input ```make clean``` into the terminal. 

### 11. Commit and push your changes to GitHub. 
``` 
git add .
git commit -m "Initial commit with Python template setup"   
git push origin main
```

### 12. Enable GitHub Actions. 
GitHub Actions is a tool that allows us to automate tasks directly on GitHub. For example, you could set GitHub Actions to automatically run tests on your code every time you push changes. 

I added the following YAML code by navigating on GitHub to "Actions" --> "New workflow" --> "Set up a workflow yourself", then committed and pushed this file to my repository: 
```
name: Python Template for IDS706

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.11'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Lint with flake8
      run: flake8 hello.py
    - name: Run tests
      run: pytest --cov=hello
```

## Usage Examples

### Running the Application
After setting up the project, you can run the application by executing the following command in the terminal:
```
python hello.py
```

To run the tests that you created, use this command: 
``` make test ```

Similarly, refer to steps 8-10 in the setup instructions to format and lint the code. 


## Acknowledgments 
This template was created as part of IDS 706: Data Engineering Systems at Duke University. I referred to Professor Zhongyuan Yu's template and code to create this: https://github.com/zhongyuan-duke/IDS-706-week-1-template.git. 