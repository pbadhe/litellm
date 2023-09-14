# Use Completion() for OpenAI, Azure

## Basic Completion()
```python
import os 
from litellm import completion

# openai configs
os.environ["OPENAI_API_KEY"] = ""

# azure openai configs
os.environ["AZURE_API_KEY"] = ""
os.environ["AZURE_API_BASE"] = "https://openai-gpt-4-test-v-1.openai.azure.com/"
os.environ["AZURE_API_VERSION"] = "2023-05-15"



# openai call
response = completion(
    model = "gpt-3.5-turbo", 
    messages= = [{ "content": "Hello, how are you?","role": "user"}]
)

# azure call
response = completion(
    model = "azure/<your-azure-deployment>",
    messages = [{ "content": "Hello, how are you?","role": "user"}]
)

```

## Completion() with Streaming
```python
import os 
from litellm import completion

# openai configs
os.environ["OPENAI_API_KEY"] = ""

# azure openai configs
os.environ["AZURE_API_KEY"] = ""
os.environ["AZURE_API_BASE"] = "https://openai-gpt-4-test-v-1.openai.azure.com/"
os.environ["AZURE_API_VERSION"] = "2023-05-15"



# openai call
response = completion(
    model = "gpt-3.5-turbo", 
    messages= = [{ "content": "Hello, how are you?","role": "user"}],
    stream=True
)

# azure call
response = completion(
    model = "azure/<your-azure-deployment>",
    messages = [{ "content": "Hello, how are you?","role": "user"}],
    stream=True
)

```

## Completion() with Streaming + Async
```python
import os 
from litellm import acompletion

# openai configs
os.environ["OPENAI_API_KEY"] = ""

# azure openai configs
os.environ["AZURE_API_KEY"] = ""
os.environ["AZURE_API_BASE"] = "https://openai-gpt-4-test-v-1.openai.azure.com/"
os.environ["AZURE_API_VERSION"] = "2023-05-15"



# openai call
response = acompletion(
    model = "gpt-3.5-turbo", 
    messages= = [{ "content": "Hello, how are you?","role": "user"}],
    stream=True
)

# azure call
response = acompletion(
    model = "azure/<your-azure-deployment>",
    messages = [{ "content": "Hello, how are you?","role": "user"}],
    stream=True
)

```

## Calling completion() multi-threaded

```python
import os
import threading
from litellm import completion

# Function to make a completion call
def make_completion(model, messages):
    response = completion(
        model=model,
        messages=messages,
        stream=True
    )

    print(f"Response for {model}: {response}")

# Set your API keys
os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"
os.environ["AZURE_API_KEY"] = "YOUR_AZURE_API_KEY"

# Define the messages for the completions
messages = [{"content": "Hello, how are you?", "role": "user"}]

# Create threads for making the completions
thread1 = threading.Thread(target=make_completion, args=("gpt-3.5-turbo", messages))
thread2 = threading.Thread(target=make_completion, args=("azure/your-azure-deployment", messages))

# Start both threads
thread1.start()
thread2.start()

# Wait for both threads to finish
thread1.join()
thread2.join()

print("Both completions are done.")
```