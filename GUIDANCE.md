# Welcome Lab Creators!

You can follow this guiandance yourself if you want to do it yourself.  However, we **highly recommend** using GitHub Copilot to work on your behalf.  It will both make this process easier for you and improve the outcome.

Go leverage github copilot

1. Open up this repo in a GitHub Codespace (or your favorite dev environment).
    1. Click the green 'code' button and then choose to create a new codespace'
    <img width="315" height="68" alt="image" src="https://github.com/user-attachments/assets/8c626100-21f0-4473-8047-d3c262911d9c" />
    3. Let it load.
3. open a chat window with copilot.  Ask it:

`prompt
read guidance.md and help me get this repo ready to publish
`

**GitHub Pages Setup Guide**

For Content Creators: This guide is designed to help you work with GitHub Copilot to prepare your Lab repository for publication through GitHub pages. Copilot will ask you questions and help implement the necessary changes to meet all repository requirements.

For Copilot: When a content creator asks you to help prepare their repository, read this entire file and guide them through each step interactively. Ask questions to gather the information you need, then implement the changes. Work through the tasks in order.

CRITICAL RULE FOR COPILOT:

NEVER infer, assume, or add information that the content creator hasn't explicitly provided
DO NOT fill in gaps with what you think should be there
ALWAYS highlight missing or unclear information and ask the creator about it.  You can make suggestions to them about things to add, but only after they approve it. 
Only work with what is explicitly given to you
If something is missing, point it out and ask: "I don't see [X] in your content. Do you want to add it, or should I proceed without it?"

How This Works
The content creator will ask you to "help me prepare my repo for publication" or similar
You'll read this GUIDANCE.md file to understand what needs to be done
You'll work through each step, asking the creator for necessary information
You'll implement the changes as you go
At the end, you'll help delete this GUIDANCE.md file

Step-by-Step Setup Instructions
Work through these steps in order with the content creator:

## Step 1: Decide about Documentation

Creator:  Some labs we've seen in the past could use some help cleaning up and prettifying. The instructions folder is the right place to put all the steps that your going to ask your learners to walk through.

If its ready and polishied you can just paste it into the instructions folder as is.  If you'd like copilot to see if it can refactor it.

Copilot - CRITICAL INSTRUCTIONS:

DO NOT INFER OR ADD ANY INFORMATION that is not explicitly in the source content
DO NOT fill in gaps or make assumptions about what should be included
DO HIGHLIGHT anything that appears to be missing or incomplete.
DO make suggestions about what could be added.
Only transform and reorganize what is actually provided

Ask the content creator:

"Do you have your lab content ready?"

If NO: "Let me know when it's ready and I can help you structure it. We should keep GUIDANCE.md until then."
If YES: Continue with questions below
"Where is your lab content located?"

Check common locations: /lab/instructions/, /instructions, /exercises, rawlab.md, /lab/README.md, or root directory .md files
Show the creator what you found: "I found content in [location]. Is it good to go, or Would you like to see what I can do polishing it up? You can always delete what I create without any risk"

If No: Go to step 2.

If Yes:
"I'm going to review the content now. I'll only use what's explicitly written - I won't add or infer anything."

Review the content and report back:

"I found [X] exercises/sections in your content"
Flag missing elements: "I notice the following might be missing or unclear:"
Prerequisites/setup instructions?
Expected outcomes for each exercise?
Navigation between sections?
Any introductory context?
Ask: "Should I proceed with just what's here, or do you want to add these missing pieces first?"
Only after they confirm, structure the content:

Create folders that match the structure in their content (e.g., /instructions/exercises/exercise-1/)
Start subfolder numbering at 01
Copy content verbatim - do not paraphrase or embellish
Create an index.md landing page with navigation
Update the nav: section in mkdocs.yml
If student setup instructions exist in the source, create /instructions/student-setup/, otherwise skip it

## Step 2: Update README.MD Content

Copilot: You may be able to determine the lab title from the name of the repository, or from the readme.  If you can, ask the content creator to confirm your belif.  If you can't, just ask them for it:

### "What is your lab title?" (e.g., "Azure Monitor Lab")

Update the main heading in README.MD.  

### "What is your session description?  Would you like me to suggest a description?" (2-3 sentences about what the session covers)

Replace "Add Session Description" section

### "What are the 3 main learning outcomes?  Would you like me to suggest some?" (What will learners be able to do after completing this session?)

Come up with some suggestions if asked.
Fill in the bullet points under "🧠 Learning Outcomes"

### "What technologies are featured in this session? Would you like me to suggest some?" (List the main technologies)

Come up with some suggestions if asked.
Fill in the numbered list under "💻 Technologies Used"
IMPORTANT: Use Learn MCP server to identify good links on learn.microsoft.com to share with customers so they can learn more.

### "Who are the content owners besides you?" (Names and GitHub usernames)

Update the Content Owners table
Remove extra placeholder entries if only one owner
Then update the README.MD file with this information and remove the placeholder
Ask the content creator for information needed to complete the table.  Search on github if necessary or if it would be helpful.

### How customers in a guided session get started?

Copilot: Ask if the lab requires an Azure subscription and if so, in the getting started section, include a link to the Azure Free Trial at https://aka.ms/azure-free-account

Copilot: If this is a self paced lab :ask "For learner performing this lab, what steps do they need to take to get started?"  If you think you know the answer from reading their content, suggest a possible set of steps for the user. 

Fill in the ### 🏫 Getting started in a guided session section.

### How learners learning on their own get started

Reminder: we are creating public repositories so customers are able to follow this guidance on their own.  We know they were

Fill in the ### 🏠 Getting started in your own environment section.  Make sure the customers know that they will be using their own environments and so will be paying cloud costs to go through these steps themselves.

If this is a guided session, ask the creator "Are customers in their own environment able to take this lab?"  

If they say no, ask them why not.  Add "Note: you may be unable to follow all of these steps in your own environment because" and complete the sentence with the reasons the creator provided to the readme. 

## Step 3: Clean Up Folder Structure

Please use these standard subfolder names so customers can have a consistent experience:
 /data if your session includes data that will be procesed during the session
 /src if your session includes source code to share with customers
 /instructions if your session includes several steps for customers to follow. The majority of your content should be in the instructions folder.

Copilot: Ask the content creator about possible sub folders. Remind them that consistency is key for customer experience:

"Are you going to be sharing source code with customers in your session?" 

If they say yes, ask them if they'd like you to create an src folder to house it. If they say yes, create it. 

Same questions for data and instructions folders. Available folders and their purposes:

data/ - for session data files
instructions/ - for documentation (keep if using MkDocs)

## Step 4: Remove Placeholder Content from /instructions

Check the /instructions folder for placeholder content
Remove the 01-demo folder if it exists
Remove the old README.md file from /instructions (it will conflict with index.md for MkDocs)
Remove any other placeholder files from /instructions/artifacts/

### Step 6: Verify Documentation Structure
Before proceeding, verify:

 All lab content is in the /instructions folder
 The mkdocs.yml nav section lists all your pages
 Run mkdocs serve to preview and check for errors
 All links work correctly

### Step 7: Update GitHub Repo Settings (Manual Step)
Remimd the creator that they'll have to complete this step:  Have them Click the gear icon ⚙️ in the upper right of the GitHub repo
Set a good description of this repo.  Suggest a description from earlier.
Add technology tags (same items from Technologies Used section).  Suggestion the tags from the Technologies Used section.

As the content creator if they've completed the repo settings step. 

## Step 9: Slides and Recordings

Show a summary of everything completed
Ask: "Are you satisfied with all the changes? Should I delete GUIDANCE.md now, or would you like to review anything first?"
If they confirm, delete this file with rm GUIDANCE.md
Remind them: "Don't forget to update the GitHub repository settings (description and tags) through the repository settings page"
Questions?
If you encounter issues or need clarification as a content creator, surface through your content lead or ping Mike Kinsman on teams.
