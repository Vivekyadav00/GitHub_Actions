i have created a files .github/workflows/first-actions.yml   .github/workflows/self-hosted.yml     src/addition.py              on github for performing ci/cd using github actions  
 we can do ci/cd actions using github in two ways 
1.using github actions itself
2. self hosted runner 

1. github actions
   
   created file with source code src/addition.py
   
def add(a, b):

    result = a + b
    print(f"Adding {a} and {b} gives {result}")
    return result

def test_add():

    assert add(1, 2) == 3
    assert add(-1, 1) == 0
    assert add(0, 0) == 0
    assert add(1.5, 2.5) == 4 and 
    
and .github/workflows/first-actions.yml 
name: My First GitHub Actions

on: [push]

jobs:

  build:
  
    runs-on: ubuntu-latest



on the above i mentioned   runs-on: ubuntu-latest. which means it runs on ubuntu terminal. github tests the above source code every time for the everypush in source code i.e in addition.py.
 thats how we can build ci/cd pipeline on github. one disadv of this method   is security, we didnt have any information about the hosts and their  location. if the hosts is shared between the multiple oragnizaations . their is a possibility of security issues.


2 self hosted runners

In the self hosted runners we create our own ec2 instance and we change our security groups inbound and outbound rules to allow ec2 to interact with http and https.  Created file of   .github/workflows/self-hosted.yml 
name: My First GitHub Actions

on: [push]

jobs:

  build:
  
    runs-on: self-hosted

in the code we mentioned runs-on: self-hosted

On github settings - actions-runners- activated so it provided with the commands to be executed in our self host to connect with github. Once the connection is made for every change in the source code, ec2 will execute the code for testing. In the source code we have addition function in python. We try test the execution of the python using the python version 3.9.


Using GitHub Actions Runner
Setup:

Source code: src/addition.py

Workflow configuration: .github/workflows/first-actions.yml

Runs on: ubuntu-latest

Testing: Python versions 3.8 and 3.9

Workflow:

Check out the repository.

Set up Python.

Install dependencies.

Verify the existence of the src directory.

Run tests using Pytest.

Execution:

The workflow runs automatically on each push to the repository.

The GitHub-hosted runner handles the execution in a secure, isolated environment.
Advantages:

Easy setup and configuration.

Managed environment by GitHub, ensuring consistency and reliability.

Disadvantages:

Limited control over the execution environment.

Potential security concerns due to shared infrastructure.

Using Self-Hosted Runner

Setup:

Launch an AWS EC2 instance.

Configure security groups to allow HTTP and HTTPS traffic.

Connect to the instance via SSH.

Install necessary dependencies and configure the self-hosted runner using commands provided by GitHub.

Workflow Configuration:

Source code: src/addition.py

Workflow configuration: .github/workflows/self-hosted.yml

Runs on: self-hosted

Testing: Python version 3.9

Workflow:

Check out the repository.
Set up Python.

Install dependencies.

Verify the existence of the src directory.

Run tests using Pytest.

Execution:

The self-hosted runner on the EC2 instance executes the workflow whenever changes are pushed to the repository.

Advantages:

Full control over the execution environment.
Enhanced security by isolating the runner to your infrastructure.

Disadvantages:

Requires additional setup and maintenance.
Potential costs associated with running EC2 instances.

Conclusion

This projectshowcases the implementation of CI/CD pipelines using GitHub Actions in two ways: GitHub-hosted runners and self-hosted runners. By leveraging GitHub Actions, Python, Pytest, and AWS EC2, the project demonstrates how to automate testing and ensure code quality for a Python application.

The GitHub-hosted runner provides a straightforward and managed environment for running CI/CD pipelines, while the self-hosted runner offers more control and security by utilizing dedicated infrastructure. Both approaches ensure that the tests are run automatically on each code change, enhancing the development workflow and improving code quality.

