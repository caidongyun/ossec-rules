
.. _manual-syscheck:

Syscheck
========

**Syscheck** is the name of the integrity checking process inside OSSEC. It runs periodically 
and checks if any configured file (or registry entry on Windows) has changed.

Why Integrity checking?
-----------------------

This is the explanation from the `OSSEC book`_:

    There are multiple types of attacks and many attack vectors, but there
    is one thing unique about all of them: they leave traces and always change
    the system in some way. From viruses that modify a few files, to kernel-level
    rootkits that alters the kernel, there is always some change in the
    integrity of the system.

    Integrity checking is an essential part of intrusion detection, that
    detects changes in the integrity of the system. OSSEC does that by
    looking for changes in the MD5/SHA1 checksums of the key files in the
    system and on the Windows registry.

    The way it works is that the agent scans the system every few hours
    (user defined) and send all the checksums to the server. The server
    stores the checksums and look for modifications on them. An alert
    is sent if anything changes.

Quick facts
-----------

* How often? 
  
  - By default every 6 hours or at any configured time/day.

* Where is the database stored? 
  
  - In the manager.

* Where it helps me with compliance? (PCI DSS, etc) 

  - It helps with sections 11.5 (install FIM software) and 10.5 (integrity checking of log files) of PCI.

* How much CPU it uses? 
  
  - The scans are performed slowly to avoid using too much CPU/memory.

* How it deals with false positives? 
  
  - Files that change too often can be ignored on the configuration or using the rules.

Configuration options
---------------------

All these configurations options can be specified in each agent ossec.conf file, except 
for the "auto_ignore"" and “alert_new_file” which are manager side options. The 
“ignore” option if specified on the manager becomes global for all the agents.


.. include:: ../syntax/ossec_config.syscheck.rst 

Configuration Examples
----------------------

Configuring syscheck is very simple. First, you need to provide the files or directories 
to check. Note that when you specify a directory, it will monitor all its files recursively. 
Example:

.. code-block:: xml

    <syscheck>
        <directories check_all="yes">/etc,/usr/bin,/usr/sbin</directories>
        <directories check_all="yes">/root/users.txt,/bsd,/root/db.html</directories>
    </syscheck>

To ignore a few files or directories, use the “ignore” option (or registry_ignore 
for Windows registry entries):

.. code-block:: xml 

    <syscheck>
        <ignore>/etc/random-seed</ignore>
        <ignore>/root/dir</ignore>
        <ignore type="sregex">.log$|.tmp</ignore>
    </syscheck>

You can also set the “type” attribute to sregex to specify a :ref:`regex`
in the ignore option.

If you want to have different severities for changes on specific directories, create a 
local rule for it:

.. code-block:: xml 

    <rule id="100345" level="12">
        <if_matched_group>syscheck</if_matched_group>
        <description>Changes to /var/www/htdocs – Critical file!</description>
        <match>/var/www/htdocs</match>
    </rule>

In the above example, we created a rule to alert with high severity (12) on change to the htdocs.

Real time Monitoring
--------------------

OSSEC supports realtime (continuous) file integrity monitoring on Linux (kernels 2.6) 
and Windows systems.

The configuration is very simple. In the <directories> option where you specify what 
files or directories to monitor, you just need to add the realtime=”yes” attribute. 
For example:

.. code-block:: xml 

    <syscheck>
        <directories realtime="yes" check_all="yes">/etc,/usr/bin,/usr/sbin</directories>
        <directories check_all="yes">/bin,/sbin</directories>
    </syscheck>

In this case, the directories /etc/, /usr/bin and /usr/sbin will be monitored in real time. The 
same applies to Windows too. 

.. warning:: 

    The real time monitoring will not start right away. First ossec needs to scan the 
    file system and adds each sub-directory to the realtime queue. It can take up to 
    30 minutes for that (wait for the log "ossec-syscheckd: INFO: Starting real time 
    file monitoring" ).

.. note:: 

    Real time only works with directories, not individual files. So you can monitor the /etc 
    or C:\program files directory, but not an individual file like /etc/file.txt.

.. include:: ../faq/syscheck.rst