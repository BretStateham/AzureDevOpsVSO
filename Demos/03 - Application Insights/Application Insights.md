<a name="ApplicationInsights" />
# Monitoring Web Applications with Application Insights #

---
<a name="Overview" />
## Overview ##

In this demo, you will learn how to use **"Application Insights"** in **"Visual Studio Online"** to perform basic availability monitoring of a web application.  

<a id="goals" />
### Goals ###
In this demo, you will see how to:

1. Add **"Application Insights Telemetry"** to your Web Application
1. Add Usage monitoring to an ASP.NET Web Application
1. Create a Basic Availability Test to monitor your Web Application

<a name="technologies" />
### Key Technologies ###

- [Visual Studio Online](http://www.visualstudio.com/)
- [Application Insights](http://msdn.microsoft.com/en-us/library/dn481095.aspx)


<a name="Setup" />
### Setup and Configuration ###

1. This demo assumes that you have completed the **"Continuous Deployment with Visual Studio Online and Azure Websites"** demo.  If you haven't, you need to first complete the steps in that demo.

1. It is also especially helpful if you have ahead of time (hours or even days in advance) setup a web site with Availability Monitoring as described in this demo.  This will give you an existing set of Availability Monitoring data that you can refer to in the demo.  A brand new Single Url test will take a long time (hours) to build a usable data set. 

1. You may optionally have installed the "[Application Insights Tools for Visual Studio](http://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)" previously.  If it is already installed, fine, if not, you will install it as part of this demo. 

<a name="Demo" />
## Demo ##
This demo is composed of the following segments:

1. [Install the "Application Insights Tools for Visual Studio"](#InstallTools)
1. [Add Application Insights Telemetry to your Web Application](#AddTelemetry)
1. [Configure Availability Monitoring](#ConfigureMonitoring)

---

<a name="InstallTools" />
### Install the "Application Insights Tools for Visual Studio" ###

1. Open Visual Studio 2013 and from the menu bar, select **"TOOLS"** | **"Extensions and Updates..."**

1. In the **"Extensions and Updates*"" window, in the search box in the top right corner, type **"Application Insights"** and then in the search results, click the **"Download"** button for **"Application Insights Tools for Visual Studio"**

	![01010-Download](images/01010-download.png?raw=true "Download Application Insights Tools")

1. In the **"Download and Install"** window, click the **"Install"** button.

	![01020-Install](images/01020-install.png?raw=true "Install Applicaiton Insights Tools")

1. When the installation is complete, in the **"Extensions and Updates"** window, click the **"Restart Now"** button to restart Visual Studio

	![01030-Restart](images/01030-restart.png?raw=true "Restart Visual Studio")

---

<a name="AddTelemetry" />
### Add Application Insights Telemetry to your Web Application ###

1. In Visual Studio, re-open the Web Site project we created previously in the **"Continuous Deployment with Visual Studio Online and Azure Websites"** demo.

1. In the **"Solution Explorer"** window, right click the web application project (not the solution), and select  **"Add Application Insights Telemetry to Project..."** from the pop-up menu:

	![02010-AddTelemetry](images/02010-addtelemetry.png?raw=true "Add Telemetry")

1. In the **"Add Application Insights to Project"** window, confirm that the correct **"Visual Studio Online"** account is being used.  Note also that a **"Component"** (Application Insights "Application") will be created for monitoring, and that the name will be the same name as this web project.  If you need to change any of those settings, do so, using the **"Use different account"** and **"Configure settings"** links, otherwise, click the **"Add Application Insights To Project"** button:

	![02020-AddApplication](images/02020-addapplication.png?raw=true "Add Application")

1. When complete, a new **"ApplicationInsights.config"** node should appear under your project in the Visaul Studio **"Solution Explorer"** window.  If you click on the node, you will see that it is an XML file that contains Application Insights configuration for this web application.  This file is fully documented, but we won't discuss it further in this demo:
	
![02030-ApplicationInsightsConfig](images/02030-applicationinsightsconfig.png?raw=true "Applicaiton Insights Config")

1. In the **"Solution Explorer"** window, right-click the **"ApplicationInsights.config"** file and select **"Open Application Insights Portal..."** from the pop-up menu:

	![02040-OpenPortal](images/02040-openportal.png?raw=true "Open Portal")

1.  A browser window should open, enter your Visual Studio Online credentials if needed. 	Notice that a dashboard has been created for your web application.  Click the **"Administer Account"** (**Gear Icon**) in the top right corner to access the settings for the monitored application.

	![02050-AdministerAccount](images/02050-administeraccount.png?raw=true "Administer Account")

1. On the **"&lt;Your App Name&gt; Overview"** page, turn on the checkbox next to eh **"Send notifications about this application to"**, ensure the correct email address and click **"Apply"**:

	![02060-NotificationEmails](images/02060-notificationemails.png?raw=true "Notification Emails")

1. Next, click the **"Get configuration keys and downloads"** button:

	![02070-Configuration](images/02070-configuration.png?raw=true "Get Configuration")

1. On the **"Keys & Downloads"** page, scroll down the the **"JavaScript Usage Analytics Code"** and copy the script shown to the clipboard.

	> **Note:** Your instrumentation keys will differ from the ones shown here.

	![02080-CopyJavaScript](images/02080-copyjavascript.png?raw=true "Copy JavaScript")

1. Back in Visual Studio **"Solution Explorer"**, under the web application project, open the **"Views"** | **"Shared"** | **"_Layout.cshtml"** file, then immediately before the **closing &lt;/head&gt; tag, paste the JavaScript you just copied, and save the changes:

	> **Note:** The JavaScript logs a **"Page View""* with Application Insights.  The **"_Layout.cshtml"** file is used by all of the MVC views in the application so by adding the JavaScript to that file, it will get called for all views, and thus allow us to create an entry in Application Insights everytime a users views a page.  Cool!  Learn more about [Javascript usage analytics](http://msdn.microsoft.com/library/dn481098.aspx)

	![02090-PasteJavaScript](images/02090-pastejavascript.png?raw=true "Paste JavaScript")

1. We need to Check In our changes so they can be deployed to the live site.  In the **"Solution Explorer"** window, right click the solution, and choose **"Check In..." from the pop-up menu:

	![02100-CheckIn](images/02100-checkin.png?raw=true "Check In")

1. In the **"Team Explorer"** window, enter a **"Comment"** and click **"Check In"**.  As before, if prompted to confirm, click **"Yes"**

	![02110-CheckInChanges](images/02110-checkinchanges.png?raw=true "Check In Changes")

1. Upon successful check in, the Continous Deployment build definition that was created in the previous demo should automatically deploy the updates to the live website.  You can use the techniques discussed in the previous demo to monitor the build if you like. 

---

<a name="ConfigureMonitoring" />
### Configure Availability Monitoring ###

1. If needed, re-open the Application Insights portal for your application by right-clicking the **"ApplicationInsights.config"** node in the Visual Studio **"Solution Explorer"** and selecting **"Open the Application Insights Portal..."** from the pop-up menu: 

	![02040-OpenPortal](images/02040-openportal.png?raw=true "Open Portal")

1. In the **"Application Insights"** portal, click the **"AVAILABILITY"** link along the top, and ensure that your application is selected in the application dropdown.  Below the **"Create a single URL test."** header, enter the URL for your live web site (**http://&lt;your web site name&gt;.azurewebsites.net**), and click **"Create"**:

	> **Note:** In this step you are adding a **"Single URL Test"**.  Meaning that only a single URL is pinged.  Later, if needed, you can add a multi-URL test for more complex availability tests.  These types of tests are known as **"Synthetic Monitors"** because they test the site on an a "synthetic" schedule, rather than based on organic use of the site.

	![03010-SingleUrlTest](images/03010-singleurltest.png?raw=true "Single URL Test")

1. When the test is created (just a second or two), click the **"Success! Now head over to your availability report!"** box to see the report:

	![03020-Success](images/03020-success.png?raw=true "Success")

1. On the Availability page, you should now see a single test under your application titled **"My first test"**. Click on the name of the test to select it, then click the **edit** (**pencil**) icon to edit the test:

	![03030-EditMyFirstTest](images/03030-editmyfirsttest.png?raw=true "Edit My First Test")

1. In the **"EDIT SYNTHETIC MONITOR"** Window, edit the test to meet your desires. Give it:
	- A better (more meaningful name)
	- Choose more appropriate Locations to test from
	- Choose the desired frequency
	- Make the test more specific by requiring a certin HTTP status code or content to be returned for the test to be successful
	- Enable alerts if a certain number of test locations fail within a certain amount of time
	- Use the **Configure notification emails** link to modify the list of emails that will be notified if an alert is triggered. 
	- When you are done, click the **"OK"** button to save the changes.

	![03040-EditMonitor](images/03040-editmonitor.png?raw=true "Edit Monitor")

1. This is where it is really handy if you have previously configured a website for availability monitoring.  If you have done so, you can switch to that website now to view more interesting data.  If not, it will take some time (one set of data points every five minutes) before a useful report will be shown.

1.  Regardless of if you look at data for another site, or for the one you just configured, after a bit of monitoring, you should begin to see some data points on the **"AVAILABILITY"** page.  
	- You can change the time range you are looking at by clicking on the **"Selected date range"** link in the top right corner, or by actually dragging over a range of datapoints on the charts.
	- You can hover over a datapoint to see basic info on it

	![03050-DataPoints](images/03050-datapoints.png?raw=true "Data Points")

1. If you actually click on a data point, you can see the actual Web Test results (or a more recent web test result for the same site), including the Response details:

	![03050-WebTestDetails](images/03050-webtestdetails.png?raw=true "Web Test Details")

1. Lastly, if you switch to the **"USAGE"** page, you can view results like **"Top Pages"**, etc:

	> **Note:** This data is generated by the script that we added to **"_Layout.cshtml"** previously.  Again, this data takes a while to collect. Plus, as this is a demo site, there won't be much actual usage against it. 

	![03060-TopPages](images/03060-toppages.png?raw=true "Top Pages")

--- 

<a name="summary" />
## Summary ##

Congraulations!  In this demo you learned the basics of:

- Adding Appliation Insights Telemetry to a Web Application
- Configuring Usage monitoring for a web site
- Configuring Availability monitoring for a web site



	
