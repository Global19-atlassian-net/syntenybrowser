# JAX Synteny Browser
An interactive web-based conserved synteny browser application, The Jackson Laboratory (JAX) Synteny Browser. The browser 
allows researchers to highlight or selectively display genome features in the reference and/or the comparison genomes 
based on the biological attributes of the features. The current implementation for the browser supports the reference 
genomes of the laboratory mouse and human.

There is a live, working version of Synteny Browser available at: [syntenybrowser.jax.org](http://syntenybrowser.jax.org/)

User documentation can be found [here](http://syntenybrowser.jax.org/static/docs/SB-UserManual_v1.pdf).

# Setting up/Running Synteny Browser Locally
### Prerequisites
*Note: if you are running Windows some of the commands below might need to be altered* Before starting the setup process,
you'll need:

1. A bash terminal (Mac OS X & Linux will have this included) or a way of running shell scripts
2. A version of Python installed on your machine
3. The `pip` Python library installed on your machine (your version of Python might have Pip included by default, but if
not, you'll have to install it manually)

Assuming you have all of the above items, you'll need a Python library called Virtualenv which will allow you to run
Python scripts in isolated environments that can have their own dependencies, versions, and permissions without messing
with those belonging to your machine. To set up Virtualenv open up a bash and navigate to the root `syntenybrowser/`
directory (all of the following commands are run from this directory unless otherwise noted) and install Virtualenv:

    pip install virtualenv
    
*Note: if you're running Python 3, you may have to run `pip3 install virtualenv`.*


### Getting a Database
Once Virtualenv is installed, you'll need a database. To do this, you have two options:

#### Option 1: Download a preloaded database
A ready-made database is available from Box [here](https://thejacksonlaboratory.box.com/s/i7ru2r9mx2dmzx5m0mbb5w80l6ovd6az)
named 'syntenybrowser-db.zip' and, when decompressed, will yield a file named 'synteny.db'. **This .db file will need to be
located in the root `syntenybrowser/` directory before running the application, otherwise the application will not run.**

#### Option 2: Load a database yourself
*(if you went with Option 1, skip to 'Setting Up the Application')* To load your own database, you'll need a virtual
environment that runs in Python3.6:

    virtualenv venv-db -p python3.6

Once created, activate the virtual environment:

    . venv-db/bin/activate

Install necessary packages:

    pip install -r requirements.txt

Run the database creation script with the required parameter:

    ./create_database.sh synteny.db

*Note: we have found that one of the scripts that queries data from an API can run into issues if you are using a VPN*
This will take several minutes and when it's finished, it will yield a file named 'synteny.db' in root `syntenybrowser/`
directory (the database file needs to be located here so don't move it). Shut down the `venv-db` virtual environment:

    deactivate


### Setting Up the Application
Next, you'll need to get the application running using your new database (if you're at this step and haven't gotten a
database using one of the two available options listed above, you'll need to do that first). To do this, we'll need a
separate virtual environment that runs in Python2.7:

    virtualenv venv-app -p python2.7
    
Once created, activate the virtual environment:

    . venv-app/bin/activate
    
Install necessary packages:
    
    pip install -r requirements.txt


### Running the Application
Make sure the the application virtual environment is running. If it isn't, start it up (if it is, skip to the next step):

    . venv-app/bin/activate

Run the application:

    python runserver.py

When finished, shut down the virtual environment:

    deactivate


# Running the Synteny Browser from the Docker Image
### Prerequisites
1. A bash terminal (Mac OS X & Linux will have this included) or a way of running shell scripts
2. Docker installed on your machine 

### Pull the image
Start docker on your machine and once running, pull the image using

    docker pull lamoua/synbrowser

Once the image is done pulling from DockerHub, run the container

    docker run -p 5001:5001 synbrowser:latest

This should set off the container as well as start the Python Flask server. Navigating to the specified location (which should be localhost:5001 by default), should bring you to the JAX Synteny Browser interface running from the container. 


## Citation
**The JAX Synteny Browser for Mouse-Human Comparative Genomics.**

Manuscript in review

## License
The JAX Synteny Browser is provided under the license found [here](LICENSE.md).
