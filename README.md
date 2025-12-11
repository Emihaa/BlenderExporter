# BlenderExporter

I need to create an exporter to Blender. But before that, I need to build something that allows me to share tools with other team members. So, a user joins the company, installs Blender, and now they need to get our tools on it and later update them. I want this to work so that the user needs to update GIT and tools automatically update. 

Problems: 
- We don't know what kind of hard disk structure the target computer have and can't assume anything. The only thing we can assume is that in user folder, there can be a folder bob (C:\users}[user]\bob or ~user/bob in Mac)
- We don't know where tools are in the game. That information needs to get into the blender somehow
- We can also have different projects with different tools and partly shared tools.
  
Assignments: Comme up with a plan on how to solve this, what kind of tool is would be. Send the plan to me for review, and once approved, make it a reality.


## Suggestion:

Create a bootstrapper plugin for Blender. Because we know that there will always be a folder <i>"bob"</i>, no matter what, the bootstrapper finds that as a root folder. Basically the user can do git clone the address of Blender exporter to their <i>"bob"</i> folder that when installed as a plugin to Blender will run the bootstrapper script to search through the computer. If it doesn't find existing games or tools it installs them to the user, if user chooses they want Project A or Project B. Shared will be installed if neither of the projects is chosen.

Hierarchy:

- bob
  - Blender exporter
    - bootstrapper.py
    - config.json


<b>The config.json</b> files holds the up-to-date information of projects & tools. Their names, versions, and githup repository addresses. So for example:
The expectation is that we have Project A and Project B. Each of these game projects have their own tools (Blender plugins?) and there is also shared folder that holds inside tools that both of the projects use.
The config.json knows the names of the games and searches them by the name from <i>"bob"</i> children. The Blender tools that are known should exist per project and from shared, are being searched by <i>*/toolname.py</i>.
I think it makes sense that this information is known what projects game studio has and what tools are being used and the config.json file can be updated as projects and tools grow. This means that it is enough that only config.json file is updated by the programmer/tech artist when update is done to a tool or project. And then artist can do a git pull (throught terminal or by Blender UI) and the config.json gets updated, and it will activate the bootstrapper script as well.

<b>The bootstrapper.py</b> will do the code logic run. It will do the search from the <i>"bob"</i> folder to children. It knows from <i>config.json</i> file what it is supposed to find. If it doesn't find a project A, it will allow user manually choose a folder, or then give option to install the project or tool straight from git repo. It will also update plugins if user so chooses (the UI should have update button).

Hierarchy:

- bob
  - Blender exporter
    - bootstrapper.py
    - config.json
  - Project A (either found or created)
    - Game
    - tools
  - Project B (either found or created)
    - Game
    - tools
  - Shared (either found or created)
    - tools
