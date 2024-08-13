### Documentation Automated

**GitHub Pull Request Retrieval Documentation**
**Overview**
**This documentation provides a guide on how to retrieve a specific pull request from a GitHub repository using the GitHub API. The process involves sending an HTTP GET request to the GitHub API endpoint for pull requests, with proper authorization and targeting a specific pull request by its number.**

**Prerequisites**
Before you can retrieve a pull request, ensure you have the following:

- A GitHub account with access to the repository.
- A personal access token (PAT) with the appropriate permissions to access repository data.
- The owner's username of the repository.
- The repository name.
- The pull request number you wish to retrieve.
- Environment Setup
- Environment Variables: Store sensitive information such as the personal access token, the repository owner's username, and the repository name as environment variables to keep them secure.

**Load Environment Variables: Use the dotenv package to load the environment variables from a .env file.**

Retrieving a Pull Request
### Step 1: Define Environment Variables
Create a .env file in your project directory and add the following variables:

PR_REVIEW_BOT_TOKEN='your_personal_access_token'
PR_REVIEW_BOT_OWNER='repository_owner_username'
PR_REVIEW_BOT_REPO_NAME='repository_name'

Replace the placeholder values with your actual token, user, and repository name.

### Step 2: Load Environment Variables
Use the dotenv package to load the environment variables:

from dotenv import load_dotenv, find_dotenv

load_dotenv(find_dotenv())

### Step 3: Set Authorization Header
Prepare the authorization header using the token:

import os

token = os.getenv("PR_REVIEW_BOT_TOKEN")
headers = {'Authorization': f'token {token}'}

### Step 4: Construct the Request URL
Combine the user and repo environment variables to form the pull request URL:

user = os.getenv("PR_REVIEW_BOT_OWNER")
repo = os.getenv("PR_REVIEW_BOT_REPO_NAME")

url = f'https://api.github.com/repos/{user}/{repo}/pulls/1'

### Step 5: Send the GET Request
Use the requests library to send an HTTP GET request to the GitHub API:

import requests

response = requests.get(url, headers=headers)

### Step 6: Handle the Response
Check if the request was successful and handle the response accordingly:

if response:
    data = response.json()
    print("GitHub Pull Request is caught")
else:
    print("GitHub Pull Request is not caught:")

If the request is successful, the pull request data will be available in the data variable as a JSON object. If the request fails, an error message will be printed.

**Conclusion**
This guide provides a step-by-step approach to retrieve a pull request from a GitHub repository using the GitHub API. Remember to handle your personal access token with care and never expose it in your code or version control systems.
