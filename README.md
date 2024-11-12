# Computing Adversarial Robustness and Prompt Leakage Risk using IBM watsonx.governance

## Learning goals

This notebook shows how a prompt engineer creates and tests a prompt template for a chatbot on an insurance website. 

The goal is to evaluate the prompt template's propensity to be susceptible to jailbreak, prompt injection, and system prompt leakage attacks.

> **Jailbreak**: Attacks that try to bypass the safety filters of the language model.
> 
> **Prompt injection**: Attacks that trick the system by combining harmful user input with the trusted prompt created by the developer.
> 
> **System prompt leakage**: Attacks that try to leak the system prompt or the prompt template.

The prompt engineer uses watsonx.governance to calculate the below metrics.

**`Adversarial robustness`**: This metric checks how well the prompt template can resist jailbreak and prompt injection attacks. 

  - ***Metric Range***: 0 to 1
    - A value closer to 0 means the prompt template is weak and can be easily attacked.
    - A value closer to 1 means the prompt template is strong and resistant to attacks.

      As part of the metric result, guidance is provided on what kinds of attacks are successful against the prompt template asset so the prompt engineer can either tweak the prompt, or follow other mitigation guidelines provided, to stengthen the prompt template asset against the adversarial robustness attacks.

**`Prompt leakage risk`**: This metric measures the susceptibility of the prompt template asset to system prompt leakage attacks.
    
  - ***Metric Range***: 1 to 0
    - A value closer to 1 means the prompt template can be easily leaked.
    - A value closer to 0 means it is relatively difficult for an attacker to get the prompt template leaked.
    
      The metric result shows the top 'n' attack vectors which are able to leak the prompt template.
      
## Prerequisites

You will need to provide the following variables in order to be able to run this notebook:

- **CLOUD_API_KEY**: An IBM Cloud API key with access to a watsonx.gov service instance. If you don't have an API key handy, you can create one by accessing [IBM Cloud API Keys](https://cloud.ibm.com/iam/apikeys) and clicking on the `Create` button

- **api_endpoint**: The URL used for inferencing a watsonx.ai model. For example, `https://us-south.ml.cloud.ibm.com/ml/v1/text/generation?version=2023-05-29`

- **project_id**: The project ID in Watson Studio. ***Hint***: You can find the `project_id` as follows: Open the prompt lab in watsonx.ai. At the very top of the UI, there will be a `"Projects / *project name* /"` breadcrumb trail. Click on the `"*project name*"` link, then get the `project_id` from the project's `"Manage"` tab (`"Project -> Manage -> General -> Details"`).
      
      
