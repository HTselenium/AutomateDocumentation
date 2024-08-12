```markdown
Documentation Automated

### Pull Request Description

**Title:** Update main.py  
**Description:** Refactor the entire code space.

### Changes Summary

1. **Imports:**
   - Removed `openai` import.
   - Simplified `dotenv` import by removing `find_dotenv`.

2. **Environment Variables:**
   - Removed redundant `openai` environment variable setups.
   - Simplified `load_dotenv()` call.

3. **Headers:**
   - No changes to the headers setup.

4. **Pull Request URL:**
   - No changes to the URL setup.

5. **Fetching Pull Requests:**
   - Simplified the logic for fetching pull requests.
   - Removed nested if-else blocks for better readability.

6. **Processing Pull Requests:**
   - Simplified the logic to find the highest pull request number.
   - Improved error handling and exit conditions.

7. **Fetching Diff:**
   - Simplified the logic to fetch the diff for the first pull request.
   - Improved error handling and exit conditions.

8. **Posting Review Comment:**
   - Simplified the logic to post the review comment.
   - Removed the use of `openai.ChatCompletion.create` for generating the review.
   - Directly used the diff response text for the review comment.

### Detailed Changes

```diff
 import requests
 import os
-import openai
-from dotenv import load_dotenv, find_dotenv
+from dotenv import load_dotenv
 
-load_dotenv(find_dotenv())
+# Load environment variables
+load_dotenv()
 
+# Set up environment variables and headers
 token = os.getenv("PR_REVIEW_BOT_TOKEN")
 user = os.getenv("PR_REVIEW_BOT_OWNER")
 repo = os.getenv("PR_REVIEW_BOT_REPO_NAME")
-openai.api_key = os.getenv("OPENAI_API_KEY")
-openai.api_type = os.getenv("OPENAI_API_TYPE")
-openai.api_version = os.getenv("OPENAI_API_VERSION")
-openai.api_base = os.getenv("OPENAI_API_BASE")
-
 headers = {"Authorization": f"token {token}", "Accept": "application/vnd.github+json"}
 
+# Define the URL for the pull requests
 url = f"https://api.github.com/repos/{user}/{repo}/pulls"
-response = requests.get(url, headers=headers)
-
-if response.status_code == 200:
-    data = response.json()
-    if data:
-        last_processed_pr = max(pull_request["number"] for pull_request in data)
-        print(f"Last Processed Pull Request Number: {last_processed_pr}")
-
-        # Fetching diff for the first pull request
-        if "diff_url" in data[0]:
-            diff_url = data[0]["diff_url"]
-            diff_response = requests.get(diff_url, headers=headers)
-            if diff_response.status_code == 200:
-                # Fetching the last line of the diff
-                diff = diff_response.text
-
-                messages = [
-                    {
-                        "role": "system",
-                        "content": """You are a world-class helpful assistant. You are a superintelligent AI \
-                        with one mission: to provide as much descriptive as possible answers to \
-                        the users during a Pull Request Code Review. \
-                        Provide a detailed analysis on the changes made in a well-formatted form. \
-                        If any syntax or logic errors in the code, please provide recommendation to improve the code. \
-                        Always answer in English.""",
-                    },
-                    {
-                        "role": "user",
-                        "content": f"Please review the following pull request : {diff}",
-                    },
-                ]
-
-                response = openai.ChatCompletion.create(
-                    engine="gpt-4",
-                    messages=messages,
-                )
-
-                review = response.choices[0].message["content"].strip()
-                review = f"Review from GPT \n\n{review}"
 
-                print(diff)
-
-                comment_url = f"https://api.github.com/repos/{user}/{repo}/issues/{last_processed_pr}/comments"
-
-                comment_data = {"body": review, "user": "PR-Reviewer-Bot"}
-
-                comment_response = requests.post(
-                    comment_url, json=comment_data, headers=headers
-                )
-
-                if comment_response.status_code == 201:
-                    print("Review successfully posted on GitHub.")
-                else:
-                    print(
-                        f"Failed to post review. Status code: {comment_response.status_code}"
-                    )
-                    print(f"Response: {comment_response.json()}")
-            else:
-                print(f"Failed to fetch diff for PR: {diff_response.status_code}")
-        else:
-            print("No diff_url found for the first pull request")
-    else:
-        print("No Pull Requests Found")
-else:
+# Get the list of pull requests
+response = requests.get(url, headers=headers)
+if response.status_code != 200:
     print("Failed to fetch pull requests.")
+    exit()
+
+# Process the pull requests
+data = response.json()
+if not data:
+    print("No Pull Requests Found")
+    exit()
+
+# Find the highest pull request number
+last_processed_pr = max(pr["number"] for pr in data)
+print(f"Last Processed Pull Request Number: {last_processed_pr}")
+
+# Fetch the diff from the first pull request
+diff_url = data[0].get("diff_url")
+if not diff_url:
+    print("No diff_url found for the first pull request")
+    exit()
+
+diff_response = requests.get(diff_url, headers=headers)
+if diff_response.status_code != 200:
+    print(f"Failed to fetch diff for PR: {diff_response.status_code}")
+    exit()
+
+# Post the review comment
+comment_url = f"https://api.github.com/repos/{user}/{repo}/issues/{last_processed_pr}/comments"
+review = f"Review from GPT \n\n{diff_response.text}"
+comment_data = {"body": review}
+comment_response = requests.post(comment_url, json=comment_data, headers=headers)
+
+if comment_response.status_code == 201:
+    print("Review successfully posted on GitHub.")
+else:
+    print(f"Failed to post review. Status code: {comment_response.status_code}")
+    print(f"Response: {comment_response.json()}")
```
```