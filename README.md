# MyClawDex: Local AI Development Environment with Ollama

This open-source project provides instructions for setting up a local AI development environment using `ollama` for model hosting and VS Code for development. This allows you to leverage powerful AI models locally, ensuring privacy, speed, and cost-effectiveness.

## Project Goal

The primary goal of MyClawDex is to empower developers to:
1.  **Run AI models locally:** Utilize `ollama` to host models directly on your machine.
2.  **Integrate with VS Code:** Seamlessly interact with your local AI models from within your preferred IDE.
3.  **Develop AI-powered applications:** Build and test applications that leverage local AI without relying on external APIs.

## Getting Started

Follow these steps to set up your local AI development environment.

### Prerequisites

*   **Ollama:** Follow the official Ollama installation guide for your operating system: [https://ollama.com/download](https://ollama.com/download).
    *   **For macOS/Linux:** You can typically use:
        ```bash
        curl -fsSL https://ollama.com/install.sh | sh
        ```
    *   **For Windows:** Download and run the installer from the Ollama website.
*   **VS Code:** Download and install Visual Studio Code.
*   **Python:** Python 3.8+ is recommended.

### Step 1: Configure Ollama

1.  **Verify Ollama Installation:** After installation, verify it's working:
    ```bash
    ollama --version
    ```
2.  **Download a Local Model:** Use Ollama to download a compatible model. For this example, we'll use a local large language model (LLM). You can explore available models with `ollama list`.
    ```bash
    # Example: Downloading a Llama 3.1 model
    ollama pull llama3.1
    ```
    Confirm the model is installed:
    ```bash
    ollama list
    ```
3.  **Start Ollama Server:** Ollama runs as a background server. Ensure it's running before interacting with models. You can often start it by just running `ollama serve` in a terminal or ensuring the Ollama application is running in your system tray.

### Optional: Ollama Web UI Installation

For a graphical interface to interact with your local Ollama models, you can install the Ollama Web UI. This is a separate project and provides a chat-like interface.

1.  **Install Node.js (if not already installed):** The Ollama Web UI requires Node.js. Refer to the official Node.js website for installation instructions.
2.  **Clone the Ollama Web UI Repository:**
    ```bash
    git clone https://github.com/ollama-webui/ollama-webui.git
    cd ollama-webui
    ```
3.  **Install Dependencies and Build:**
    ```bash
    npm install
    # If you encounter ERESOLVE errors, try:
    # npm install --legacy-peer-deps
    # npm install --force
    npm run build
    ```
4.  **Run the Web UI (using the backend script):**
    After building the frontend, the Open WebUI (formerly Ollama Web UI) typically runs by starting its backend server. It's important to run this script with `bash` as some shell features (`${VAR,,}`) might not be compatible with `sh`.

    **First, ensure Python dependencies for the backend are installed in a virtual environment:**
    ```bash
    # Navigate to the backend directory within the cloned repository
    cd ollama-webui/backend
    python3 -m venv .venv_webui
    source .venv_webui/bin/activate # On Windows: .venv_webui\Scripts\activate
    pip install "uvicorn[standard]" typer "python-multipart" "typing_extensions" "pydantic" "opentelemetry-api" "opentelemetry-sdk"
    ```
    **Then, navigate back and run the start script:**
    ```bash
    # Navigate back to the main directory of the cloned repository
    cd ..

    # Run the backend script using bash
    bash ./backend/start.sh
    ```
    The Web UI will typically be accessible in your browser at `http://localhost:8080` (or another port if specified). Ensure your Ollama server (`ollama serve`) is running in the background.

    **Note:** If `start.sh` is not found, fails, or you encounter "bad substitution" errors, please check the official [Open WebUI GitHub repository](https://github.com/open-webui/open-webui) for the most current instructions and potential updates to the `start.sh` script or its required execution environment.

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
    # On macOS/Linux:
    source .venv/bin/activate
    # On Windows:
    .venv\Scripts\activate
    ```

3.  **Install Required Libraries:** You'll need the `ollama` Python library to interact with your local Ollama server.
    ```bash
    pip install ollama
    ```

### Step 3: Interact with Your Local Model from VS Code

Here's an example Python script (`app.py`) demonstrating how to interact with your local Ollama model.

#### Example using `ollama` Python library:

Create `app.py`:
```python
import ollama

def get_local_llm_response(prompt: str, model_name: str = "llama3.1"):
    """
    Interacts with a local Ollama model.
    """
    try:
        response = ollama.chat(model=model_name, messages=[{'role': 'user', 'content': prompt}])
        return response['message']['content']
    except Exception as e:
        return f"Error interacting with local Ollama model: {e}"

if __name__ == "__main":
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
