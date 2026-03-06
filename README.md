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
    pip install fastapi==0.128.5 uvicorn[standard]==0.40.0 pydantic==2.12.5 python-multipart==0.0.22 itsdangerous==2.2.0 python-socketio==5.16.1 python-jose==3.5.0 cryptography bcrypt==5.0.0 argon2-cffi==25.1.0 "PyJWT[crypto]"==2.11.0 authlib==1.6.7 requests==2.32.5 aiohttp==3.13.2 async-timeout aiocache aiofiles starlette-compress==1.7.0 Brotli==1.1.0 "httpx[socks,http2,zstd,cli,brotli]"==0.28.1 "starsessions[redis]"==2.2.1 python-mimeparse==2.0.0 sqlalchemy==2.0.46 alembic==1.18.3 peewee==3.19.0 peewee-migrate==1.14.3 pycrdt==0.12.46 redis APScheduler==3.11.2 RestrictedPython==8.1 pytz==2025.2 loguru==0.7.3 asgiref==3.11.1 tiktoken mcp==1.26.0 openai anthropic google-genai==1.62.0 langchain==1.2.9 langchain-community==0.4.1 langchain-classic==1.0.1 langchain-text-splitters==1.1.0 fake-useragent==2.2.0 chromadb==1.4.1 weaviate-client==4.19.2 opensearch-py==3.1.0 transformers==5.1.0 sentence-transformers==5.2.2 accelerate pyarrow==20.0.0 einops==0.8.2 ffty==6.3.1 chardet==5.2.0 pypdf==6.7.0 fpdf2==2.8.5 pymdown-extensions==10.20.1 docx2txt==0.9 python-pptx==1.0.2 unstructured==0.18.31 msoffcrypto-tool==6.0.0 nltk==3.9.2 Markdown==3.10.1 pypandoc==1.16.2 pandas==3.0.0 openpyxl==3.1.5 pyxlsb==1.0.10 xlrd==2.0.2 validators==0.35.0 psutil sentencepiece soundfile==0.13.1 pillow==12.1.0 opencv-python-headless==4.13.0.92 rapidocr-onnxruntime==1.4.4 rank-bm25==0.2.2 onnxruntime==1.24.1 faster-whisper==1.2.1 black==26.1.0 youtube-transcript-api==1.2.4 pytube==15.0.0 pydub ddgs==9.10.0 azure-ai-documentintelligence==1.0.2 azure-identity==1.25.1 azure-storage-blob==12.28.0 azure-search-documents==11.6.0 google-api-python-client google-auth-httplib2 google-auth-oauthlib googleapis-common-protos==1.72.0 google-cloud-storage==3.9.0 pymongo psycopg2-binary==2.9.11 pgvector==0.4.2 PyMySQL==1.1.2 boto3==1.42.44 pymilvus==2.6.8 qdrant-client==1.16.2 playwright==1.58.0 elasticsearch==9.3.0 pinecone==6.0.2 oracledb==3.4.2 av==14.0.1 colbert-ai==0.2.22 docker~=7.1.0 pytest~=8.4.1 pytest-docker~=3.2.5 ldap3==2.9.1 firecrawl-py==4.14.0 opentelemetry-api==1.39.1 opentelemetry-sdk==1.39.1 opentelemetry-exporter-otlp==1.39.1 opentelemetry-instrumentation==0.60b1 opentelemetry-instrumentation-fastapi==0.60b1 opentelemetry-instrumentation-sqlalchemy==0.60b1 opentelemetry-instrumentation-redis==0.60b1 opentelemetry-instrumentation-requests==0.60b1 opentelemetry-instrumentation-logging==0.60b1 opentelemetry-instrumentation-httpx==0.60b1 opentelemetry-instrumentation-aiohttp-client==0.60b1
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
