## Summary
TBD  

## Requirements:
- Python2.7
- Python-pip package manager
- virtualenv
- [HPE OneView SDK for Python](https://github.com/HewlettPackard/python-hpOneView#installation)
- [Anbile for OneView Setup](https://github.com/HewlettPackard/oneview-ansible#setup)

> **_NOTE:_** According to the [Control Node Requirements](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements) in the Ansible documentation, Window is not supported for Ansible.
## Environment Setup
It's recommended to spin up a Python virutal environment and install the Python package there, so the setup won't pollute the global space. The following commands creates and starts a *Python 2.7* virutal environment, named *ansible-env-python27*, with *virutalenv*:
```
$ virtualenv --python=/usr/bin/python ansible-env-python27
$ source ansible-env-python27/bin/activate
```
Install Python packages listed in *requirements.txt*:
```
(ansible-env-python27)$ pip install -r requirements.txt
```
> **_NOTE:_** Both Python and Python-pip can be installed from the Linux OS pakcage manager, such as apt-get and yum. Virtualenv can be installed from Pip. 

Set environment variables for OneView:
```
(ansible-env-python27)$ export ONEVIEWSDK_IP="192.168.0.1"
(ansible-env-python27)$ export ONEVIEWSDK_USERNAME='admin123'
(ansible-env-python27)$ export ONEVIEWSDK_PASSWORD='Password123'
(ansible-env-python27)$ export ONEVIEWSDK_API_VERSION=800
```
Edit in the **settings.csv** to match to your target ESXi host, and to your target OneView environment. These pertain to creating server profiles in OneView using server profile templates, designated server hardwares, networkings, and OS deployment plans with custom attributes.
> **_NOTE:_** An ESXi deployment plan requires specifying the *network_set_name*, *connectionid*, and *serverhardware* in its custom attributes. 

When ready, run *ov_ESXi_server_profile_loop.yml* playbook. The -vvv flag enables the verbose mode.
```
(ansible-env-python27)$ ansible-playbook ov_ESXi_server_profile_loop.yml -vvv
```
A successful run returns a *changed=1* in *PLAY RECAP*.
```
PLAY RECAP **************************************************************************************
*localhost: ok=5    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
