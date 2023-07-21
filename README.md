
1. Set API type
`export OPENAI_API_TYPE=azure`

If you want to use the earlier version `2023-03-15-preview`:

`export OPENAI_API_VERSION=2023-03-15-preview`

2. To set the base URL for your Azure OpenAI resource.
You can find this in the Azure portal under your Azure OpenAI resource.

`export OPENAI_API_BASE=https://your-base-url.openai.azure.com`

3. To set the OpenAI model deployment name for your Azure OpenAI resource.

`export OPENAI_API_MODEL_DEPLOYMENT_NAME=gpt-35-turbo-16k`

4. To set the OpenAIEmbeddings model deployment name for your Azure OpenAI resource.

`export OPENAI_API_EMBEDDING_DEPLOYMENT_NAME=text-embedding-ada-002`

</details>

### 1.1 (Optional) Prepare LLM -  Anthropic(Claude 2) API Token
<details><summary>👇click me</summary>

To get your Anthropic API token, follow these steps:

1. Go to the [Anthropic website](https://docs.anthropic.com/claude/docs/getting-started-with-claude) and sign up for an account if you haven't already.
2. Once you're logged in, navigate to the [API keys page](https://console.anthropic.com/account/keys).
3. Generate a new API key by clicking on the "Create Key" button.
4. Copy the API key and store it safely.
5. Add the API key to your environment variable, e.g. `export ANTHROPIC_API_KEY=<your API key>`
</details>

### 2. (Optional) Prepare Speech to Text - Google Cloud API
<details><summary>👇click me</summary>

To get your Google Cloud API credentials.json, follow these steps:

1. Go to the [GCP website](https://cloud.google.com/speech-to-text/docs/before-you-begin) and sign up for an account if you haven't already.
2. Follow the guide to create a project and enable Speech to Text API
3. Put `google_credentials.json` in the root folder of this project. Check [GCP website](https://cloud.google.com/speech-to-text/docs/before-you-begin#set_your_authentication_environment_variable)
4. Change `SPEECH_TO_TEXT_USE` to use `GOOGLE` in your `.env` file
</details>


### 3. Prepare Text to Speech - ElevenLabs API Key
<details><summary>👇click me</summary>
1. Creating an ElevenLabs Account
Visit [ElevenLabs](https://beta.elevenlabs.io/) to create an account. You'll need this to access the text to speech and voice cloning features.

2. In your Profile Setting, you can get an API Key. Save it in a safe place.

3. Set API key in your .env file:
```
ELEVEN_LABS_API_KEY=<api key>
```
</details>

## 💿 Installation via Python
- **Step 1**. Clone the repo
   ```sh
   git clone https://github.com/Shaunwei/RealChar.git && cd RealChar
    ```
- **Step 2**. Install requirements
    - Install [portaudio](https://people.csail.mit.edu/hubert/pyaudio/) and [ffmpeg](https://ffmpeg.org/download.html) for audio
    ```sh
    # for mac
    brew install portaudio
    brew install ffmpeg
    ```
    ```sh
    # for ubuntu
    sudo apt update
    sudo apt install portaudio19-dev
    sudo apt install ffmpeg
    ```
    - Then install all python requirements
    ```sh
    pip install -r requirements.txt
    ```
- **Step 3**. Create an empty [sqlite](https://www.sqlite.org/index.html) database if you have not done so before
    ```sh
    sqlite3 test.db "VACUUM;"
    ```
- **Step 4**. Run db upgrade
    ```sh
    alembic upgrade head
    ```
- **Step 5**. Setup `.env`: update API keys and select module
   ```sh
   cp .env.example .env
   ```
- **Step 6**. Run server with `cli.py` or use uvicorn directly
    ```sh
    python cli.py run-uvicorn
    # or
    uvicorn realtime_ai_character.main:app
    ```
- **Step 7**. Run client:
    - Use **GPT4** for better conversation and **Wear headphone** for best audio(avoid echo)
    - There are two ways to access the web client:
        - **Option 1**: Open your web browser and navigate to http://localhost:8000 (NOT 0.0.0.0:8000)
        - **Option 2**: Running the client in React.
            ```sh
            cd client/web
            npm start
            ```
            After running these commands, a local development server will start, and your default web browser will open a new tab/window pointing to this server (usually http://localhost:3000).
    - (Optional) Terminal client: Run the following command in your terminal
    ```sh
    python client/cli.py
    ```
    - (Optional) mobile client: open `client/mobile/ios/rac/rac.xcodeproj/project.pbxproj` in Xcode and run the app
- **Step 8**. Select one character to talk to, then start talking


## (Optional) 📀 Installation via Docker
<details><summary>👇click me</summary>

1. Docker image: you can use our docker image directly
    ```sh
    docker pull shaunly/real_char:latest
    ```
    (Or you want build yourself) Build docker image
    ```sh
    python cli.py docker-build
    ```
    If you have issues with docker (especially on a non-Linux machine), please refer to https://docs.docker.com/get-docker/ (installation) and https://docs.docker.com/desktop/troubleshoot/overview/ (troubleshooting).
2. Run docker image with `.env` file
    ```sh
    python cli.py docker-run
    ```

3. Go to http://localhost:8000 (NOT 0.0.0.0:8000) to start talking or use terminal    client
    ```sh
    python client/cli.py
    ```

</details>

<br/>

## 🆕! LangSmith integration
<details><summary>👇click me</summary>

If you have access to LangSmith, you can edit these environment variables to enable:
```
LANGCHAIN_TRACING_V2=false # default off
LANGCHAIN_ENDPOINT=https://api.smith.langchain.com
LANGCHAIN_API_KEY=YOUR_LANGCHAIN_API_KEY
LANGCHAIN_PROJECT=YOUR_LANGCHAIN_PROJECT
```
And it should work out of the box.

</details>

<br/>

## ⭐️ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Shaunwei/RealChar&type=Date)](https://star-history.com/#Shaunwei/RealChar&Date)

## 📍 Roadmap
- [x] Launch v0.0.1 and build a community
- [x] Move away from Vanilla JS
- [x] Launch mobile app (iOS TestFlight Beta link: https://testflight.apple.com/join/JA6p9sZQ)
- [ ] Add authentication for customization
- [ ] Allow selecting different LLM
- [ ] Add ability to add community characters

## 🫶 Contribute to RealChar
Please check out our [Contribution Guide](contribute.md)!

## 🎲 Community
- Join us on [Discord](https://discord.gg/e4AYNnFg2F)
