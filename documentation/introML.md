# Intro to Machine Learning (ML) for High Energy Physics

## Setup and running

As a first introduction to what CMS is doing with ML, it is strongly recommended to follow the CMSDAS tutorial. [Link](https://indico.cern.ch/event/1088671/timetable/#90-period-5-short-exercise-mac).

_I suggest you to watch the [lecture](https://indico.cern.ch/event/1088671/contributions/4577023/attachments/2330165/4045725/GMT20220104-211221_Recording_1920x1120.mp4) and follow the [slides](https://indico.cern.ch/event/1088671/contributions/4577023/attachments/2330165/4045705/CMSDAS2021_ML_04Jan2022.pdf)._

As a **first step** towards getting used to ML tools, I suggest you to use the CMSDAS material in the [CERN SWAN](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi1z8vfuMn7AhWSm2oFHShpDL4QFnoECA0QAQ&url=https%3A%2F%2Fswan.cern.ch%2F&usg=AOvVaw3NDWvDkT5W57BkQ8-V3xGq). SWAN is a hub created at CERN with many tools needed for CERN data analysis. For more information about SWAN follow [this link](https://swan.docs.cern.ch/intro/what_is/). Contact me if you dont have access to SWAN.

In SWAN you will be asked about the environment you need to create, at this moment you can use the default settings and click on ```Start my Session```.

<img src="https://codimd.web.cern.ch/uploads/upload_734ab2206b1d5c9222fd4faf5282260d.png" alt="drawing" width="400"/>


Once you access your SWAN projects, you can include directly github repositories by click on the button next to the plus button.

<img src="https://codimd.web.cern.ch/uploads/upload_094a01da472ebfa750df5aa0411369ac.png" alt="drawing" width="400"/>

There you can add the github link `https://github.com/FNALLPC/machine-learning-das.git` from the [repository](https://github.com/FNALLPC/machine-learning-das). After this, you will have all the jupiter notebooks in SWAN ready to run. You must start with the `0-setup-libraries.ipynb` notebook, which it will create the environment you need for the rest of the notebooks.

Jupyter notebooks are a wonderful tool to teach and to learn coding. However, since you have working code there, it is easy just to run it once and do not understand what the code is doing. I strongly suggest you to take your time to see what the example is doing. Literally play as much as you can with it.

## Some known issues

### 3.1-dense-pytorch.ipynb

This notebook is *optional*, you can continue to notebook 4 without loosing any major information.
If you have a problem with `import torch`, you need to modify the first cell. From:
```
!{sys.executable} -m pip install torch torchvision root_pandas --user
```
to
```
!{sys.executable} -m pip install torch --user
```
Then you can run it without problems.

### 3.2-dense-bayesian-optimization.ipynb

This notebook relies on the `skopt` package, which is recommended to use with `python3`. The current environment has `python2.7`. We can fix this issue, but for now it is not necessary.

### 4-preprocessing.ipynb

#### Notebook restarts after running

This only means that you might need to change your environment. Go back to your main SWAN folder and in the top right, click on the three dots. There, find the option `change configuration`, which it will bring you back to the settings. In my test, it work perfectly with 16 Gb.

#### Downloading files
In this notebook, you need to access some files that exist only in the CERN storage area. For that you need to set your certificate in lxplus. If you have never installed your certificate in lxplus, please follow [this instructions](https://ca.cern.ch/ca/Help/?kbid=024010).

Then, in lxplus, run:
```
voms-proxy-init -rfc -voms cms --valid 168:00
```
it will print a message containing some information and a line that looks like this:
```
Created proxy in /tmp/x509up_u99999.
```
These file contains a certificate that you need to copy to your cernbox. To do that, run:
```
cp -p /tmp/x509up_u99999 /eos/user/X/USER/tmp/x509up_u15148
```
where `X` and `USER` depends on *YOUR* user. For instance if your cern user is agomez then `X=a` and `USER=agomez`.

Then in the notebook `4-preprocessing.ipynb`, in the first cell right after `import numpy as np`, copy:

```
##### REMEMBER TO MANUALLY COPY THE PROXY TO YOUR CERNBOX FOLDER AND TO MODIFY THE NEXT LINE
import os
os.environ['X509_USER_PROXY'] = '/eos/home-X/USER/tmp/x509up_u99999'
if os.path.isfile(os.environ['X509_USER_PROXY']): pass
else: print("os.environ['X509_USER_PROXY'] ",os.environ['X509_USER_PROXY'])
os.environ['X509_CERT_DIR'] = '/cvmfs/cms.cern.ch/grid/etc/grid-security/certificates'
os.environ['X509_VOMS_DIR'] = '/cvmfs/cms.cern.ch/grid/etc/grid-security/vomsdir'
```
where `X` and `USER` follows the same notation as before.

Once you properly modify this line, you can run it once because it will download many files needed and it will take a lot of time.

If you have any technical problem, dont hesitate on contacting me on mattermost.

**More to come**
