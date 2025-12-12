shawn
  5:29 AM
gmaia team :evergreen_tree:
I have a first draft of the Regen Registry Assistant MCP live.
I made a loom video here: https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb
You can interact with the MCP here: https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant/c/693187b8-68b0-8333-8f8a-581347791497
It's implemented here: https://github.com/gaiaaiagent/regen-registry-review-mcp
The associated Eliza Agent is here: https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar
I'm planning on having the Agent hosted at registry.regen.gaiaai.xyz (hitting some deployment snags, I think I need to do some DNS modification to get it working.)
Meanwhile, the Eliza Agent can be ran locally.
So there are two reference agents using one MCP.
Claude Code or other IDEs are also good for connecting to the Registry MCP.
Currently the MCP saves data in a directory on the server. The next iteration is intended to iterate on that model to be able to connect to google drive directly.
Happy to provide more information in the coming days and weeks and continue iterating on this with feedback from the team. (edited) 


Transcript from Loom:
Hey Regens, I wanna give you an update on the Registry Review Assistant and how to test out this new agent.
0:12
Umm, there's two ways that I'd like to show off. One is this link to this GPT, the Registry Review Assistant, on, chat GPT that has access to the Registry Review MCP server, and additionally, We can run this locally.
0:32
This is just a branch on the Gaia repo. Oh. So I have this locally. Umm, and that's just unrun dev.
0:42
And we have this. . . Eliza OS agent here. Umm, that is also connected to the MCP. P. So we can see how these work.
0:54
I can say here, list sessions is generally how I start this off. So why don't we do that? In both cases, list sessions.
1:03
Uhm, okay, regen registry assistant. Houston. Is thinking. And here the gptu version is working. Okay. Okay. So, list sessions, umm, returns a, table of currently active review sessions.
1:32
Umm. Sessions generally have, uhh, they're initialized with a name. Uhm, and then they have a current, current, uhh, um, status, umm, number of documents, um, coverage and stage.
1:48
the edge. So, usually this should render as a markdown table, but let's just keep going here. So, okay, let's say load, Uhh, the bot-me-e-e-e-e-e-e-e-e-e-e-e-e.
2:03
loaded up. Okay, and this one is still rolling. Okay. Okay. So here we've loaded the botany farm soil carbon project.
2:18
And we can see the phases that this has moved. It's gone through evidence extraction. Umm, let's start a new, let's start a new, start a new, uhh, second.
2:29
Umm, let's start a called, umm, test a, okay, confirm. firm. And. And, new review session created, okay?
2:48
Uh, upload your documents. So, umm, yes. Please generate an upload link. So, this is what I want to show off.
2:56
This is how this works. If you want to upload documents to the GPT here, it's going to- I'll do that.
3:01
I'm going you a link. You can click that link. You can select- like to find out. In this case, I can upload the, um, example, uh, files here.
3:12
There. Open. And upload. I love it. Okay, upload complete. That puts the f- ills on the server. I can say complete.
3:29
Uhm, and on the server, those PDFs. Are going to be transformed and processed into markdown files. And those markdown files are mapped, uh, via the a.
3:41
So I'll just say continue, and it's going to do the requirements mapping according to the default checklist. list. Okay, it has some items requiring attention.
3:55
attention. Umm, let's, let's just proceed. So would you like to confirm all mappings? and move on to evidence extraction? Okay, so this is an opportunity for review by the registry agent.
4:13
And. All right. Umm, but let's suppose we've reviewed that and it's okay. So we're going to go through the uhh.
4:21

Umm, requirements mapping, phase, evidence extraction complete for test A. Okay. , , , Here's the evidence extraction. Next step is cross-validation. So let's continue with that.
