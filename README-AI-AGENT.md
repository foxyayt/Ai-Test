# Property AI Assistant - Setup Guide

This AI Agent is a self-contained widget designed to live on every page of your website. It uses the Open Router API with the `stepfun/step-3.5-flash:free` model.

## 1. How to Use on Your Pages

To add the AI agent to any page, simply add this line of code just before the closing `</body>` tag:

```html
<iframe src="ai-agent.html" style="position: fixed; bottom: 0; right: 0; width: 400px; height: 650px; border: none; z-index: 10000; pointer-events: none;" id="ai-agent-iframe"></iframe>

<script>
    // This allows clicking through the iframe to the button underneath
    window.addEventListener('message', function(e) {
        const iframe = document.getElementById('ai-agent-iframe');
        if (e.data === 'expand') {
            iframe.style.pointerEvents = 'auto';
        } else if (e.data === 'collapse') {
            iframe.style.pointerEvents = 'none';
        }
    });
</script>
```

> [!NOTE]
> Since the widget is in an `iframe`, you may need to add a small script inside `ai-agent.html` to send the `expand/collapse` messages to the parent page (already partially handled in the design).

## 2. Setting Up the API Key (GitHub Secrets)

Since this site is hosted on GitHub Pages, we use GitHub Actions to securely inject your API key.

1.  **Get an API Key**: Go to [Open Router](https://openrouter.ai/) and create an API key.
2.  **Add Secret to GitHub**:
    - Go to your GitHub repository.
    - Click **Settings** > **Secrets and variables** > **Actions**.
    - Click **New repository secret**.
    - Name: `OPENROUTER_API_KEY`
    - Value: Paste your API key here.
3.  **Deploy**: 
    - When you push your code to the `main` branch, the GitHub Action in `.github/workflows/deploy.yml` will automatically replace the placeholder in `ai-agent.html` and deploy it to GitHub Pages.

## 3. Customizing the AI

- **Change Knowledge/Personality**: Open `ai-agent.html` and find the `SYSTEM_PROMPT` constant. You can update the property trends, tone of voice, and instructions there.
- **Change Model**: Find the `MODEL_ID` constant (default is `stepfun/step-3.5-flash:free`).
- **Change Design**: All styles are in the `<style>` block at the top of `ai-agent.html`. Look for the `:root` section to change colors and gradients.

## 4. Local Testing

Since the API key is injected during deployment, the widget **will not work** locally until you manually replace `__OPENROUTER_API_KEY__` with your real key in your local `ai-agent.html`.

> [!WARNING]
> DO NOT commit your real API key to GitHub. Always use the `__OPENROUTER_API_KEY__` placeholder in your repository.
