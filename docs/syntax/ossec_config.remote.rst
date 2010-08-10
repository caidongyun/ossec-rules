.. object:: connection 

    Specify the type of connection being enabled: secure or using syslog.

    **Default:** secure 

    **Allowed:** secure/syslog 

.. object:: port 

    Specifies the port to listen for events.

    **Default:**

    - 1514: if connection is set to `secure` 
    - 514: if connection is set to `syslog`

    **Allowed:** Any port number from 1 to 65535

.. object:: allowed-ips 

    List of IP addresses that are allowed to send syslog messages to the server (one per element).

    **Allowed:** Any IP address or network 

.. object:: deny-ips 

    List of IP addresses that are not allowed to send syslog messages to the server(one per element).

    **Allowed:** Any IP address or network 

.. object:: local_ip 
    
    Local ip address to listen for connections.

    **Default:** all interfaces

    **Allowed:** Any internal ip address
