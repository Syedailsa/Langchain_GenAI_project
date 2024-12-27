Project 01: Langchain Hello World
Prerequisites
Python Environment: Ensure you have Python installed.

Google Colab: This notebook is designed to run in Google Colab.

Google Gemini API Key: Obtain your API key for Google Gemini and save it in the Colab environment using userdata.

Installation
Install the required libraries:

!pip install langchain

Code Explanation
1. Import Libraries

from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from google.colab import userdata
from langchain_google_genai import ChatGoogleGenerativeAI
2. Setup API Key

The API key is securely fetched from userdata:

gemini_api_key = userdata.get('GEMINI_API_KEY')

3. Configure the LLM

Set up the Google Gemini Flash model with desired parameters:

llm = ChatGoogleGenerativeAI(
    model="gemini-1.5-flash",
    max_retries=2,
    temperature=0.2,
    api_key=gemini_api_key
)
4. Create a Prompt Template

Define a prompt template to customize how the model responds:

prompt_template = PromptTemplate(
    input_variables=["question"],
    template="You are a helpful assistant. Answer the following question:\n\n{question}"
)
5. Initialize the Chain

Combine the LLM and the prompt template into an executable chain:

chain = LLMChain(llm=llm, prompt=prompt_template)
6. Run the Chain

Pass a question to the chain and print the response:

question = "What is LangChain?"
response = chain.run({"question": question})

print('='*40)
print("Question:", question)
print("Answer:", response)
