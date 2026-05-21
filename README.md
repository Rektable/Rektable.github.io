<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Email verification</title>
    <style>
      :root {
        --bg: #0b1020;
        --card: #121a33;
        --text: #e5e7eb;
        --muted: #9ca3af;
        --accent: #60a5fa;
      }
      body {
        margin: 0;
        font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica,
          Arial, "Apple Color Emoji", "Segoe UI Emoji";
        background: var(--bg);
        color: var(--text);
      }
      .wrap {
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 24px;
      }
      .card {
        width: 100%;
        max-width: 720px;
        background: rgba(18, 26, 51, 0.92);
        border: 1px solid rgba(96, 165, 250, 0.25);
        border-radius: 14px;
        padding: 22px;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
      }
      h1 {
        margin: 0 0 10px;
        font-size: 22px;
      }
      p {
        margin: 8px 0;
        color: var(--muted);
        line-height: 1.5;
      }
      .row {
        margin-top: 16px;
        padding: 14px;
        border-radius: 12px;
        background: rgba(96, 165, 250, 0.08);
        border: 1px solid rgba(96, 165, 250, 0.18);
        overflow-wrap: anywhere;
      }
      .btn {
        display: inline-block;
        margin-top: 14px;
        padding: 10px 14px;
        border-radius: 10px;
        background: var(--accent);
        color: #071024;
        font-weight: 700;
        text-decoration: none;
      }
      code {
        color: #c7d2fe;
      }
    </style>
  </head>
  <body>
    <div class="wrap">
      <div class="card">
        <h1>✅ Email verification processed</h1>
        <p>
          If Supabase was able to verify your account, you can now sign in in the Telmos Game Launcher.
        </p>

        <div class="row" id="params"></div>

        <a class="btn" href="/">Go to website</a>
        <p>
          Note: Desktop apps cannot be reliably “opened” directly from an email link.
          After verification, open the launcher and log in.
        </p>
      </div>
    </div>

    <script>
      (function () {
        const params = new URLSearchParams(window.location.search);
        const token = params.get('token');
        const type = params.get('type');
        const redirectTo = params.get('redirect_to');

        const pretty = [
          ['type', type],
          ['redirect_to', redirectTo],
          ['token_present', token ? 'yes' : 'no'],
        ]
          .filter(([, v]) => v !== null)
          .map(([k, v]) => `${k}: ${v}`)
          .join('<br/>');

        document.getElementById('params').innerHTML = `
          <div style="font-weight:700; margin-bottom:8px; color: var(--text);">Query parameters</div>
          <div style="font-size: 13px;">${pretty}</div>
        `;
      })();
    </script>
  </body>
</html>

