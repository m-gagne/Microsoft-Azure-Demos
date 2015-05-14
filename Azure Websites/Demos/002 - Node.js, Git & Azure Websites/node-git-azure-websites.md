[[Home]](../../README.html)

# Node.js, Git & Azure Websites

[TOC]

## Prepping your machine

### Install Node.js for Windows

- Navigate to http://nodejs.org/
- Click `Install`
- Download & run the msi installer
	- Click `Next`
	- Accept the Terms & Conditions & Click `Next`
	- Click `Next`, unless you desire to change the installation directory
	- Click `Next` to accept the default install
	- Click `Install`
	- Click `Finish`

### Confirm the installation was successful

- Open a command prompt
	- `Start Key + R` then type `cmd <enter>`
- Type `node` and hit <enter>
- You should be greated with a '>' prompt where you could say enter `console.log("Well done yourself!");
- To exit hit `Ctrl+c` twice

### Install the Express Web Framework

Why use Express? It's a popular Node.js web framework (think what MVC & ASP.NET is to C# ). Also it prevents you from either copy+pasting a lot of code and saying "voila" or live coding and potentially getting a syntax error. 

Another good reason to install Express is that this is a **node package** (what nuget is to .NET). It shows that you can deploy these types of packages to Azure Websites easily!

- Install Express
	- In a cmd prompt run `npm install express --save -g`
- Install Express Generator (for scaffolding a sample app)
	- run `npm install express-generator -g`
- You can verify the installation worked by running (in a cmd prompt) `npm express`
	- You should see the command options displayed

### Install Git

- Download Git for Windows here: http://git-scm.com/download/win
	- Save & run the exe
	- Click `Next`
	- Click `Next` to accept the Terms & Conditions
	- Click `Next`, unless you desire to change the installation directory
	- Click `Next` to accept the default components
	- Click 'Next' to accept the default start menu shortcut
	- Select the second option **(x) Use Git from the Windows Command Prompt** and click `Next`
	- Select **(*) Checkout as-is, commit as-is** if you will not be sharing code across platforms (Windows and Linux). Otherwise if you will select **(*) Checkout Windows-style, commit Unix-style line endings** and click `Next`
	- De-select **[ ] View ReleaseNotes.rtf** and click `Finish`

### Running Git

You have two options for using Git in a command prompt

#### Using the Git Bash

- You can simply open a **Git Bash** which is a command prompt setup for Git by searching for `Git` and executing `Git Bash`
- If you do this I would recommend pinning it to your Taskbar or Start Screen for easier access when demoing

#### Use Git from Windows Command Prompt or Power Shell

- During the installation you did select the `(x) Use Git from the Windows Command Prompt` right? If not, no big deal, run the installer again and select this option, it will setup your paths accordingly (basically it adds `C:\Program Files (x86)\Git\Cmd` to your Systems' `Path` Environment Variable).
- You should be able to open any cmd or Power Shell prompt and run `git --version` to see if it's working.

#### Setting up Git

You will need to tell Git who you are (useful later when creating repositories and doing deployments).

- Open a cmd prompt (or Git Bash)
- Run `git config --global user.email "you@example.com"`
- Run `git config --global user.name "Your Name"`

## Demo Script

### Why we do this demo

This short demo (~10 minutes) highlights a number of key features & strengths of Azure including

- Support for Open-Source projects like Node.js
- Support for the broader Node.js development community with support for node packages
- Behind the scenes Azure Websites is powered by Azure VMs (IaaS) running IIS (Internet Information Services, our web server). This demo shows how well it can run Node.js
- Shows the source control & continuous integration support for Git (or GitHub and others)
- Showcases the roll-back feature of Azure Websites when using integrated source control
- Shows how in minutes you can setup an app using a real-world deployment strategy

### Demo Steps

#### Step 1: Create a Website with integrated source control

- Log into [Azure Management Portal](https://manage.windowsazure.com/microsoft.onmicrosoft.com)
- Click `+ New` > `Website` > `Quick Create` & enter a unique site name such as `NodeDemoSite`
	- *Speaking Tip*: Although this only takes a few seconds I like to at this point mention that
		- Azure has behind the scenes setup a website in IIS for you either on your own dedicated server (when using standard) or on a shared server (when using basic/shared).
- Click on your newly created site (NodeDemoSite) to view the **Quick Start** screen
- At the bottom you will see *Integrate source control* click on `Set up deployment from source control`
	- *Speaking Tip*: When the Source Control deployment wizard is visible scroll through the option and explain that Azure Websites integrates with many of today popular source control systems including Visual Studio Online, Git, GitHub, DropBox and more.
- Select `Local Git repository` from the list of source control origins & Click `->` (next)
	- *Speaking Tip*: At this point I usually comment that magic is happening. Azure is setting up a remote git repository for you to push your code to with hooks to detect with code is updated so it can automatically deploy it for you. For more on what's really going on (very technical) see the Open Source Kudu project: https://github.com/projectkudu/kudu/wiki
- Once complete you'll be on the Deployment screen, leave the browser here, it's time to write some code!

#### Step 2: Create a sample app

There are a number of ways to do this, you can start with a fully baked app, you can live code one, or you can do what I like to do which is use the Express generator to create a sample app (the equivalent in ASP.NET of doing File > New Website > ASP.NET Website)

To create your demo app

- Open a cmd prompt
- Navigate to a demo directory (e.g. c:\demos)
- Run `express demo-app` where `demo-app` is the name (and directory) your app will be created in
- run `cd demo-app` to change into the newly created directory (which includes your demo app)
- run `npm install` to install package dependencies
	- *Speaking Tip*: This could take a minute depending on your bandwidth. So I usually take this opportunity to explain that we are using Express since it's a popular framework and means we are demoing something more advanced than "hello world", i.e something closer to what they will likely do.
- with the packages installed you can run the app locally by running `npm start`
- show the running app by opening http://localhost:3000 in your favourite browser
	- *Speaking Tip*: I usually joke that now that we have a very complex app we can deploy it into production!

#### Step 3: Creating your apps Git repository

- Creating a local Git repository as as easy as init, add & commit
- In the `demo-app` directory 
	- run `git init .` to initialize the base Git repository
	- run `git add .` to add all new/changed files
	- run `git commit -am "Initial Commit"` to commit all (-a) files with the message (-m) "Initial Commit"
		- *Speakers Notes*: You might see errors having to do with CR/LF (carriage return & line feeds) which has to do with the way Windows & Linux handle newlines differently. You can ignore these, or if they are really bothering you run `git config --global core.autocrlf true`. Learn more [here](https://help.github.com/articles/dealing-with-line-endings/)

#### Step 4: Adding the Azure remote Git repository & pushing to production

Git doesn't have a central server like subversion, TFS or Visual Studio Online. To connect your local Git repository to a remote Git repository you add it as a remote.

Back in your open browser is some instructions on how to add the Azure remote origin Git repository.

- Go back to your browser that is open to the `DEPLOYMENTS` tab in the portal.
- Scroll down to Step 3: "Add remote Microsoft Azure repository and push your stuff"
- Copy and run the two commands
- It will prompt you for your Azure deployment credentials , enter your password and hit `<enter>`
	- Not clear on Deployment Credentials? [Documentation is here](http://azure.microsoft.com/en-us/documentation/articles/web-sites-manage/#ftp-credentials)
- At this point it should start pushing code to you Git repository connected to your Azure Website.
- It's a good idea to make sure your browser is visible as the `DEPLOYMENTS` page will update with status as the code is being commited and deployed
	- *Speakers Notes*: Explain that the magic (aka Kudu Service) is making use of Git Hooks to detect that a push is occuring and to prepare for a new deployment. You can further explain that Kudu will then take the new code and automatically deploy it for you!
- Once the deployment is complete (as indicated by the green checkmark and 'ACTIVE DEPLOYMENT') click `Browse` at the bottom to open your production website.
	- You should see a site come up with "Welcome to Express"

#### Step 5: "Breaking" the code and re-deploying

Here I like to "break" the code (usually just by changing text rather than code) and pushing it to Azure to simulate what happens when a "bad build" makes it to production. I usually prompt the audience for typical resolutions like putting up a maintenance page, live site investigation, deploying a backup of the code etc. Then I demo how easy you can re-deploy a previous commit allowing you to resolve your live site issues immediately. I then go on to explain you can deploy your app to another website for testing and resolution.

- "Break" the code by either introducing a bug, or by editing the text in `demo-app\views\index.jade`
	- I typically change `Welcome to #{title}` to `OMG I BROKE IT` :)
	- Commit & Push this change
		- `git commit -am "Who needs to test?"`
		- `git push azure master`
			- Enter your password when prompted
			- Navigate back to the browser on the Azure DEPLOYMENTS tab to show Azure picking up on the new push.
		- *Speakers Notes*: I like to joke about developers not following best practices, testing code, unit tests, integration tests etc. but rather just blindly pushing code into production like we have just done!
- Once Azure has deployed the new code (when the status changes from "Deploying..." to "Active Deployment") refresh the website to show them the "broken code"
- Explain that it's easy to revert back to working code without having to deal with backups or even being at the office/having access to the code.
- Back in your browser at your websites Azure DEPLOYMENTS tab
	- Click on the first commit (or any previous commit)
	- Click `REDEPLOY` (at the bottom)
- Explain that Azure is now automatically reverting to the previous commit so your web app will be back up and running in seconds
- Also explain that you can now create a test site, deploy to it to investigate the bug, or that you can use the staging feature of Azure Websites.

## The abridged version

Once you are comfortable with Node, Express, Git & Azure I find I only need a high level overview printed out to remind me of the steps

### Short Demo Script

* Create sample app using Express
	* `express demo-app`
* `Azure Portal` > `(+) NEW` > `Custom Create`
    * Enter unique name & select [x] Publish from source control
    * Select `Local Git Repository`
* Goto Deployments
* Add git repo to demo-app\

        git init .
        git add .
        git commit -am "Initial Commit"

* Add remote branch & push to Azure

#### Deploy Rollback

* Edit code
* Commit & Push to Azure
* Show changes, rollback