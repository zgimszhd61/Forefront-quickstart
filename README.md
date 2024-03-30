Here is a quickstart guide for using Forefront AI, with complete code examples:

## Installation

First, install the Forefront Python SDK:

```python
pip install forefront
```

## Authentication

Import the Forefront client and instantiate it with your API key:

```python
from forefront import ForefrontClient

client = ForefrontClient(api_key='YOUR_API_KEY') # Replace with your actual API key
```

## Fine-tuning a Model

To fine-tune a model, you'll need a dataset of examples in JSONL format, with "prompt" and "completion" fields. Let's download an example dataset:

```python
import requests

dataset_url = "https://example.com/open-hermes-2.5.jsonl"
dataset = requests.get(dataset_url).content

with open("dataset.jsonl", "wb") as f:
    f.write(dataset)
```

Now we can fine-tune the Mistral-7B model on this dataset:

```python
fine_tune_response = client.fine_tunes.create(
    model="mistral-7b",
    dataset="dataset.jsonl",
    n_epochs=4,
    batch_size=8
)

print(fine_tune_response)
```

This will start the fine-tuning process, which may take some time depending on the dataset size. You can check the status by:

```python
status = client.fine_tunes.status(fine_tune_response.id)
print(status)
```

## Inference

Once fine-tuning is complete, you can use the fine-tuned model for inference:

```python
response = client.completions.create(
    model=fine_tune_response.fine_tuned_model,
    prompt="Write a short poem about spring:"
)

print(response.text)
```

This will generate a poem using your fine-tuned model! You can use the same `client.completions.create()` method to generate text for any task by varying the prompt.

## Example Use Cases

Here are some example use cases you could explore with Forefront:

- Fine-tune a model on your product documentation to build a query assistant
- Train a model on software code to assist with code generation/explanation
- Create a creative writing assistant by fine-tuning on novels/stories
- Build a chatbot by fine-tuning on conversational data

The key is to provide relevant examples in your fine-tuning dataset for the specific task you want the model to perform. Refer to the Forefront documentation for more details on advanced features like exporting models, using datasets, etc. [1][2][3][4][9][10]

Citations:
[1] https://help.forefrontcrm.com/knowledge-base/quick-start-guide/quick-start-guide/
[2] https://help.forefrontcrm.com/knowledge-base/quick-start-guide/setting-up-your-account/
[3] https://www.youtube.com/watch?v=Zi6S_cQYfhA&t=0
[4] https://docs.forefront.ai/api-reference/authentication
[5] https://forefront.education/support/teacher-overview-video/
[6] https://forefront.education/training/getting-started/
[7] https://docs.smrtphone.io/en/articles/7733864-using-forefront-crm-s-api-key
[8] https://help.forefrontcrm.com/knowledge-base/settings/integration/integration-with-smrtphone/
[9] https://docs.forefront.ai/get-started/quickstart
[10] https://docs.forefront.ai
[11] https://www.youtube.com/watch?v=M25YxUmA8Gs
[12] https://www.youtube.com/watch?v=iecvUIXazn0
[13] https://forefront.education/project-view/getting-started-in-forefront/
[14] https://myforefront.org/programs-services/webinar-library/quickstart-proposal-writing/
[15] https://www.youtube.com/watch?v=0xdcvgT6rkc
[16] https://manage.opti-tune.com/help/site/articles/using/applications/examples/forefront.html
[17] https://www.quickstart.com/programming-language/is-coding-is-right-for-me/
