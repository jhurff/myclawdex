# MyClawDex: Local AI Development Environment

This open-source project provides instructions for setting up a local AI development environment using `exo` for model hosting and VS Code for development. This allows you to leverage powerful AI models locally, ensuring privacy, speed, and cost-effectiveness.

## Project Goal

The primary goal of MyClawDex is to empower developers to:
1.  **Run AI models locally:** Utilize `exo` to host models directly on your machine.
2.  **Integrate with VS Code:** Seamlessly interact with your local AI models from within your preferred IDE.
3.  **Develop AI-powered applications:** Build and test applications that leverage local AI without relying on external APIs.

## Getting Started

Follow these steps to set up your local AI development environment.

### Prerequisites

*   **Exo CLI:** Ensure you have the Exo CLI installed. If not, follow the official Exo installation guide.
    ```bash
    # Example (check official docs for latest)
    curl -sfL https://exo.dev/install | sh
    ```
*   **VS Code:** Download and install Visual Studio Code.
*   **Python:** Python 3.8+ is recommended.

### Step 1: Install and Configure Exo

1.  **Install Exo:** If you haven't already, install the Exo CLI.
    ```bash
    # Verify installation
    exo --version
    ```
2.  **Start Exo Gateway:** The Exo Gateway manages your local models.
    ```bash
    exo gateway start
    ```
    Verify it's running:
    ```bash
    exo gateway status
    ```
3.  **Download a Local Model:** Use Exo to download a compatible model. For this example, we'll use a local large language model (LLM). You can explore available models with `exo models list`.
    ```bash
    # Example: Downloading a Llama 3.1 model
    exo model install ollama/llama3.1:latest
    ```
    Confirm the model is installed:
    ```bash
    exo model list
    ```

### Step 2: Set Up Your VS Code Environment

1.  **Install VS Code Extensions:**
    *   **Python Extension:** Essential for Python development.
    *   **Remote - SSH (Optional):** If you're developing on a remote machine.
    *   **OpenClaw Extension (if available/desired):** For direct integration with OpenClaw's capabilities, including local model interactions.

2.  **Create a Python Virtual Environment:**
    ```bash
    mkdir my-ai-project
    cd my-ai-project
    python -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    ```

3.  **Install Required Libraries:** You'll need a library to interact with the local Exo model. This often involves a client library or making direct HTTP requests to the Exo Gateway's local API.

    *   **Option A: Using the `ollama` Python library (if using an Ollama model via Exo):**
        ```bash
        pip install ollama
        ```
    *   **Option B: Direct HTTP requests (more general):**
        ```bash
        pip install requests
        ```

### Step 3: Interact with Your Local Model from VS Code

Here's an example Python script (`app.py`) demonstrating how to interact with your local model.

#### Example using `ollama` Python library:

Create `app.py`:
```python
import ollama

def get_local_llm_response(prompt: str, model_name: str = "llama3.1"):
    """
    Interacts with a local Ollama model hosted via Exo.
    """
    try:
        response = ollama.chat(model=model_name, messages=[{'role': 'user', 'content': prompt}])
        return response['message']['content']
    except Exception as e:
        return f"Error interacting with local model: {e}"

if __name__ == "__main__":
    user_prompt = "Explain the concept of quantum entanglement in simple terms."
    print(f"Prompt: {user_prompt}
")
    response = get_local_llm_response(user_prompt)
    print(f"Local LLM Response:
{response}")

    user_prompt_2 = "Write a short, creative story about a curious squirrel."
    print(f"
Prompt: {user_prompt_2}
")
    response_2 = get_local_llm_response(user_prompt_2)
    print(f"Local LLM Response:
{response_2}")
```

#### Example using `requests` (for generic Exo API interaction):

The Exo Gateway exposes a local API, typically on `http://localhost:18789` or similar. You'd need to consult Exo's documentation for the exact API endpoint for your model. Assuming a common `/chat/completions` like endpoint for an OpenAI-compatible interface:

Create `app.py`:
```python
import requests
import json

EXO_GATEWAY_URL = "http://localhost:18789/v1/chat/completions" # Consult Exo docs for exact endpoint

def get_exo_llm_response(prompt: str, model_id: str = "ollama/llama3.1:latest"):
    """
    Interacts with a local model exposed via Exo Gateway.
    """
    headers = {
        "Content-Type": "application/json",
    }
    payload = {
        "model": model_id,
        "messages": [
            {"role": "user", "content": prompt}
        ],
        "temperature": 0.7
    }
    try:
        response = requests.post(EXO_GATEWAY_URL, headers=headers, data=json.dumps(payload))
        response.raise_for_status() # Raise an exception for HTTP errors
        return response.json()['choices'][0]['message']['content']
    except requests.exceptions.RequestException as e:
        return f"Error interacting with Exo Gateway: {e}"
    except KeyError:
        return f"Unexpected response format from Exo Gateway: {response.json()}"

if __name__ == "__main__":
    user_prompt = "Describe the lifecycle of a butterfly."
    print(f"Prompt: {user_prompt}
")
    response = get_exo_llm_response(user_prompt)
    print(f"Local LLM Response:
{response}")
```

### Step 4: Run Your Application

1.  **Save** your `app.py` file in your `my-ai-project` directory.
2.  **Open your terminal** (or VS Code's integrated terminal) and navigate to `my-ai-project`.
3.  **Activate your virtual environment** (if not already active).
    ```bash
    source .venv/bin/activate
    ```
4.  **Run the Python script:**
    ```bash
    python app.py
    ```

You should see output from your local AI model!

## Contributing

We welcome contributions to MyClawDex! Feel free to:
*   Add instructions for other local models or configurations.
*   Improve existing guides.
*   Suggest new features or integrations.

Please open an issue or submit a pull request on GitHub.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
