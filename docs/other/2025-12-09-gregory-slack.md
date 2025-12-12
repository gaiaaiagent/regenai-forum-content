Gregory
  Today at 8:53 AM
I am using the GPT KOI right now and finding some issues.  I will try to make a full report.
40 replies
Gregory
  Today at 8:54 AM
issue 1: Aneka.io is no longer an active explorer, so we need to update docs to reflect that fact.  only mintscan.io works now, or direct ledger / registry api interfaces
Gregory
  Today at 9:03 AM
It looks to me like the issue is the Regen KOI bot does not have the regen ledger MCP integration, so it is not really able to produce accurate real time queries of onchain data, so it is just making things up.
Gregory
  Today at 9:15 AM
here is a link to the chat, in case that’s useful in improving MCP performance: https://chatgpt.com/share/e/69385920-f140-800d-931a-c9e707b083b3
Darren Zal
  Today at 9:35 AM
the Regen KOI mcp is seperate from the ledge mcp (that JuanCarlo started), we would combine them easily if you want
shawn
  Today at 9:41 AM
image.png
 
image.png


shawn
  Today at 9:50 AM
@Gregory Can you tell me the prompt?
Gregory
  Today at 9:54 AM
I understand that these are two seperate MCPs.  however our KOI certainly must be able to accurately query the params, credits and data onchain.
9:54
and or we need a sub agent it can query for those requests in a routing system
9:58
here is the full output: https://docs.google.com/document/d/1C3Usgs6gLIaVKL8ZZCpqp4sVQFl-2B6guqkVim56Pww/edit?tab=t.0
Google Docs


Google Docs Logo
KOI MCP test 1 GPT Output
Document in Google Docs
9:58 AM


shawn
  Today at 9:59 AM
@Gregory I asked claude code which is connect to both MCPs:
Please discover the aggregate value of all credits that have ever been issued on the regen chain. (edited) 
Gregory
  Today at 10:00 AM
Nice.  I need to get my claude code running etc.  I still keep getting sucked into work flows instead of getting tooling set up!
shawn
  Today at 10:00 AM
image.png
 
image.png


Gregory
  Today at 10:00 AM
mind putting that into a .md or google doc or something?
shawn
  Today at 10:00 AM
Sure
10:01
But we can add both MCPs to the KOI GPT and also tell the KOI GPT to not make up data.
Gregory
  Today at 10:02 AM
here was my original prompt:
10:02
what is the total number of credits, their credit class information, and the number of hectares of land managed that the total and each class represents, as well as their dollar value, live on regen ledger right now?
10:03
that list of credits does not look complete to me.  for instance it is missing kulshun carbon trusts biochar, terrasos, ecometric, and some others i think
10:04
i had a call get canceled.  I am going to review forum post and see if I can’t get claude code running and get myself connected to both MCPs.
10:04
wish me luck!
shawn
  Today at 10:06 AM
Because of limitation on post lengths I split the post into two. The first post is about architecture and motivation for KOI. The second post being put out this week will be about installation and usage. And I'm gathering good direction from this discussion now.
I can start working on that post now and hopefully have it up tomorrow. (possibly today)
shawn
  Today at 10:36 AM
https://www.notion.so/regennetwork/Aggregate-Credit-Values-MCP-Test-2c425b77eda1806881e8ce7cb8da7569
image.png
 
image.png
Gregory
  Today at 10:40 AM
could you share details about how you set up claude code repos on your local machine?
10:40
just want to make sure I am doing that part in the best possible way
10:41
also @shawn you are now the highest level of user
10:41
so you should be able to go to town on the forum
shawn
  Today at 10:41 AM
Oh awesome!
10:41
Thanks!
10:41
Yeah I'll make a quick notion doc now.
Gregory
  Today at 10:41 AM
i can also make either you or darren or both admins if you want
10:41
if we want to play with forum as a key knowledge repo and automate anything there.
shawn
  Today at 10:42 AM
Sure perhaps you can make both of us admins.
Gregory
  Today at 10:47 AM
will do
Darren Zal
  Today at 10:51 AM
"could you share details about how you set up claude code repos on your local machine?"  do you mean how you install the MCP servers to work with claude code?  or how to initialize a repo when working with claude code (create a claude.md etc)? or both?
shawn
  Today at 11:03 AM
This works for me for a fresh installation of three mcps (KOI MCP, Regen MCP, and Python Regen MCP)
https://www.notion.so/regennetwork/Claude-Code-MCP-Setup-2c425b77eda180729dc9cc377043c4ed
11:03
I didn't include the registry MCP but I could include that as well.
Darren Zal
  Today at 11:09 AM
pros for cloning the repos:
- You can modify the source code
 - Test changes before they're published
 - Run from a specific branch or commit
 - Useful for development/debugging
for the koi mcp you can also install it for claude code with
claude mcp add regen-koi npx regen-koi-mcp@latest
Pros:
 - One command, instant setup
 - Auto-updates (always gets @latest from npm)
 - Works globally across all projects
BUT, you cannot modify the code
shawn
  Today at 11:10 AM
I historically find that claude mcp add command very brittle, often not working. I find the cloning method to be more reliable. But if it works that's great, the auto-updating is very valuable.
11:10
I appended a second version in the doc that includes the registry mcp.
Darren Zal
  Today at 11:15 AM
I just tested it and it worked for me, but please let me know if it is not working, another thing is that the local clone approach with .mcp.json is project-scoped, not global right?  so the MCPs would only be available when you're in that directory (regen-mcps, or its subdirectories)?
I think to get them to work from any directory you could do:
# 1. Create a permanent home for the MCPs
  mkdir -p ~/regen-mcps/mcps
  cd ~/regen-mcps

  # 2. Clone the MCP repos
  git clone https://github.com/regen-network/mcp.git mcps/mcp
  git clone https://github.com/gaiaaiagent/regen-koi-mcp.git mcps/regen-koi-mcp
  git clone https://github.com/gaiaaiagent/regen-python-mcp.git
  mcps/regen-python-mcp
  git clone https://github.com/gaiaaiagent/regen-registry-review-mcp.git
  mcps/regen-registry-review-mcp

  # 3. Build the MCP servers
  cd mcps/mcp && npm install && npm run build && cd ../..
  cd mcps/regen-koi-mcp && npm install && npm run build && cd ../..
  cd mcps/regen-registry-review-mcp && uv sync && cp .env.example .env && cd ../..

  # 4. Add to global Claude Code settings
  claude mcp add-json regen-koi
  "{\"command\":\"node\",\"args\":[\"$HOME/regen-mcps/mcps/regen-koi-mcp/dist/index
  .js\"],\"env\":{\"KOI_API_ENDPOINT\":\"https://regen.gaiaai.xyz/api/koi\"}}"

  claude mcp add-json regen "{\"command\":\"node\",\"args\":[\"$HOME/regen-mcps/mcp
  s/mcp/server/dist/index.js\"],\"env\":{\"NODE_ENV\":\"production\"}}"

  claude mcp add-json regen-network "{\"command\":\"uv\",\"args\":[\"run\",\"--dire
  ctory\",\"$HOME/regen-mcps/mcps/regen-python-mcp\",\"python\",\"main.py\"],\"env\
  ":{\"PYTHONPATH\":\"$HOME/regen-mcps/mcps/regen-python-mcp/src\"}}"

  claude mcp add-json registry-review
  "{\"command\":\"uv\",\"args\":[\"run\",\"--directory\",\"$HOME/regen-mcps/mcps/re
  gen-registry-review-mcp\",\"python\",\"-m\",\"registry_review_mcp.server\"],\"env
  \":{\"REGISTRY_REVIEW_LLM_EXTRACTION_ENABLED\":\"true\"}}"

Now the MCPs are available in any directory when you run claude.
(edited)



