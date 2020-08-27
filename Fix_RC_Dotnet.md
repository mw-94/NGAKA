## Issue
Dotnet package on RC is not being installed properly

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
- You'll need root access to the RC and the RC will need to be able to reach the public internet
- You can download the dotnet.tar.gz file here: https://github.com/mw-94/D42-Shared/blob/master/dotnet.tar.gz

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
