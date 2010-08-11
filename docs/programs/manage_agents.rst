
.. _manage_agents:

manage_agents
=============

manage_agents is available in two versions:

-a version for OSSEC server installations
-a version for OSSEC agent installations

The purpose of manage_agents is to provide an easy-to-use interface to handle authentication keys for OSSEC agents. These authentication keys are required for secure (encrypted and authenticated) communication between the OSSEC server and its affiliated agent instances.

To add an agent to a server with manage_agents you need to follow the steps below.

1. Run manage_agents on the OSSEC server.
2. Add an agent.
3. Extract the key for the agent.
4. Copy that key to the agent.
5. Run manage_agents on the agent.
6. Import the key copied from the server.
7. Restart the OSSEC server.
8. Start the agent.


manage_agents on OSSEC servers
------------------------------

The server version provides an interface to

- add an OSSEC agent to the OSSEC server
- extract the key for an agent already added to the OSSEC server
- remove an agent from the OSSEC server
- list all agents already added to the OSSEC server.

Running manage_agents and start screen
======================================

To run manage_agents, you have to execute the following command on the OSSEC server as a user with appropriate privileagues (e.g. root):

.. code-block:: console

    # /var/ossec/bin/manage_agents

After that, you see the start screen:

.. code-block:: console

    ****************************************
    * OSSEC HIDS v2.5-SNP-100809 Agent manager.     *
    * The following options are available: *
    ****************************************
       (A)dd an agent (A).
       (E)xtract key for an agent (E).
       (L)ist already added agents (L).
       (R)emove an agent (R).
       (Q)uit.
    Choose your action: A,E,L,R or Q:

You can now choose one of the actions.

Adding an agent
===============

To add an agent type A in the start screen:

.. code-block:: console

    Choose your action: A,E,L,R or Q: a

You are then asked to provide a name for the agent to be added.
This can for example be the hostname. In this example the agent name will be agent1.

.. code-block:: console

    - Adding a new agent (use '\q' to return to the main menu).
      Please provide the following:
       * A name for the new agent: agent1

After that you have to specify the IP adress for the agent. This can either be a single IP adress (e.g. 192.168.1.25) or a range of IPs (e.g. 192.168.2.0/24). The latter way is preferrable if the IP of the agent will change a lot, e.g. by being assigned a new IP via DHCP after each boot.

.. code-block:: console

       * The IP Address of the new agent: 192.168.2.0/24

The last information you will be asked for is the ID you want to assign to the agent. manage_agents will suggest a value for the ID to you. This value is the lowest positive number that is not already assigned to another agent. The ID 000 is assigned to the OSSEC server. To accept the suggestion, simply press ENTER. To choose another value, type it in and press ENTER.

.. code-block:: console

       * An ID for the new agent[001]:

Now you have to confirm adding the agent and you are done with this step.

.. code-block:: console
    Agent information:
       ID:002
       Name:agent1
       IP Address:192.168.2.0/24

    Confirm adding it?(y/n): y
    Agent added.

After that manage_agents appends the agent information to /var/ossec/etc/client.keys and goes back to the start screen.


Extracting the key for an agent
===============================

After adding an agent, a key for the agent is created that has to be copied to the agent. To get the key, use the E option in the manage_agents start screen. You will be given a list of all agents already added to the server. To extract the key for an agent, simply type in the ID of the respective agent. It is important to note that you have to enter all digits of the ID.

.. code-block:: console

    Choose your action: A,E,L,R or Q: e

    Available agents: 
       ID: 001, Name: agent1, IP: 192.168.2.0/24
    Provide the ID of the agent to extract the key (or '\q' to quit): 001

    Agent key information for '001' is: 
    MDAyIGFnZW50MSAxOTIuMTY4LjIuMC8yNCBlNmY3N2RiMTdmMTJjZGRmZjg5YzA4ZDk5MmQ4NDE4MjYwMjJkN2ZkMzNkYzZiOWE5NWY4MzU5YWRlY2JkY2Rm

    ** Press ENTER to return to the main menu.

You can now copy that key to the agent1 and import it there via the agent version of manage_agents.

Removing an agent
=================

If you want to detach an OSSEC agent from the server, use the R option in the manage_agents start screen. You will be given a list of all agents already added to the server. To remove an agent, simply type in the ID of the respective agent, press enter and confirm the deletion. It is important to note that you have to enter all digits of the ID.

.. code-block:: console

    Choose your action: A,E,L,R or Q: e

    Available agents: 
       ID: 001, Name: agent1, IP: 192.168.2.0/24
    Provide the ID of the agent to extract the key (or '\q' to quit): 001
    Confirm deleting it?(y/n): y
    Agent '001' removed.

Afterwards the agent information manage_agents invalidates the agent information in /var/ossec/etc/client.keys. Only the values for ID and the key are still being stored to avoid conflicts when adding other agents later. The deleted agent can no longer communicate with the OSSEC server.


manage_agents on OSSEC agents
------------------------------

The agent version provides an interface for importing authentication keys.

.. code-block:: console

    ****************************************
    * OSSEC HIDS v2.5-SNP-100809 Agent manager.     *
    * The following options are available: *
    ****************************************
       (I)mport key from the server (I).
       (Q)uit.
    Choose your action: I or Q: i

    * Provide the Key generated by the server.
    * The best approach is to cut and paste it.
    *** OBS: Do not include spaces or new lines.

    Paste it here (or '\q' to quit): [key extracted via manage_agents on the server]

    Agent information:
       ID:001
       Name:agent1
       IP Address:192.168.2.0/24

    Confirm adding it?(y/n): y
    Added.
    ** Press ENTER to return to the main menu.


After that you can quit manage_agents. For the changes to be in effect you have to restart the server and start the agent.


