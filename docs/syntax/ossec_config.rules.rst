
.. object:: include 

    Load a single rule file.  

    **Allowes:** Path and file name of rule to load example: rules/config.xml 

        
.. object:: rule 

    
    Load a single rule file.  

    **Allowes:** Path and file name of rule to load example: rules/config.xml 

    .. note:: 

        This is the same as include, but created to keep the syntax constant with 
        other sections of the rules config. 

.. object:: rule_dir 

    Load a directory of rules.  The order of loaded files will be in alphebics order 
    and will not load any files that have been loaded before. 

    **Attributes:** 
    
    - *pattern*: is a regex match string use to detemine if a file needs to be 
      loaded. 
        
        - *Defaults*: regex "_rules.xml$" is used unless another one is specified. 
      
    **Allowes:** Path to a directoy of rule files 

    **Example:**

    #. Loading all rules in directory /var/ossec/rules ending ending with _rules.xml 
        
        .. code-block:: xml 
            
            <ossec_config>
                <rules>
                    <rules_dir>rules</rules_dir>
                </rules>
            </ossec_config>

    #. Loading all rules in directory /var/ossec/rules/plugins ending with .xml 

        .. code-block:: xml 
            
            <ossec_config>
                <rules>
                    <rule_dir pattern=".xml$">rules</rule_dir>
                </rules>
            </ossec_config>

.. object:: decoder 

    Load a single decoder file.  
    
    .. note:: 

        If no decoders are spcified in ossec.conf the lagacy etc/decoder.xml and 
        etc/local_decoder.xml are loaded

    **Allowes:** Path and file name of decoder to load example: rules/decoder/decoder.xml 


.. object:: decoder_dir 

    Load a directory of decoders.  The order of loaded files will be in alphebics order 
    and will not load any files that have been loaded before. 

    **Attributes:** 
    
    - *pattern*: is a regex match string use to detemine if a file needs to be 
      loaded. 
        
        - *Defaults*: regex "_decoder.xml$" is used unless another one is specified. 
      
    **Allowes:** Path to a directoy of decoder files 

    **Example:**

    #. Loading all decoders in directory /var/ossec/rules ending ending with _decoder.xml 
        
        .. code-block:: xml 
            
            <ossec_config>
                <rules>
                    <decoder_dir>rules</decoder_dir>
                </rules>
            </ossec_config>

    #. Loading all decoders in directory /var/ossec/rules/plugins/plugins/decoders 
       ending with .xml 

        .. code-block:: xml 
            
            <ossec_config>
                <rules>
                    <decoder_dir pattern=".xml$">rules/plugins/decoders</decoder_dir>
                </rules>
            </ossec_config>

.. object:: list  

    Load a single cdb refences for inclusion by other rules.  

    .. note:: 

        Due to the way cdb files are compiled using tmp files by the `ossec-makelists` 
        program the file extenstion should not be include in this directive.  ossec's 
        tools will correct append the correct .cdb or .txt extenstion as needed. 

    **Allowes:** Path to a list file to be loaded and compiled. 


