# MISP-Maltego User Guide

This user guide should help you through the installation of **MISP-Maltego**, and should guide you how to use it through a few use-cases. As this is a collaborative project, do not hesitate to propose changes, write other use-cases or raise [feature requests](https://github.com/MISP/MISP-maltego/issues) for missing features.

## Installation
These instructions have been tested on Ubuntu 18.04 LTS, but should be similar on other systems.
1. Download and install [Maltego](https://www.paterva.com/web7/downloads.php)
2. Install dependencies:  `sudo apt install git build-essential python3-setuptools python3-dev python3-pip`
3. Clone the repository, install and create the Maltego local transform bundle.
   To the question *".canari/canari.conf already exists, would you like to overwrite it?"* you will probably want to answer yes.
```
git clone https://github.com/MISP/MISP-maltego.git
cd MISP-maltego
sudo pip3 install .
canari create-profile MISP_maltego
```
5. Import this bundle in Maltego. 
   1. Open Maltego
   2. Click on the home button (Maltego icon, top-left corner).
   3. Click on 'Import'
   4. Click on 'Import Configuration'.
   5. Load the `MISP_maltego.mtz` file and follow the prompts.
6. Edit `$HOME/.canari/MISP_maltego.conf` and enter your `misp_url` and `misp_key`

## Custom Entities
MISP-Maltego tries to use as much as possible the default Paterva entities, or the most popular from the community. It however comes with a few custom entities: 
* **MISPEvent**: A representation of an *Event* on MISP, containing *Attributes* (MISP) / *Entities* (Maltego)
* **MISPObject**: A way to group associated attributes in a structured way.
* **MISPGalaxy**: A *Tag* containing much more metadata. Please refer to the [MISP Galaxy
](https://github.com/MISP/misp-galaxy) for more information. **MITRE ATT&CK** is for example completely available through MISPGalaxy entities (see use-cases for an example)

# Use Cases
## Transform on existing data
In this use case we will be using already existing entities and will initiate a transform using MISP. The currently supported entities are: `AS`, `DNSName`, `Domain`, `EmailAddress`, `File`, `Hash`, `IPv4Address`, `NSRecord`, `Person`, `PhoneNumber`, `URL`, `Website`.

Example:
* create an entity `domain` with the value `1dnscontrol.com`.
* right click and choose *Local Transforms*  > *MISP_maltego* > *Domain To Event*  
![animated screenshot](https://raw.githubusercontent.com/MISP/MISP-maltego/master/doc/img/usecase1-transform.gif)
* continue loading transforms on the *MISP Event*

## Transform from MISP Event ID
While MISP already has a graphing capability we would like to use the power of Maltego to look at the data and expand the work.
* create a *MISP Event* and give it an `event id`, or `UUID`
* One **manual** way is to right click and choose *Local Transforms* > *MISP_maltego* > *Event To Attributes* 
  * Notice the event is transformed to *Attributes*, *Objects*, *Tags*, *Galaxies* and related *MISP Events*
  * You can now further transform on an *Object* > *Object To Attributes* and see the content of the object
![machine transforms](https://raw.githubusercontent.com/MISP/MISP-maltego/master/doc/img/usecase2-manual.gif)
* Alternatively you can also use the **Maltego Machine** to speed up things. 
   * Click on the *MISP Event* and in the left menu choose *Event to All* in the *Machines* section. 
![machine transforms](https://raw.githubusercontent.com/MISP/MISP-maltego/master/doc/img/usecase2-machine-menu.png)
   * Notice that the whole event, objects and such will get expanded with data from your MISP instance.
![animated screenshot](https://raw.githubusercontent.com/MISP/MISP-maltego/master/doc/img/usecase2-machine.gif)
* You can now further transform on any data.

## Which data is already in MISP?
If you use MISP as central database it can be quite convenient to know which data is present in MISP, and which data is not; especially after using a number of other transforms.
To permit this MISP-Maltego will always add a green bookmark to all the data that is present in MISP.
![green bookmark](https://raw.githubusercontent.com/MISP/MISP-maltego/master/doc/img/usecase3-bookmark.png)


## Transform from Galaxy
TODO
## Visualise MITRE ATT&CK
TODO