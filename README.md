## CI For Flask Application using Github Actions
### Step 1: Create the Flask App 
In Flask Application there are multiple file Main file is app.py. For requirements there is requirement.txt file where your dependencies are written.
### Step 2: Create .github/workflow/main.yml file
in that file we will write our CI pipeline
Check the main.yml file in this github repository and download Artifact
### Step 3 : Deploy the Artifact On IIS Server
Install wfastcgi and Enable it 
wfastcgi.py provides a bridge between IIS and Python using WSGI and FastCGI, similar to what mod_python provides for Apache HTTP Server.

It can be used with any Python web application or framework that supports WSGI, and provides an efficient way to handle requests and process pools through IIS.
open Powershell/cmd and Install it 
```
pip install wfastcgi
```
open the folder in cmd which is downloded and type
```
wfastcgi enable
```
This give you the path of wfastcgi copy it 
open Web.config file and in handler --Scriptprocesser paste the path 
```
<add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Users\QPL0038\AppData\Local\Programs\Python\Python312\python.exe|C:\Users\QPL0038\AppData\Local\Programs\Python\Python312\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" requireAccess="Script" />
```
Go to your folder -- properties-- security -- Give permission to user and IIS user to modify this file.
in Appsetting value type your file name if app.py type app.app
```
<appSettings>
	<add key="WSGI_HANDLER" value="app.app" />
```
in pythonpath give value of your folder 
```
	<add key="PYTHONPATH" value="C:\inetpub\wwwroot\Flask_New" />
	<add key="WSGI_LOG" value="C:\inetpub\wwwroot\Flask_New\app.log" />
</appSettings>
```
save this file in the folder
go to IIS give the path of this file write the port deploy your app


if the error is HTTP error 500.0 -- FastCGI Error
Go to IIS manager
Click on your server's Application Pools tab
Click Set Application Pool Defaults...
Set the Identity under Process Model to LocalSystem


for this Flask Deployment you must have in configuration of Application Developement CGI Enable
