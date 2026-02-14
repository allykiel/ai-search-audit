# AI Search Audit Tool — Ally Kiel

Two versions of your AI search visibility audit tool for premium F&B brands.

---

## 📁 What's Included

### 1. `consultant-mode.html` — For Your Personal Use
A single HTML file you open in your browser. Run audits during discovery calls via screen-share.

**Setup (2 minutes):**
1. Get your API key at [console.anthropic.com](https://console.anthropic.com)
   - Create an account (or sign in)
   - Go to **API Keys** → **Create Key**
   - Copy the key (starts with `sk-ant-...`)
2. Open `consultant-mode.html` in Chrome/Edge/Firefox
3. Paste your API key when prompted
4. That's it — start auditing brands

**Cost:** Each audit runs 5 API calls with web search. Roughly **$0.15–0.30 per audit** depending on response length.

**Your key is stored in your browser's localStorage** — it never leaves your machine except to authenticate with Anthropic's API directly.

---

### 2. `ai-audit-leadgen/` — For Lead Generation (Public-Facing)
A Vercel-deployable app where prospects audit their own brand. Includes email capture gate before showing results.

**Setup (10 minutes):**

1. **Install Vercel CLI** (if you don't have it):
   ```bash
   npm install -g vercel
   ```

2. **Set your API key as an environment variable:**
   ```bash
   cd ai-audit-leadgen
   vercel env add ANTHROPIC_API_KEY
   ```
   Paste your API key when prompted. Select all environments (Production, Preview, Development).

3. **Deploy:**
   ```bash
   vercel --prod
   ```
   Vercel will give you a URL like `ai-audit-leadgen.vercel.app`.

4. **Custom domain (optional):**
   - In your Vercel dashboard → Project Settings → Domains
   - Add something like `audit.allykiel.com`
   - Update your DNS as instructed

**How lead capture works:**
- Prospects enter their brand, category, and first name
- The audit runs (they see live progress)
- Results are gated behind an email capture
- They see their overall score (teaser) but must enter email for the full report
- Leads are logged to the browser console — see the comment in the code for where to add your email service (Mailchimp, ConvertKit, etc.)

**To connect email capture to your CRM/email tool:**
Look for the `unlockReport()` function in `public/index.html`. There's a commented-out fetch call where you can POST lead data to your email service's API.

---

## 💡 How to Use in Discovery Calls

1. Open the consultant version before the call
2. When you're talking to a prospect, say: *"Let me show you something — I'm going to run a live AI search audit on your brand right now"*
3. Enter their brand and category
4. Screen-share as it runs through the 5 dimensions
5. Walk them through the results together
6. The report ends with a CTA to book a strategy session

**Pro tip:** Run the audit on their brand BEFORE the call so you know what to expect. Then run it live during the call for the "wow" moment.

---

## 🔧 Customization

**To change categories:** Edit the `CATEGORIES` array in either HTML file.

**To change your CTA link:** Search for `allykiel.carrd.co` and replace with your actual booking link.

**To adjust scoring:** The `calcScore()` function in each file controls how scores are calculated. You can tune the weights to match your consulting methodology.

**To add/modify audit dimensions:** Edit the `QUERIES` array. Each query has an id, label, description, and prompt template. You can add new dimensions or modify existing prompts.

---

## 📊 What It Audits

| Dimension | What It Measures |
|-----------|-----------------|
| Brand Discovery | Can AI find the brand at all? How prominent is it? |
| Category Authority | Is the brand recommended when consumers ask for "best in category"? |
| Reputation & Reviews | What does AI surface about quality, press, awards? |
| Competitive Landscape | How is the brand positioned vs. competitors? |
| Purchase Intent | Does AI recommend the brand when someone's ready to buy? |

Each dimension is scored 0–100, averaged into an overall score, and assigned a letter grade (A–F).
