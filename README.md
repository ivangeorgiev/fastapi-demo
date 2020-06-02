# fastapi-demo
Python FastApi Demo



## Setup the environment

Create a virtual environment:

```bash
py -3.7 -m venv .venv
```

Activate the virtual environment:

```bash
#bash
source .venv/Scripts/activate
```

```powershell
#PowerShell
. ./.venv/Scripts/Activate.ps1
```

Create `requirements.txt` file:

```
fastapi
uvicorn
```

Install the dependencies:

```bash
pip install -U fastapi uvicorn
```



## Create the API

Place your API code inside `application.py` file:

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

You can use other name for the file. Modify the following commands accordingly.

Commit your app to git.

## Create the Web App

In Azure create a new Web App resource.

Modify the Web App startup command. You can do this manually. Here is an example using PowerShell:

```powershell
$WebApp = Get-AzWebApp -ResourceGroupName fastapidemo-rg -Name fastapidemo
$WebApp.SiteConfig.AppCommandLine = 'python -m uvicorn application:app --host 0.0.0.0 --port 8000'
Set-AzWebApp -WebApp $WebApp
```



Modify the Deployment Settings. If you are using local git option, select App Service Kudu. You will get an url like following:

```
https://fastapidemo.scm.azurewebsites.net:443/fastapidemo.git
```

From deployment credentials get the credentials.

```
git remote add azure-hello https://fastapidemo.scm.azurewebsites.net:443/fastapidemo.git
git commit --allow-empty -m 'first deployment'
git push azure-hello master
```

Here is sample output from `git push`

```
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 193 bytes | 193.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0)
remote: Deploy Async
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '0fe79c0936'.
remote: Repository path is /home/site/repository
remote: Running oryx build...
remote: Build orchestrated by Microsoft Oryx, https://github.com/Microsoft/Oryx
remote: You can report issues at https://github.com/Microsoft/Oryx/issues
remote:
remote: Oryx Version      : 0.2.20200312.1, Commit: 8fe90af07018bd4454a39b0edea6ecc5119642da, ReleaseTagName: 20200312.1
remote: Build Operation ID: |yFDxE/tqtpk=.52d8f570_
remote: Repository Commit : 0fe79c0936c007b19f4e2e481147d05176aacc4f
remote:
remote: Warning: An outdated version of python was detected (3.7.7). Consider updating.\nVersions supported by Oryx: https://github.com/microsoft/Oryx
remote:
remote: Using intermediate directory '/tmp/8d8073d9db9198d'.
remote:
remote: Copying files to the intermediate directory...
remote: Done in 0 sec(s).
remote:
remote: Source directory     : /tmp/8d8073d9db9198d
remote: Destination directory: /home/site/wwwroot
remote:
remote: Python Version: /opt/python/3.7.7/bin/python3
remote: Python Virtual Environment: antenv
remote: Creating virtual environment ...
remote: ........
remote: Activating virtual environment ...
remote:
remote: Upgrading pip...
remote: Collecting pip
remote:   Using cached https://files.pythonhosted.org/packages/43/84/23ed6a1796480a6f1a2d38f2802901d078266bda38388954d01d3f2e821d/pip-20.1.1-py2.py3-none-any.whl
remote: Installing collected packages: pip
remote:   Found existing installation: pip 19.2.3
remote:     Uninstalling pip-19.2.3:
remote:       Successfully uninstalled pip-19.2.3
remote: Successfully installed pip-20.1.1
remote: Done in 12 sec(s).
remote: Running pip install...
remote: [21:41:22+0000] Collecting fastapi
remote: [21:41:22+0000]   Downloading fastapi-0.55.1-py3-none-any.whl (48 kB)
remote: [21:41:23+0000] Collecting uvicorn
remote: [21:41:23+0000]   Downloading uvicorn-0.11.5-py3-none-any.whl (43 kB)
remote: [21:41:24+0000] Collecting pydantic<2.0.0,>=0.32.2
remote: [21:41:24+0000]   Downloading pydantic-1.5.1-cp37-cp37m-manylinux2014_x86_64.whl (7.3 MB)
remote: [21:41:26+0000] Collecting starlette==0.13.2
remote: [21:41:26+0000]   Downloading starlette-0.13.2-py3-none-any.whl (59 kB)
remote: [21:41:27+0000] Collecting uvloop>=0.14.0; sys_platform != "win32" and sys_platform != "cygwin" and platform_python_implementation != "PyPy"
remote: [21:41:27+0000]   Downloading uvloop-0.14.0-cp37-cp37m-manylinux2010_x86_64.whl (3.8 MB)
remote: [21:41:28+0000] Collecting websockets==8.*
remote: [21:41:28+0000]   Downloading websockets-8.1-cp37-cp37m-manylinux2010_x86_64.whl (79 kB)
remote: [21:41:28+0000] Collecting click==7.*
remote: [21:41:28+0000]   Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
remote: [21:41:28+0000] Collecting httptools==0.1.*; sys_platform != "win32" and sys_platform != "cygwin" and platform_python_implementation != "PyPy"
remote: [21:41:28+0000]   Downloading httptools-0.1.1-cp37-cp37m-manylinux1_x86_64.whl (217 kB)
remote: [21:41:29+0000] Collecting h11<0.10,>=0.8
remote: [21:41:29+0000]   Downloading h11-0.9.0-py2.py3-none-any.whl (53 kB)
remote: [21:41:29+0000] Installing collected packages: pydantic, starlette, fastapi, uvloop, websockets, click, httptools, h11, uvicorn
remote: ....
remote: [21:41:39+0000] Successfully installed click-7.1.2 fastapi-0.55.1 h11-0.9.0 httptools-0.1.1 pydantic-1.5.1 starlette-0.13.2 uvicorn-0.11.5 uvloop-0.14.0 websockets-8.1
remote: Done running pip install.
remote:
remote: Compressing existing 'antenv' folder...
remote: ......
remote: Done in 10 sec(s).
remote:
remote: Copying files to destination directory '/home/site/wwwroot'...
remote: Done in 1 sec(s).
remote:
remote: Removing existing manifest file
remote: Creating a manifest file...
remote: Manifest file created.
remote:
remote: Done in 57 sec(s).
remote: Running post deployment command(s)...
remote: Triggering recycle (preview mode disabled).
remote: Deployment successful.
remote: Deployment Logs : 'https://fastapidemo.scm.azurewebsites.net/newui/jsonviewer?view_url=/api/deployments/0fe79c0936c007b19f4e2e481147d05176aacc4f/log'
To https://fastapidemo.scm.azurewebsites.net:443/fastapidemo.git
   27a1cdc..0fe79c0  master -> master
```



## Appendix A. Update Web App configuration using Azure CLI

Create a `settings.json` file:

```json
{
  "appCommandLine": "python -m uvicorn application:app --host 0.0.0.0 --port 8000"
}
```

Apply settings:

```powershell
az webapp config set -n fastapidemo -g fastapidemo-rg --generic-configurations '@settings.json'
```



## Quick Notes

uvicorn app:app --host 0.0.0.0 --port 8000 --reload

Specify Startup Command:

```bash
python -m uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

```powershell
$WebApp = Get-AzWebApp -ResourceGroupName fastapidemo-rg -Name fastapidemo
$WebApp.SiteConfig.AppCommandLine = 'python -m uvicorn app:app --host 0.0.0.0 --port 8000 --reload'
Set-AzWebApp -WebApp $WebApp
```

```bash
gunicorn --bind=0.0.0.0 --timeout 600 app:app
```



```powershell
az webapp config show --name fastapidemo --resource-group fastapidemo-rg
```





https://docs.microsoft.com/en-us/azure/app-service/containers/how-to-configure-python

