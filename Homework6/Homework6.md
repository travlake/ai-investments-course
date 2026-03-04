# Homework 6

## **Due 11:59pm on Tuesday 3/10/2026**

Finance 372T/397 "AI Powered Investments"
Professor Travis Johnson
McCombs School of Business, The University of Texas at Austin

## Grading

You are graded on:

- The quality of your written explanations and economic reasoning
- Whether your backtest results are internally consistent and economically sensible
- Your ability to work with a coding agent to implement, debug, and iterate on a strategy

You are *not* graded on whether your custom strategy "works" (generates alpha). You *are* graded on whether you can explain what it does, why you thought it might work, and what the results tell you.

## Deliverable

Submit a single PDF containing your responses to all tasks below. Include any tables, charts, or terminal output that support your answers. Screenshots are fine.

---

## Overview

In this assignment you will use a **CLI coding agent** — Claude Code or OpenAI Codex — to run a stock-selection backtest. You do not need to write any code yourself. Instead, you will give instructions to the agent in plain English, and it will write and run code on your behalf.

By the end, you will have:

1. Set up a professional development environment on your laptop
2. Run a published academic trading strategy (gross profitability) through a backtest
3. Diagnosed a subtle but important data error (look-ahead bias)
4. Designed and tested your own original trading strategy

---

## Task 1: Set Up Your CLI Coding Agent

Install **Claude Code** on your laptop. Claude Code is a command-line tool that gives Claude direct access to your filesystem and terminal, so it can write, edit, and run code for you.

**Installation steps:**

1. Install **Node.js** (version 18 or later) from [nodejs.org](https://nodejs.org)
2. Open a terminal (Terminal on Mac, PowerShell or Terminal on Windows)
3. Run: `npm install -g @anthropic-ai/claude-code`
4. Run: `claude` to launch it for the first time
5. Follow the prompts to authenticate with your Anthropic account

If you don't have an Anthropic account, you can create one at [console.anthropic.com](https://console.anthropic.com). You'll need a **Pro** subscription (\$20/month). Note that there are usage limits that apply per 5 hour session. You will likely be able to complete this assignment in a single session, but don't count on it. **Start early so you can use multiple sessions if necessary.** As a failsafe, you can enable [Extra usage](https://claude.ai/settings/usage), which bills you per-token once you go above your session limit.

> **Alternative:** If you prefer, you may use **OpenAI Codex CLI** instead. The setup and workflow are similar, but we won't provide step-by-step instructions — you're on your own. Everything below assumes Claude Code, but any capable CLI agent will work.

### Task 1 Submission

*None*

---

## Task 2: Download and Unzip the Data

Download [backtest_data.zip - Google Drive](https://drive.google.com/file/d/1d_W39xM2AoD_uUDm7DwPRfm1BUE8dJG4/view?usp=sharing). Create an empty folder for this project somewhere, and move the data zip into it. Then open a terminal in that folder and run `claude` to start your coding agent.

Once open, ask your coding agent to unzip the data. For example, you might type:

> "Unzip the file backtest_data.zip into the current directory"

The zip file contains three data files:

- **`compustat_with_permno.parquet`** — Quarterly accounting data from Compustat (revenue, cost of goods sold, total assets, etc.), already merged with CRSP stock identifiers
- **`crsp_m.dta`** — Monthly stock returns and prices from CRSP
- **`ff5_plus_mom.dta`** — Monthly Fama-French factor returns (market, size, value, momentum)

### Task 2 Response

*None*

---

## Task 3: Clone the Backtest Repository

Ask your coding agent to clone the backtest framework and put everything in your project folder:

> "Clone https://github.com/travlake/teaching-backtest and put the contents directly in this folder (not in a subfolder)"

Then ask Claude to read through the code and explain what it does. Good questions to ask:

- "What does this backtest do, step by step?"
- "What trading strategy is currently implemented?"
- "What data does it need, and how does it avoid look-ahead bias?"
- "What output will it produce when I run it?"

### Task 3 Response

*In your own words, briefly summarize (1 paragraph) what the backtest code does and what strategy it tests*

---

## Task 4: Run the Gross Profitability Backtest

Ask Claude to install the required packages and run the backtest as-is:

> "Install the requirements and run backtest_gp.py"

Work with Claude to adjust the output so that it's formatted nicely to paste into your solution. If the plot or table is difficult to read you will lose points here.

### Task 4 Response

*Description of Gross Profitability results, including a table and figure*

---

## Task 5: Introduce a Look-Ahead Bias Bug

Now we're going to deliberately introduce a common mistake to see how it affects the results. Note that the initial code produced by `Claude Code` during lecture (but not in my testing before class using the same prompt) embedded this exact bias.

The current code filters out stocks with a **lagged** price (last month's price) below $3. This is correct — when forming portfolios at the start of month *t*, you should only use information available at the end of month *t-1*.

Ask Claude to modify the code so that it filters by the **current month's price** instead of the lagged price. In other words, when deciding which stocks go into the month *t* portfolio, it should use the month *t* price instead of the month *t-1* price. This is a look-ahead bias: you're using information from the future to make a decision today.

Run the backtest again with this change.

### Task 5 Response

*Describe the new results, including a table and figure. Compare the results to Task 4. Explain why filtering this way creates a bias and which direction this bias goes.*

---

## Task 6: Revert and Design Your Own Strategy

First, ask Claude to revert the look-ahead bias change from Task 5:

> "Undo the price filter change — go back to using lagged price"

Now comes the creative part. Design your own trading strategy using the accounting variables available in the Compustat data. Ask Claude what variables are available:

> "What accounting and market (returns, volume, price) variables are in the data that I could use to build a trading signal?"

Explain your strategy idea to Claude in plain English, and ask it to implement the signal in the backtest. For example:

> "I want to test whether firms with high asset growth underperform. Compute asset growth as the percentage change in total assets (atq) over the past year. The signal direction should be that *lower* asset growth is better — I want to be long low-asset-growth stocks and short high-asset-growth stocks."

Run the backtest with your new signal.

### Task 6 Response

1. *[What is your strategy? Explain the economic logic — why might this signal predict future stock returns?]*
2. *[What did you tell Claude to implement? Paste the key part of your conversation.]*

---

## Task 7: Interpret Your Backtest Results

Look at the output from your custom strategy backtest.

### Task 7 Response

*Describe your results, including a table and figure. Include in your discussion the following:*

1. *Does the long-short portfolio earn a positive average return? Is the alpha statistically significant (look at the t-statistic)?*
2. *How do the equal-weighted and value-weighted results compare? If they differ, what might that tell you about whether the strategy works better among large or small stocks?*
3. *Look at the cumulative return plot. Is the performance steady over time, or are there periods where the strategy does especially well or poorly?*
4. *Overall, do you think this is a "real" effect that could be exploited in practice, or is it more likely noise? What additional tests or checks would help you decide?*
