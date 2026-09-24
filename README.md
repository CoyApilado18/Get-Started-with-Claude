## 30 Second Summary

Claude Code is an AI assistant that lives in your terminal. You type plain English, and it executes real tasks on your computer. No coding experience required.

In this project, we will install Claude Code, learn its safety modes and prompting patterns, and use it to organize real files on my computer. By the end, we'll have a working setup of Claude Code, a personalized preferences file, and reusable commands you can run anytime.

## What We'll Build
We'll go from never having opened a terminal to confidently using Claude Code as our personal AI assistant for file management, organization, and automation.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/eff06a5aaeadd2d08fabd6f0ba7f88a21bae9ce5/Images/Architecture_Claude_Code_managing_files.png)

## By the end of this project, you'll have:
- A working `Claude Code installation`, fully authenticated and ready to use.
- A personalized `CLAUDE.md preferences file` and a reorganized folder as proof that Claude Code works for you.
- A mental model of how to `prompt Claude Code effectively` for any task, with a library of reusable prompt patterns and use cases to explore next.
- `Secret Mission`: Build a multi-step "digital audit" command that analyzes storage, finds duplicates, identifies forgotten files, and produces a readable report.

## Are there any prerequisites?
None. This project assumes zero coding or terminal experience. You will need a Claude Pro subscription ($28/month) though, and the project walks you through signing up if you don't already have one.


## Step 1. Get Access to Claud Code
In this step, we'll:
- Get a Claude subscription (Pro or higher).
- Install Claude Code.
- Launch Claude Code and authenticate.

### Get a Claude subscription 
Claude Code requires a paid Claude plan. It is included with Pro, Max, Team, and Enterprise subscriptions.
- Open your browser and go to claude.ai/upgrade.
- Choose the Pro plan at $28/month. This includes full access to Claude Code.
- Complete the payment process and confirm your account is active.

### Why Pro?
The Pro plan ($20/month) gives you plenty of usage for the file management tasks in this project. Max plans ($100/month or $200/month) offer more usage but are unnecessary for getting started.

### Install Claude Code
- Open a terminal, press `Cmd+Space` (macOS) then type `terminal`or the `Windows` key (Windows) to open your search bar or since I'm using Ubuntu `ctrl+Alt+t`. In my case, I just used my VScode terminal to install Claude. 
- Follow this link for the commands to install Claude Code [Native Install](https://code.claude.com/docs/en/overview#terminal) either from MacOS, Linux or Windows.
- Double check that Claude Code is all set up and ready to go by running the command below and you should see the Claude Code version as the output.
```bash
claude --version
```

### Launch and authenticate
Now that Claude Code is installed, you need to launch it and log in with your Claude account. 

- In your terminal, type `claude` and press Enter.  
You have launched Claude Code before, so it skips the login and first-time setup screens. Continue to the `Trust the folder and complete setup` substep below. This is your very first time launching Claude Code, follow along for the next steps.

### Choose a theme
The first prompt asks which colour theme to display in your terminal.
- Use the arrow keys to highlight Dark mode (or whichever you prefer) and press Enter. You can change this later with the /theme command.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/Theme-Output.png)

### Login to Claude Code
Claude Code shows a welcome screen and asks you to select a login method.
- Select option 1: Claude account with subscription and press `Enter`.
- Your browser opens automatically for you to log in. If it does not open, copy the URL shown in the terminal and paste it into your browser.
- Log in with the same Claude account you used for your subscription.
- Once authenticated, return to your terminal and you'll see a "Login Successful" message.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/terminal_login_successfull.png)

### Trust the folder and complete setup
After authenticating, Claude Code asks whether you trust the folder it is running in. This prompt appears every time you open Claude Code in a new folder, not just the first time.
- Use the arrow keys to highlight `Yes, I trust this folder` and press `Enter`.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/trust-folder-message.png)

## Why does Claude ask about folder trust?
Claude Code can read and modify files inside the folder it runs in. The trust prompt ensures you never accidentally give it access to a folder you did not intend. You will see this prompt once per new folder.

- Type hello, `what can you do?` and press `Enter` to confirm Claude Code is responding.

Claude Code should reply with a summary of its capabilities. You now have a working AI assistant in your terminal.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/claude-code-confirmation-working-successfully.png)

### Not seeing the welcome screen?
- Make sure you completed the browser login step. Check your browser for any open Claude authentication tabs.  
- If the browser showed a code instead of redirecting back, paste that code into the terminal where prompted. This happens when the browser cannot reach Claude Code's local callback server.  
- Try typing `claude` again. If you see a login prompt, your first attempt may have timed out.

### Check which model you're using
Claude Code can use different AI models behind the scenes. The model you get by default depends on your subscription plan. Pro subscribers default to Sonnet 4.6, while Max subscribers default to Opus 4.7.

- See which model you are currently using by typing this command and pressing Enter:
```bash
/model
```
A picker appears showing your current model highlighted. Press `Escape` to close it without changing anything.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/current-AI-model.png)

### When should I use each model?
Each model trades off between speed, capability, and how much of your subscription allowance it uses per response.
- `Sonnet` — fast and efficient. Handles everyday tasks like file organization, automation, and general questions. Default for Pro plans. Best choice for this project.
- `Opus` — most capable. Best for complex multi-step reasoning, large-scale analysis, and difficult problems. Default for Max plans. Uses significantly more of your allowance per response, so you get fewer total responses per day.
- `Haiku` — fastest and lightest. Good for quick, simple tasks like renaming a file or getting a short answer. Uses the least allowance but can miss nuance on complex prompts.

We'll stick to Sonnet 5 for this project as it's best fit for this project. 
Our AI assistant is installed and ready to go. Next up, we'll give Claude a real task and see its safety features in action.


## Step 2. Give Claude our First Task
Claude Code is installed and responding. Time to give it a real task with real files on our computer.

Our Downloads folder is full of random files that have piled up over weeks or months. In this step, we'll ask Claude to analyze that folder, propose an organization plan, and sort everything into subfolders. Along the way, we'll learn how Claude asks for our permission before doing anything.

In this step we'll:
- Ask Claude to analyze your Downloads folder.
- Learn how to approve or reject Claude's actions.
- Watch Claude organize your files into subfolders.

### Ask Claude to look at your Downloads folder
Before organizing anything, we want to understand what is in there. We will ask Claude to scan our Downloads folder and report back what it finds.

- Make sure Claude Code is open in your terminal. If you closed it, type claude and press Enter to start a new session.
- Type the following prompt and press `Enter`:
```bash
Look at my Downloads folder and tell me: how many files are there, what types of files do you see, and what is the oldest file?
```

![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/Downloads-folder-summary.png)

- If Claude Code shows a Permissions dialog listing the command it wants to run, press `Enter` to approve it.

Let's take a moment to read Claude's summary. I now know what is in my Downloads folder without opening a single file.

### How do I decide whether to approve?
Read actions are always safe. If Claude says it wants to move, rename, or delete something, read the details first. If you are unsure, deny it and Claude will explain what it needs.

### Tell Claude to organize it
Now that we know what is in there, We'll tell Claude how we want it organized and be specific about which file types go into which folders.

- I'll type the following prompt and press `Enter`. Customize the categories to match the file types Claude found:
```bash
My Downloads folder is a mess. Can you organize it into subfolders by file type? Show me your plan before you move anything.
```

![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/organize-plan-for-subfolder.png)

### Why ask Claude to show its plan first?
Including `show me your plan first` in your prompt forces Claude to stop and explain before acting. You get to see exactly how many files will move and where they will go. This is a habit worth building: as best practice ALWAYS ask Claude to show its work before making changes.

- Claude presents a plan showing how many files it will move to each subfolder. Read through it.
- If the plan looks good, type `yes` and press `Enter` to approve. In my case since I have sensitive files, I selected 4 and typed `Move all these files into a new Sensitive/ subfolder so they're easy to find`
- Claude starts moving files. It asks permission for each mv (move) command. Approve each one by pressing Enter.  

![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/moved-files-to-subfolders.png)

### Too many permission prompts?
If Claude asks permission for every single file move and you are tired of pressing `Enter`, look for the option that says `Always approve mv` or similar. Selecting it lets Claude run all `mv` commands for the rest of this session without asking each time.

### Use Plan Mode when you just want ideas
If you ever want Claude to think through a problem without touching any files, press `Shift+Tab` twice to enter `Plan Mode`. In this mode, Claude reads and analyzes but never moves, renames, or deletes anything.

Press `Shift+Tab` twice again to return to normal mode when you are ready to let Claude act.

### Three habits for better prompts
These three patterns work for any task you give Claude Code, not just file organization.

- Be specific: name the folder path, file types, and destination. Vague prompts produce vague results.
- Ask for a plan first: include `show me your plan before you start` so you always know what will happen before it happens.
- Build on results: after Claude finishes, refine with follow-ups like `also sort by date` or `undo that and try organizing by project instead`. Claude remembers the full conversation.

### Check what Claude did
Claude reports a summary when it finishes. But you should always verify with your own eyes.

- Open your Downloads folder in Finder (macOS) or File Explorer (Windows).
- You should see new subfolders eg: Documents, Images, Videos, and Misc.
- Open each subfolder and spot-check that the right files landed in the right places.
- Back in Claude Code, type `/cost` and press `Enter` to see how many tokens that task used.

![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/costs.png)

### Files ended up in the wrong folder?
No problem. This is normal. Just ask Claude to fix it. For example: `Move the PDFs from Misc into Documents` Claude remembers what it did and can correct individual files without re-running the whole organization.

Press `Esc` to dismiss the permission overlay and return to the main input where you can type your next prompt.

Your `Downloads` folder is organized and you have seen how Claude asks permission before every action. Next up, we'll teach Claude our preferences so it remembers how we like things done across every session.


### Step 5. Set Up CLAUDE.md
We just organized a real folder using nothing but plain English prompts. That proves Claude Code works.

But right now, every time we start a new session, Claude forgets everything about what we did. Our preferences, our naming style, which folders are off-limits. In this step,we will create a `CLAUDE.md` file that teaches Claude our preferences once so it remembers them automatically in every future session.

In this step we'll:
- Create a `CLAUDE.md` preferences file using the `/init` command.
- Fill it with your personal rules and organization style.
- Test that Claude remembers your preferences across sessions.

### Create your preferences file
Claude Code has a memory system built on a file called `CLAUDE.md`. This is a plain text file that Claude reads at the start of every session. Whatever instructions we write in it, Claude follows automatically without us needing to repeat ourselves.

- In my terminal (with Claude Code still running), I'll type the following command and press `Enter`:
```bash
/init
```
### What does `/init` do?

The `/init` command creates a `CLAUDE.md` file in the current folder. Claude Code reads this file at the start of every session and treats the contents as persistent instructions.
For personal preferences that apply "everywhere", the file lives at `~/.claude/CLAUDE.md` (our user-level preferences). For folder-specific preferences, it lives in the folder where we ran the command.

Claude Code will ask us a few questions about how we like to work. We'll answer them honestly. As an example, I'll type the following prompt into Claude Code:
```bash
Help me create a CLAUDE.md for my personal file management. Ask me questions about my preferences so you can write it for me.
```

### TIP: Ask the AI to interview you

When you don't know what you don't know, ask the AI to interview you. Instead of staring at a blank screen trying to think of every preference upfront, you hand that job to Claude.
Use this pattern anytime you need something personalized: writing a resume, configuring a tool, drafting project requirements. Say what you want to end up with and ask Claude to ask you the questions.


- Review the final `CLAUDE.md` by asking Claude to display it:
```bash
show me the final CLAUDE.md
```

Make sure it captures your actual preferences and remove anything generic.

### Test that your preferences work
The real test is whether Claude remembers our preferences after we reset the conversation. A fresh session forces Claude to re-read CLAUDE.md from scratch.

- I'll clear the current conversation:
```bash
/clear
```

- Now I'll ask Claude something about our files without mentioning our preferences. As an example, I want Claude to reorganize my Projects/ and show me his plan first in the terminal.
```bash
I want to reorganize my Projects/. What's your plan?
```

When I checked Claude's response, as you can see it already reflect our preferences (showing a plan first, asking before deleting, using our preferred organization style) without us having to remind Claude.

![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/plan-to-reorg-projects-dir.png)


### What should you see?
Claude's response should show that it already knows your rules. If you said `always show a plan before making changes`, Claude should present a plan and ask for approval rather than jumping straight into moving files.

If you said `never touch my Work folder`, Claude should either skip that folder or mention it as excluded.


### If Claude ignored my preferences?
Make sure you ran `/init` from the same folder where you are now working. Claude Code only reads `CLAUDE.md` files from the current directory or from `~/.claude/CLAUDE.md` (your global user preferences).

Try running `/init` again from the same folder to regenerate the file. Then run `/clear` and test again.

Our `CLAUDE.md` is set. From now on, every Claude Code session starts with my personal rules already loaded. We now have a working AI assistant that knows how we like things done. 


## Extra Credit
Digital Storage Audit

How much space is hiding in plain sight on my computer?

So what we'll do here is to create a single powerful workflow. We'll prompt Claude Code to scan multiple folders, cross-reference files for duplicates, surface forgotten large files, and produce a clean markdown report with actionable recommendations. Then we'll save the whole thing as a reusable command we can run monthly.

In this extra credit we'll:
- Scan two folders and identify duplicate files, large forgotten files, and empty folders.
- Generate a markdown report saved to our Desktop with findings and recommendations.
- Save the entire workflow as a reusable `/audit` command for monthly use.

### Start in Plan Mode to explore safely
This audit touches multiple folders and compares files across them. `Plan Mode` ensures Claude reads everything without changing anything until we're ready.
- Press `Shift+Tab` twice to enter Plan Mode.
- We'll choose two folders we want to audit. Since I'm using my test machine I'll my Projects and Downloads folders.
- I'll Use the prompt below as our starting point. In your case just replace each variable with your actual paths and values:
```bash
Scan your first folder path (e.g. ~/Documents or C:UsersYourNameDocuments) and your second folder path (e.g. ~/Downloads or C:UsersYourNameDownloads). Find: (1) duplicate files by comparing names and sizes, (2) files over size limit, e.g. 100MB not modified in time period, e.g. 6 months, (3) empty folders. Don't delete anything. Write a summary report to where to save, e.g. ~/Desktop/storage-audit.md with what you found, how much space I could recover, and what you recommend. Show me the report before saving it.
```

Actual example:
```bash
Scan ~/Downloads/ and ~/Projects/. Find: (1) duplicate files by comparing names and sizes, (2) files over 50MB not modified in 6 months, (3) empty folders. Don't delete anything. Write a summary report to ~/Projects/Claud-Projects/Get-Started-with-Claude/storage-audit.md with what you found, how much space I could recover, and what you recommend. Show me the report before saving it.
```

### Don't know what folders to check to test this out?
In you case you can choose your `Downloads` and `Documents` folders since these are the most common source of wasted space. Files pile up when you download something, move it to Documents, but the original stays in Downloads.  
Large files over 100MB that haven't been touched in 6 months are often installers, old exports, or video files you forgot about. Empty folders accumulate after reorganization and serve no purpose.

### Review Claude's findings before saving
The prompt asks Claude to show us the report before writing it to disk. This is our chance to refine.
- I'll review the report Claude shows me and check that it includes all five sections: duplicates found, large forgotten files, empty folders, total reclaimable space, and recommended actions. see storage-audit.md file.
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/storage-audit-report.png)


If something is missing or you want more detail, use Pattern 3 (build on results) to refine. For example:
```bash
That's good, but also sort the duplicates by size so I know which ones free up the most space first.
```
![alt images](https://github.com/CoyApilado18/Get-Started-with-Claude/blob/6ad7ca233662012ab998276df173f8a6e5806689/Images/duplicate-by-size-report.png)


- Once the report looks complete, switch to Normal Mode by pressing Shift+Tab to cycle back.
- Approve Claude's action when it asks to save the report file to your Desktop.
- Verify the file exists by asking Claude:
```bash
Confirm that storage-audit.md was saved to my current directory. Show me the first 10 lines.
```

### Save the workflow as a reusable command
The real power of this audit is running it monthly without re-typing everything. I'll save the entire workflow as a custom command that Claude remembers for me.
- I'll ask Claude to save the workflow by using this prompt:
Save this entire workflow as a custom command called 'audit' that I can run monthly. Since I made some changes for the command, below is what I typed in the prompt:
```bash
Yes. Save the initial workflow (from where I told you to "scan..") as a custom command called 'audit' that I can run monthly.
```

- In your case you can use this prompt:
```bash
Save this entire workflow as a custom command called 'audit' that I can run monthly.
```

This will be saved in the current folder under `.claude/commands/audit.md` you can view the `audit.md` file there.


To use `/audit` from any folder, copy the file to `~/.claude/commands/audit.md`. 
You need `commands/` first. Claude Code doesn't make `~/.claude/commands/` for you; it only reads the folder if it exists. You can create the folder and copy the command into it in one step:
```bash
mkdir -p ~/.claude/commands
cp ~/your-project-directory/.claude/commands/audit.md ~/.claude/commands/
```

Reset your conversation by running this command:
```bash
/clear
```

Test your saved command by running:
```bash
/audit
```

