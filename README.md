# Table of contents
General info, objectives <br>
Requirements, limitations <br>
Configuration, usage | Use case 1 <br>
Configuration, usage | Use case 2 | Initial uploading and extending over SSH <br>
Configuration, usage | Use case 3 | Integrate the rm_calendar with the rm_calendar_memo <br>
• optional configurations, debugging, notes <br>
Tested environments <br>
References

# ======== General info, objectives ====

* See this video demonstration: https://www.youtube.com/watch?v=YAz8Y30VeO0
* The current repo has all the RM-specific files, which are required and related to the one single PDF document, the "rm_calendar.pdf" file. 
* It's possible to transfer the PDF without the need for enabling the "Developer Mode", and "use it as it is (PDF file)" - for that see **"Use Case 1"**.
* Because the current PDF document is a hyperlinked calendar, it's possible to extend it easily, however, in "Developer Mode" - see **"Use Case 2"**.
* Also, if you would like to benefit from the **"Calendar memo app for Remarkable"** app in conjunction with the current PDF file, see **"Use Case 3"**.
* It's crucial that, if you opt-in for the **Use Case 2**, **Use Case 3**, it would be needed to enable the "Developer mode" and SSH access.

# ======== Requirements, limitations, features ====
**(LIMITATIONS)** Currently, the TODO List/planner has the calendar until the 28 February 2025. <br>
**(FEATURE)** Each calendar page contains the calendar placed on top of the page. Each date of that calendar is hyperlinked and can be navigated to. <br>
**(LIMITATIONS)** For the **"supported RM+versions"** refer to the "Tested environments" section of the current memo. <br>
**(REQUIRED)** Make sure you are aware how to enable the "USB Web interface" on RMPP. Consult **Reference 3**, section `How to enable USB transfer on your reMarkable` to get to know more about it. <br>
**(Use Case 2,3 | REQUIRED)** Know your "<RMPP_SSH_ROOT_PASSWORD>" password for SSH. Consult the **Reference 1**, section "Accessing your reMarkable Paper Pro via SSH". <br>
**(Use Case 2,3 | REQUIRED)** "ssh" command available from the terminal. On MacOS it is available by default. For Windows consult **Reference 2**. <br>

# ======== Configuration, usage | **Use case 1** ====
**Unpack the current repo into some folder. Choose which format do you prefer (currently 2 formats of PDF are available). And then change directory to it, "format1" or "format2"**. <br>
Enabling the USB connection. To verify and proceed further, navigate to the `Settings` - `Storage` , and there would be section `USB connection`. Make sure it's enabled (checked). <br>
Right after that, below, you'd see the HTTP URL, like **"http://10.11.99.1"** (it could be different for you). Note that down. <br>
On your Windows/MacOS/Linux (depending on what you use) machine, open the browser of your preference and navigate to that address you've noted down. <br>
You should see your RMPP file structure. There would be button `Import`. Click on that and specify the `rm_todo_calendar_format1.pdf` or `rm_todo_calendar_format2.pdf`, depending on the `format` you have chosen earlier. <br>
Check on your RMPP, you should be able to see the new file. That's it, you can use it. <br>

# ======== Configuration, usage | **Use case 2** | **Initial uploading and extending over SSH** ====
* <a name="step_a"></a> **[Use case 2 | Step A](#step_a)** Connect your RMPP device to your Mac/Windows via the USB C cable. After that you need to make sure the "USB web interface" is enabled. <br>
After that, navigate to the "Settings" - "Storage" , and there would be section "USB web interface". <br>
Locate the IP address of your RMPP, written after the "http://". Note it down somewhere in your notepad as "<RMPP_IP_ADDRESS>". <br>
About "USB web interface" consult **Reference 3**. Open the terminal (let's label it **"Terminal 1"**) on your Mac or Windows and execute these commands:
```
ssh root@<RMPP_IP_ADDRESS>
root@<RMPP_IP_ADDRESS>'s password:
# It would prompt you for the password, so, enter it and then hit "enter":
<RMPP_SSH_ROOT_PASSWORD>
```
**NOTE**: For the **"ssh"** command itself make sure the "Requirements", **(Use Case 2 | REQUIRED)** sections have been reviewed. <br>
**NOTE**: The value of <RMPP_SSH_ROOT_PASSWORD> is visible from the "General > About > Copyrights and licenses" page of the RMPP itself. <br>

Once we have accessed the RMPP, let's also now execute this command to being able to write files into the system folders, as we would needed this later on:
```
umount -l /etc
mount -o remount,rw /
```

* <a name="step_b"></a> **[Use case 2 | Step B](#step_b)** Previous steps have confirmed that you have the SSH connection from your MacOS or Windows to your RMPP device. <br>
The next step would be to transfer the files using the SFTP rather than Web UI, because we need to transfer without modification of the files. <br>
At this point, depending on the OS type, there can be used many tools to transfer the files using SFTP, consult **Reference 4**. <br>
In this manual I would be using tool called "scp" , and would be using MacOS platform. Open another **"Terminal 2"**. Navigate to the project dir. <br>
From inside that folder let's execute this command:
```
[bash Downloads]$ pwd
/Users/<my_user_id>/Downloads
[bash Downloads]$ ls -ltra rm_calendar
total 16672
-rw-r--r--@  1 staff   4.0M Nov 21 19:32 rm_todo_calendar.pdf
-rw-r--r--@  1 staff   4.0M Nov 21 19:32 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pdf
-rw-r--r--@  1 staff   106B Nov 21 19:32 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pagedata
-rw-r--r--@  1 staff   229B Nov 21 19:32 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.metadata
-rw-r--r--@  1 staff    34B Nov 21 19:32 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.local
drwxr-xr-x@  2 staff    64B Nov 21 19:32 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff
drwx------@  7 staff   224B Nov 21 21:32 ..
-rw-r--r--@  1 staff    11K Nov 21 21:36 LICENSE
-rw-r--r--@  1 staff   6.9K Nov 21 21:51 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.content
-rw-r--r--@  1 staff    13K Nov 21 22:33 README.md
drwxr-xr-x@  3 staff    96B Nov 21 22:34 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.thumbnails
drwxr-xr-x  12 staff   384B Nov 21 22:34 .
[bash Downloads]$ cd rm_calendar
[bash Downloads]$ scp -r 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff* root@<RMPP_IP_ADDRESS>:/home/root/.local/share/remarkable/xochitl/
root@<RMPP_IP_ADDRESS>'s password:
# It would prompt you for the password, so, enter it and then hit "enter":
<RMPP_SSH_ROOT_PASSWORD>
430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.content                                                          100% 7077     3.8MB/s   00:00
430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.local                                                            100%   34    37.4KB/s   00:00
430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.metadata                                                         100%  229   162.2KB/s   00:00
430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pagedata                                                         100%  106    61.4KB/s   00:00
430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pdf                                                              100% 4140KB  18.0MB/s   00:00
5eb37c39-6f7b-4e60-92c2-fa90d836a6b3.png                                                              100% 1045   374.0KB/s   00:00
```
**NOTE**: The value of <RMPP_SSH_ROOT_PASSWORD> is visible from the "General > Help > About > Copyrights and licenses" page of the RMPP itself. <br>

* <a name="step_c"></a> **[Use case 2 | Step C](#step_C)** Once we have completed uploading the files, we can verify whether they have been uploaded correctly, from the "Terminal 1". <br>
```
root@<MY_RMPP_HOSTNAME>:~# cd /home/root/.local/share/remarkable/xochitl/
root@<MY_RMPP_HOSTNAME>:~/.local/share/remarkable/xochitl# ls -ltra | grep 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff
drwxr-xr-x    2 root     root          4096 Nov 21 20:15 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.thumbnails
drwxr-xr-x    2 root     root          4096 Nov 21 20:15 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff
-rw-r--r--    1 root     root       4239569 Nov 21 21:40 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pdf
-rw-r--r--    1 root     root           106 Nov 21 21:40 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pagedata
-rw-r--r--    1 root     root           229 Nov 21 21:40 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.metadata
-rw-r--r--    1 root     root            34 Nov 21 21:40 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.local
-rw-r--r--    1 root     root          7077 Nov 21 21:40 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.content
```

* <a name="step_d"></a> **[Use case 2 | Step D](#step_d)** Extending the "rm_calendar.pdf" with the new content. <br>
**Use this step only if you have updated your existing PDF file, on the Windows/Mac/Linux and would like to update it on your RMPP** <br>
**Also, make sure to only Extend the original PDF, and Not "cut" it, like do not remove existing pages, only add pages, if you need**. <br>
Check the instructions from the **Use case 2 | Step B** , but in this case, only reupload the single file **430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pdf** <br>
(do not reupload the other files or folders)
```
[bash Downloads]$ scp -r 430f8cdf-e2e8-412c-b7e3-5ebf3b126bff.pdf root@<RMPP_IP_ADDRESS>:/home/root/.local/share/remarkable/xochitl/
```
**NOTE**: The point is that the RMPP would store all the "strokes/markings" within the "430f8cdf-e2e8-412c-b7e3-5ebf3b126bff/" **directory itself**, and we are not touching that files, but only replacing the original PDF file.

# ======== Configuration, usage | Use case 3 | Integrate the rm_calendar with the rm_calendar_memo ====
This use case is documented as part of the separate repository. Here is the direct link https://github.com/anti22dot/rm_calendar_memo?tab=readme-ov-file#-configuration-usage--use-case-1--integrate-the-rm_calendar-with-the-rm_calendar_memo-

# ======== Tested environments ====
```
* Tested combination 1 | Device: Remarkable Paper Pro, firmware: 3.15.2.1
* Tested combination 2 | Device: Remarkable Paper Pro, firmware: 3.15.3.0
* Tested combination 3 | Device: Remarkable Paper Pro, firmware: 3.16.0.60
* Tested combination 4 | Device: Remarkable Paper Pro, firmware: 3.16.1.0
* Tested combination 5 | Device: Remarkable Paper Pro, firmware: 3.17.0.62
```

# ======== References ========
• [Reference 1](https://support.remarkable.com/s/article/Developer-mode) <br>
• [Reference 2](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) <br>
• [Reference 3](https://support.remarkable.com/s/article/importing-and-exporting-files) <br>
• [Reference 4](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol) <br>
• [Reference 5](https://en.wikipedia.org/wiki/Universally_unique_identifier) <br>
