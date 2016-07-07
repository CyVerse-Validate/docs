**********************************************
Running Validate on Syngenta_heldback data set
**********************************************
--------------------------
Install Cyverse CLI tools
--------------------------

Accessing Validate through the Agave API hugely streamlines the task of managing your data and accessing applications through the Cyverse Data Store with a variety of command-line tools. For a comprehensive overview please see the full documentation `here <https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk`

Download Agave API::
    
    git clone https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk.git

Change directory into the downloaded repository and unpack the cli tools::
   
    cd cyverse-sdk
    tar xf cyverse-cli.tgz

Add the cli tools to your home directory and bash profile::
    
    mv cyverse-cli $HOME
    echo "PATH=\$PATH:\$HOME/cyverse-cli/bin" >> ~/.bashrc
    source ~/.bashrc

(note that on a Macintosh system your default profile may be .bash_profile)

Initialise the CLI tools::

    tenants-init -t iplantc.org

Create an OAAuth client application with API keys::
    
    clients-create -S -v -N my_client -D "Client used for app development"

Where -S saves the keys for future use, -D provides a brief description, and -N is your application name.

You will be asked to enter your CyVerse account information::
    
    auth-tokens-create -S

At this point::
    
    apps-list

should return a list of all publicly-available apps.






