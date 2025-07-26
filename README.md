Will add read me info
- Added Ollama on local llama3.2:1b
-ollama run llama3.2 for chatbot
- Ollama: Free alternative to Paid APIs (but please see Warning about llama version)
Ollama is a product that runs locally on your machine. It can run open-source models, and it provides an API endpoint on your computer that is compatible with OpenAI.

First, download Ollama by visiting: https://ollama.com

Then from your Terminal in Cursor (View menu >> Terminal), run this command to download a model:

ollama pull llama3.2
WARNING: Be careful not to use llama3.3 or llama4 - these are much larger models that are not suitable for home computers.

And now, any time that we have code like:
openai = OpenAI()
You can use this as a direct replacement:
openai = OpenAI(base_url='http://localhost:11434/v1', api_key='ollama')
And also replace model names like gpt-4o-mini with llama3.2.

You don't need to put anything in your .env file for this; with Ollama, everything is running on your computer. You're not calling out to a third party on the cloud, nobody has your credit card details, so there's no need for a secret key! The code api_key='ollama' above is only required because the OpenAI client library expects an api_key to be passed in, but the value is ignored by Ollama.

Below is a full example:

# You need to do this one time on your computer
!ollama pull llama3.2

from openai import OpenAI
MODEL = "llama3.2"
openai = OpenAI(base_url="http://localhost:11434/v1", api_key="ollama")

response = openai.chat.completions.create(
 model=MODEL,
 messages=[{"role": "user", "content": "What is 2 + 2?"}]
)

print(response.choices[0].message.content)
You will need to make similar changes to use Ollama within any of the Agent Frameworks - you should be able to google for an exact example