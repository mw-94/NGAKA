## Issue
Dotnet package on RC is not being installed properly

## Requirements to fix
- You'll need root access to the RC and the RC will either need to be able to reach the public internet or you will need another host in the customers environment to scp from
- You can download the dotnet.tar.gz file here: https://github.com/mw-94/D42-Shared/blob/master/dotnet.tar.gz
- You will need a publicly routable linux VM to download this file to so you can SCP it from the customers RC (or another host in their environment that you can upload/download the file to and SCP from that.

## Steps to resolve
1. First verify that this is actually the issue

        systemctl status job-manager
        
- If it is, you should see something like this:

        job-manager.service - D42 Job Manager
        Loaded: loaded (/etc/systemd/system/job-manager.service; enabled; vendor preset: disabled)
        Active: failed (Result: start-limit) since Tue 2020-08-18 10:34:49 EDT; 1 weeks 1 days ago
        Process: 1878 ExecStart=/usr/bin/dotnet /opt/rc/services/job-manager/JobManager.dll (code=exited, status=203/EXEC)
        Main PID: 1878 (code=exited, status=203/EXEC)

2. Copy dotnet package from remote source to RC  

        scp remoteuser@remotehost:dotnet.tar.gz ~/

3. Unpack the tar.gz file  
- Create a temp folder and unpack the tar.gz file to that folder

        mkdir temp && tar -xzf dotnet.tar.gz -C temp && cd temp

4. Install the dotnet packages
- Make sure you are in that temp folder

        rpm -Uvh libicu-50.1.2-17.el7.x86_64.rpm dotnet-host-2.1.6-x64.rpm dotnet-hostfxr-2.1.6-x64.rpm dotnet-runtime-2.1.6-x64.rpm aspnetcore-runtime-2.1.6-x64.rpm dotnet-runtime-deps-2.1.6-rhel.7-x64.rpm

5. Restart job manager and verify fix is working
- dotnet should execute without any errors if it is working as expected

        systemctl start job-manager
        journalctl -u job-manager
        dotnet

6. Attempt a discovery job using the RC and exit root if task executes
