<a name="ContinousDeployment" />
# Continuous Deployment with Visual Studio Online and Azure Websites #

---
<a name="Overview" />
## Overview ##

In this demo, we'll show you how to configure Continous Deployment using Visual Studio Online and Azure Websites.

<a id="goals" />
### Goals ###
In this demo, you will see how to:

1. Create a Team Project in Visual Studio Online
1. Create an Azure Web Site
1. Link your Azure Website to your Visual Studio Online Team Project
1. Perform Continous Builds using Visual Studio Online

<a name="technologies" />
### Key Technologies ###

- [Azure Web Sites](http://azure.microsoft.com/en-us/documentation/services/web-sites/)
- [Visual Studio Online](http://www.visualstudio.com/)


<a name="Setup" />
### Setup and Configuration ###

In order to execute this demo you need to do a little prep.

1. ***IMPORTANT - Follow all of the steps in this demo to create a Visual Studio Team Project, Azure Website and Web Project.  Having the site deployed ahead of time, along with the Application Insights and Load Testing Steps in subsequent demos allow you to demo with real information.  If you do this on the fly, the Application Insights data will be sparse and un-interesting.  

1. Ensure that you have installed the Azure SDK (latest version) on your demo machine (or VM).  Go to http://azure.microsoft.com/en-us/downloads/ and click the **"VS 2013 Install"** link, then follow the prompts. 

1. Optionall install the "Windows Azure Powershell" command line toos.  
	- From the Windows Start menu, type "Microsoft Web Platform Installer" and in the search results click the link to launch it. 
	- In the Web Platform Installer search box, type **"Azure PowerShell"**
	- Click the **"Add"** button to the right of **"Windows Azure PowerShell"**
	- Clikc the **"Install"** button and follow the prompts to complete the installation

1. Optionally the "[Application Insights Tools for Visual Studio](http://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)", although we won't use the Applicaiton Insights tools in this demo.   

<a name="Demo" />
## Demo ##
This demo is composed of the following segments:

1. [Create a Team Project in Visual Studio Online](#CreateTeamProject)
1. [Create an Azure Web Site and link it to your Team Project](#CreateWebSite)
1. [Create a Web Project and Check It In](#CreateWebProject)
1. [Verify Continuous Deployment](#VerifyContinuousDeployment)

---

<a name="CreateTeamProject" />
### Create a Team Project in Visual Studio Online ###

1. If you don't already have a Visual Studio Online Account, create one here: <http://go.microsoft.com/fwlink/?LinkId=307137>

1. Sign into your own Visual Studio Online site at **https://&lt;your vso account name&gt;.visualstudio.com** 

1. If this is your first time in, you should be prompted to create a new project.  If not, under **"Recent projects & teams"**, click the **"New"** link to create a new Team Project. 

	![01010-NewTeamProjectLink](images/01010-newteamprojectlink.png?raw=true "New Link")

1. In the **"CREATE NEW TEAM PROJECT"** pop-up, complete the fields as such, and click the **"Create project** button:

	- **Project Name**: Any name
	- **Description**: Any description
	- **Process Template**: Microsoft Visual Studio Scrum 2013
	- **Version Control**: Team Foundation Version Control

	![01020-CreateNewTeamProjectPopUp](images/01020-createnewteamprojectpopup.png?raw=true "Create New Team Project Pop-Up")

1. Wait until the team project creation is complete, then click the **"Navigate to project"** button:

	![01030-NavigateToProjectButton](images/01030-navigatetoprojectbutton.png?raw=true "Navigate To Project Button")

1. In the team project page, click the **"CODE"** link along the top, and note that other than the default **"BuildProcessTemplates"** folder, there isn't any content in the source code repository:

	![01040-EmptyCodeRepository](images/01040-emptycoderepository.png?raw=true "Empty Code Repository")

1. Then, click the **"BUILD"** menu along the top, and confirm that there are no build definitions currently exist:

	![01050-NoBuildDefinitions](images/01050-nobuilddefinitions.png?raw=true "No Build Definitions")

---

<a name="CreateWebSite" />
### Create an Azure Web Site and link it to your Team Project ###

1. Open the Azure Management Portal (https://manage.windowsazure.com)

1. First, let's show the available web site templates.  Click **+NEW**" | **COMPUTE** | **WEB SITE** | **FROM GALLERY**:

	![02010-FromGallery](images/02010-fromgallery.png?raw=true "From Gallery")

1. In the **"ADD WEB APP"** pop-up, scroll through the list of available templates, to show them, but rather than actually creating a site from a template, click the **"x"** button in the top right corner to close the pop-up window:

	![02020-WebSiteGallery](images/02020-websitegallery.png?raw=true "Web Site Gallery")

1. To create the actual site, click **+NEW+** | **COMPUTE** | **WEB SITE** | **CUSTOM CREATE**

	![02030-CustomCreate](images/02030-customcreate.png?raw=true "Custom Create Web Site")

1. In the **"NEW WEB SITE - CUSTOM CREATE"** window, complete the fields as follows, and click the **Next** (right arrow) button to continue:

	- **URL** : Enter a valid, unique host name for your web site.
	- **WEB HOSTING PLAN**: Choose, or create a new free web hosting plan as needed
	- **REGION**: Pick an appropriate region
	- **DATABASE**: No Database
	- **Publish from source control**: **CHECKED** - **IMPORTANT** - this is the point of the demo.  Make sure you enable this checkbox. 

	![02040-CreateWebSite](images/02040-createwebsite.png?raw=true "Create Web Site")

1. On the **"Where is your source code?"** page, select **"Visual Studio Online** and click **Next**

	![02050-VisualStudioOnline](images/02050-visualstudioonline.png?raw=true "Visual Studio Online")

1. On the **Authorize connection** enter the name of your **Visual Studio Online** account, and click the **Authorize Now** link:
	
	![02060-AuthorizeVsoAccess](images/02060-authorizevsoaccess.png?raw=true "Authorize VSO Account Access")

1. Another browser window should appear prompting you to allow you website to access your Visual Studio Online account.  Click the **Accept** button. 

	![02070-Accept](images/02070-accept.png?raw=true "Accept")

1. On the **"Chose a repository to deploy"** page, select the Visual Studio Online team project you create in the previous demo.  

	![02080-ChooseTeamProject](images/02080-chooseteamproject.png?raw=true "Choose Team Project")

1. Back in the Azure Management Portal, wait until the new website's status says **"Running"**, then, right-click on the link to the website to the right, and select **"Open in new window"**

	![02090-WebsiteLink](images/02090-websitelink.png?raw=true "Website Link")

1. Then in the window that opens, verify that a place holder page is shown, and close the browser witht he placeholder page when done:

	![02100-PlaceholderSite](images/02100-placeholdersite.png?raw=true "Placeholder Site")

1.  Lastly, open the "Team Project" again back in your **"https://&lt;your account name&gt;.visualstudio.com"** visual studio online account, and on the **"BUILD"** page, notice that there is now a **"&lt;WebSiteName&gt;_CD"** build definition.  The **"CD"** stands for **"Continuous Deployment"** and is the build definition that will cause our site to be built and deployed on each check in.  We'll look at its configuration later. 

	![02110-BuildDefinition](images/02110-builddefinition.png?raw=true "Build Definition")

---

<a name="CreateWebProject" />
### Create a Web Project and Check It In ###

1. Back on the **"Websites"** page of the Azure Management portal, click on the name of your new website to open it's dashboard:

	![03010-OpenWebsiteDashboard](images/03010-openwebsitedashboard.png?raw=true "Open Website Dashboard")


1. Click on **"DEPLOYMENTS"** along the top, and you should see that your site is linked to your Visual Studio Online account.  Click the **"VISUAL STUDIO"** link along the bottom to open the associated team project in Visual Studio.  (You don't have to do it this way, you could connect to the team project in Visual Studio manually instead):

	![03020-LaunchVisualStudio](images/03020-launchvisualstudio.png?raw=true "Launch Visual Studio")

1. If prompted, click the **Checkmark** button to confirm the launch of Visual Studio (the dialog says 2012, but 2013 is better!

	![03030-OpenVisualStudio](images/03030-openvisualstudio.png?raw=true "Open Visual Studio")

1. Visual Studio should be launched, and in the **"Team Explorer"** window, you should see that you are connected to the team project in Visual Studio Online:

	![03040-TeamExplorer](images/03040-teamexplorer.png?raw=true "Team Explorer")

1. From the Visual Studio menu bar, select **"FILE"** | **"New"** | **"Project..."**, then in the **"New Project"** window, under the list templates select **"Installed"** | **"Templates"** | **"Visual C#"** | **"Web"**, then select the **"ASP.NET Web Application"** Project template.  Give it a name and location and **MAKE SURE THE "ADD TO SOURCE CONTROL" CHECKBOX IS CHECKED!**, also, if the Application Insights options are available, make sure **"Add Application Insights to Project"** option is **NOT CHECKED** (You could do it here, but we'll do it later in the next demo instead):

	![03050-NewProject](images/03050-newproject.png?raw=true "New Project")

1. In the **"New ASP.NET Project"** window, select **MVC"**, turn on the checkbox for **Add unit tests"** and **UNCHECK** the **"Host in the cloud"** checkbox.  We will host it in the cloud, but we have already configured that by connecting our Azure Website to our Visual Studio Online team project.  

	![03060-NewWebSite](images/03060-newwebsite.png?raw=true "New Web Site")

1. In the **"Choose Source Control"** dialog, select **"Team Foundation Version Control"** and click **"OK"**:
	![03070-TeamFoundationVersionControl](images/03070-teamfoundationversioncontrol.png?raw=true "Team Foundation Version Control")

1. In the *""Add Solution to Source Control"** window, select the Team Project you created earlier, and click **"OK"** 

	![03080-SelectTeamProject](images/03080-selectteamproject.png?raw=true "Select Team Project")

1. In the **"Solution Explorer"** window, open the **"Views"** | **"Home"** | **"Index.cshtml"** file, and modify the content of the first **&lt;h1&gt;ASP.NET&lt;/h1&gt;** tag to something unique, then run it to ensure the site works locally:

	![03090-ModifySiteAndVerify](images/03090-modifysiteandverify.png?raw=true "Modify Site and Verify")

1. Verify that the site runs properly in the browser, then close the browser window:

	![03100-VerifySite](images/03100-verifysite.png?raw=true "Verify Site")

1. Finally, let's check in our changes to the website.  In the Visual Studio Solution Explorer, right click on the name of the solution (make sure to select the solution, not just the project) and select **"Check In..."** from the pop-up menu 

	![03110-CheckInSolution](images/03110-checkinsolution.png?raw=true "Check In Solution")

1. In the **"Team Explorer"** window, enter a comment, and click the **"Check In"** button.

	![03120-CheckIn](images/03120-checkin.png?raw=true "Check In")

1. If prompted, click &&"Yes"** to confirm the check in:

	![03130-ConfirmCheckIn](images/03130-confirmcheckin.png?raw=true "Confirm Check In")

1. Wait for the Check In to complete:

	![03140-CheckInComplete](images/03140-checkincomplete.png?raw=true "Check In Complete")

---

<a name="VerifyContinuousDeployment" />
### Verify Continuous Deployment ###

1. Remember that when we linked the Azure Web Site to our Visual Studio Online Team Project, and **"&#42;_CD"** build definition created for us in Visual Studio Online.  Now that we have checked-in, we should see that the build definition has been queued (or possibly already completed).  We can see in in various places:

	> **Note:** As luck would have it, the deployment went very quickly as I was writing these steps.  As "Murphy" would have it however, it often takes significantly longer during live demos.  Be prepared to waith for the build / deployment process to take a long time (sometimes 5-10 minutes) before it completes.  If you look at it while it is still in process the build will be "Queued" rather than "Completed".  You can also open the queued build in both the Visual Studio Online website, as well as from within Visual Studio to monitor it's progress.  


1. In the Visual Studio **"Team Explorer"** window's **"Builds"** page: 

	![04020-TeamExplorerBuilds](images/04020-teamexplorerbuilds.png?raw=true "Team Explorer Builds")

1. On the **BUILD** page for our Visual Studio Online Team Project (depending on how fast you look it may be under **"Queued"** or **"Completed"**):

	![04010-CompletedBuildInVSO](images/04100-completedbuildinvso.png?raw=true "Completed Build in VSO")

1. As well as from the **"DEPLOYMENTS"** page for our website in the Azure Management Portal:

	![04030-WebSiteDeployments](images/04030-websitedeployments.png?raw=true "Web Site Deployments")

1. Finally, if the deployment has completed, we can verify that the site is now live.  Open the **http://&lt;your website name&gt;.azurewebsites.net" site in the browser, and verify that the created website is now live (Refresh the browser if necessary). 

	![04040-LiveWebSite](images/04040-livewebsite.png?raw=true "Live Web Site")

1. Lastly, back in Visual Studio, in the **"Team Explorer"** window, click the **Home** button along the top, then select **Builds** from the list of options. 

	![04050-Builds](images/04050-builds.png?raw=true "Builds")

1. Then in the list of builds, at the bottom, right click the **&#42;_CD** build definition for your website, and select **"Edit build defintion..."** from the pop-up menu:

	![04060-EditBuildDefinition](images/04060-editbuilddefinition.png?raw=true "Edit Build Definition")

1. On the **"Trigger"** page, note that **"Continous Integration - Build each check-in"** is selected:

	![04070-Trigger](images/04070-trigger.png?raw=true "Trigger")

1. On the **"Source Settings"** page, notice that the source is set to the entire team project.  You could be more specific if you wanted:

	![04080-SourceSettings](images/04080-sourcesettings.png?raw=true "Source Settings")

1. And finally on the **"Process"** page, note the project that will be built is our Web project, the Unit Tests will be run, and it will be deployed to our Azure Website when it was done!  You can close the build definition when you are done. 

	![04090-Process](images/04090-process.png?raw=true "Process")
	

--- 

<a name="summary" />
## Summary ##

Congraulations!  In this demo you learned the basics of:

- Creating Visual Studio Online Team Projects
- Creating Azure Web Sites
- Using Continuous Deployment Builds with Visual Studio Online