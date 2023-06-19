Github Automated Analysis

In this project,  i build a Python-based tool which, when given a GitHub user's URL, returns the most technically complex and challenging repository from that user's profile. The tool will use GPT and LangChain to assess each repository individually before determining the most technically challenging one. 

Requirements: 

1. Fetch a user’s repositories from their GitHub user URL. 

2. Preprocess the code in repositories before passing it into GPT. Specifically, implement memory management techniques for large repositories and the files within them. Consider that repositories may contain large Jupyter notebooks or package files which, if passed raw through GPT, would greatly exceed token limits. 

3. Implement prompt engineering when passing code through GPT for evaluation to determine its technical complexity. 

4. Identify which of the repositories is the most technically complex. Use GPT to justify the selection of the repository. 

5. Deploy your solution on a hosting platform like Vercel, Netlify, or GitHub pages. The interface should include a simple text box where users can input a GitHub user URL for analysis. Then, the interface should display a link to the most complex repository as well as GPT analysis justifying the selection. 


The code you provided is a Flask application that fetches GitHub repositories for a given user, calculates the complexity score of the longest repository, and displays the result on a web page.

Let's go through the code and explain each section:

1. Importing the required libraries:
   - `tkinter` for GUI components (not used in this code)
   - `requests` for making HTTP requests to the GitHub API
   - `urlparse` from `urllib.parse` for parsing the user URL
   - `GPT2Tokenizer` and `GPT2LMHeadModel` from `transformers` for text generation using the GPT-2 model
   - `Flask`, `render_template`, and `request` from `flask` for creating the web application

2. Initializing the Flask application:
   - `app = Flask(_name_)` creates a Flask application instance.

3. Defining the `evaluate_complexity` function:
   - This function takes a repository name as input.
   - It initializes a GPT-2 tokenizer and model.
   - It generates a text prompt for evaluating the technical complexity of the repository using the GPT-2 model.
   - The generated output is passed to the `calculate_complexity_score` function to derive the complexity score.
   - The complexity score is returned.

4. Defining the `calculate_complexity_score` function:
   - This function takes the output from the GPT-2 model as input.
   - It processes the output by decoding it using the tokenizer and removing special tokens.
   - It counts the number of words in the processed output.
   - It defines a maximum complexity score.
   - The complexity score is determined as the minimum of the word count and the maximum complexity score.
   - The complexity score is returned.

5. Defining the Flask route:
   - The route `'/'` is specified for the root URL of the web application.
   - The route handles both GET and POST requests.
   - If a POST request is received, it retrieves the user URL from the form data.
   - It extracts the GitHub username from the user URL using `urlparse`.
   - It constructs the GitHub API URL to fetch the user repositories.
   - It makes a request to the GitHub API and retrieves the repository data as JSON.
   - If repositories are found, it processes the repositories to find the longest repository name.
   - It calls the `evaluate_complexity` function to calculate the complexity score of the longest repository.
   - It renders the `index.html` template with the repository name and complexity score as template variables.
   - If no repositories are found, it renders the `index.html` template with an error message.
   - If an exception occurs during the request, it renders the `index.html` template with an error message.

6. Running the Flask application:
   - The `if _name_ == '_main_':` block ensures that the Flask application runs only when the script is executed directly.
   - It starts the Flask development server with debugging enabled.

Overall, this code defines a Flask application that allows users to enter a GitHub user URL, fetches the user's repositories, calculates the complexity score of the longest repository using the GPT-2 model, and displays the result on a web page.
