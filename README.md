Documentation Automation

The pull request introduces several changes to `main.py`:

1. **Removed Imports:**
   - The `openai` import has been removed, indicating that OpenAI's API is no longer being used in this script.
   - The `find_dotenv` function from the `dotenv` package is no longer imported, suggesting that the environment loading process has been simplified.

2. **Environment Variable Loading:**
   - The comment above `load_dotenv()` has been updated to "# Load environment variables" for better clarity.

3. **Environment Variable Usage:**
   - The script no longer sets up OpenAI API-related environment variables (`OPENAI_API_KEY`, `OPENAI_API_TYPE`, `OPENAI_API_VERSION`, `OPENAI_API_BASE`). This change aligns with the removal of the `openai` import, indicating a shift away from using the OpenAI API in this script.

4. **API Headers:**
   - The headers for API requests are now defined immediately after the environment variables are set, streamlining the setup process.

5. **Pull Request URL Definition:**
   - The URL for GitHub pull requests is now clearly defined with a comment, improving code readability.

6. **Removed Code Logic:**
   - The entire block of code that fetched pull requests, processed them, and posted a review comment using the OpenAI API has been removed. This includes the conditional checks, API requests, and response handling.

7. **New Code Logic:**
   - The new code introduces a simplified flow for fetching pull requests from GitHub and posting a review comment. It includes error handling for unsuccessful API requests and exits the script if no pull requests are found or if there is an issue fetching the diff for the first pull request.
   - The script now prints the number of the last processed pull request.

8. **Review Comment Posting:**
   - The process for posting a review comment has been retained but simplified. The script now posts the raw diff text as the review comment without processing it through the OpenAI API.

In summary, the pull request refactors `main.py` by removing dependencies on the OpenAI API, simplifying the environment variable loading, and streamlining the process of fetching and handling pull requests from GitHub.