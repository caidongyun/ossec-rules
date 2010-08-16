
Configuring MySQL
-----------------

Database Setup 
^^^^^^^^^^^^^^

Create a database, setup the database user, and add the schema with the following 
commands. 

.. code-block:: console 

    # mysql -u root -p

    mysql> create database ossec;

    mysql> grant INSERT,SELECT,UPDATE,CREATE,DELETE,EXECUTE on ossec.* to ossecuser@<ossec ip>;
    Query OK, 0 rows affected (0.00 sec)

    mysql> set password for ossecuser@<ossec ip>=PASSWORD('ossecpass');
    Query OK, 0 rows affected (0.00 sec)

    mysql> flush privileges;
    Query OK, 0 rows affected (0.00 sec)

    mysql> quit


    # wget http://www.ossec.net/files/other/mysql.schema

    # mysql -u root -p ossec < mysql.schema 


OSSEC Setup 
^^^^^^^^^^^

Inorder for ossec to output alerts and other data into the database the 
/var/ossec/etc/ossec.conf will need to be updated and have the <database_output> 
section completed.  

.. code-block:: xml

    <ossec_config>
        <database_output>
            <hostname>192.168.2.30</hostname>
            <username>ossecuser</username>
            <password>ossecpass</password>
            <database>ossec</database>
            <type>mysql</type>
        </database_output>
    </ossec_config>

The values will need to be corrected for your installations hostname, user, password, and 
database.  

Complete MySQL Output 
^^^^^^^^^^^^^^^^^^^^^ 

All that is left is to restart ossec for the changes to take effect. 

.. code-block:: console 

    # /var/ossec/bin/ossec-control restart 



