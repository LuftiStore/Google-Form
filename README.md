# LufzAI Form Assistant

A study-focused Android WebView app and Python backend. It accepts a public Google Forms responder URL, attempts to extract the currently embedded public form payload, and asks an OpenAI model to explain the questions. It does not submit answers.

## Important limitations
- Google does not provide a stable public unauthenticated API for reading arbitrary Google Forms. The reader in this starter relies on the page's embedded `FB_PUBLIC_LOAD_DATA_` data and may break if Google changes its page format.
- Sign-in-required, restricted, closed, CAPTCHA-protected, or unsupported forms may not be readable.
- AI-generated answers can be incorrect. Use this as a study aid and verify the explanations.
- Never put your OpenAI API key in the APK or GitHub repository.

## Deploy the backend
1. Push this folder to a GitHub repository.
2. Create a Python web service on Render using this repository and root directory `backend`.
3. Build command: `pip install -r requirements.txt`
4. Start command: `uvicorn app:app --host 0.0.0.0 --port $PORT`
5. Add environment variables in the hosting dashboard:
   - `OPENAI_API_KEY`: your OpenAI API key
   - `OPENAI_MODEL`: `gpt-4.1-mini` (or a model available to your account)
   - `APP_TOKEN`: a long random token used by your app
6. Copy the deployed HTTPS URL.

`render.yaml` is included as a deployment starting point. Keep secrets in the hosting dashboard only.

## Build the APK with GitHub Actions
1. Add repository variable `BACKEND_URL` containing the deployed HTTPS URL (no trailing slash).
2. Open GitHub Actions and run **Build Android APK**.
3. Download the `LufzAI-debug-apk` artifact.

## Configure the app
Open the APK, enter the backend HTTPS URL and the `APP_TOKEN`, save settings, paste a public Google Forms responder link, then tap **Analisis untuk belajar**.

## Security checklist
- If an API key was ever shared in a chat, screenshot, or repository, revoke it and create a new one.
- Do not commit `.env`, API keys, or `APP_TOKEN`.
- This starter has a shared app token, not user accounts. For a public release, add authentication, rate limits, abuse protection, and usage quotas.
