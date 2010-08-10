.. object:: directories

    Use this option to add or remove directories to be monitored (they must be comma separated).

    **Default:** /etc,/usr/bin,/usr/sbin,/bin,/sbin 

    **Attributes:**

    - **realtime**: Value=yes 

        - This will enable realtime/continous montoring on linux using the inotify system calls.

    - **report_changes**: Value=yes 

        - Report diffs of files changes.  This is limited to text files at this time.  

    - **check_all**: Value=yes 

        - All the following check_* options are used together.  
        
    - **check_sum**: Value=yes

        - Check the md5 and sha1 hashs of the  of the files will be checked.  

          This is the same as using both check_sha1sum="yes" and check_md5sum="yes"
          
    - **check_sha1sum**: Value=yes

        - When used only the sha1 hash of the files will be checked.  

    - **check_md5sum**: Value=yes

        - The md5 hash of the files will be checked.  

    - **check_size**: Value=yes

        - The size of the files will be checked.  

    - **check_owner**: Value=yes

        - Check the owner of the files selected 

    - **check_group**: Value=yes  

        - Check the group owner of the files/directories selected 

    - **check_perm**: Value=yes 
       
        - Check the UNIX permission of the files/directories selected.
          On windows this will still on check POSIC permissions. 

    **Allowed:** Any directory or file name 

.. object:: ignore 

    List of files or directories to be ignored (one entry per element).

    **Default:** /etc/mtab
    
    **Attributes:**

    - **type**: Value=sregex 

        - This is the regex pattern to use to filter out files to not generate alerts on.  

    **Allowed:** Any directory or file name 

.. object:: frequency

    Frequency that the syscheck is going to be executed (in seconds).

    The default is 6 hours or 21600 seconds

    **Default:** 21600

    **Allowed:** Time in seconds 

.. object:: scan_time 

    Time to run the scans (can be in the formats of 21pm, 8:30, 12am, etc) 

    **Allowed:** Time to run scan

.. object:: scan_day 

    Day of the week to run the scans (can be in the format of sunday, saturday, monday, etc)

    **Allowed:** Day of the week

.. object:: auto_ignore 

    Specifies if syscheck will ignore files that change too often (after the third change) 

    **Default:** no

    **Allowed:** yes/no 

.. object:: alert_new_files 

    Specifies if syscheck should alert on new files created. 

    **Default:** no 

    **Allowed:** yes/no 

.. object:: scan_on_start 

    Specifies if syscheck should do the first scan as soon as it is started.

    **Default:** yes 

    **Allowed:** yes/no 

.. object:: windows_registry

    Use this option to add Windows registry entries to be monitored (Windows-only). 

    **Default:** HKEY_LOCAL_MACHINE\Software 

    **Allowed:** Any registry entry (one per element)
    
.. object:: registry_ignore 

    List of registry entries to be ignored.

    **Default:** ..Cryptography\RNG

    **Allowed:** Any registry entry (one per element) 


