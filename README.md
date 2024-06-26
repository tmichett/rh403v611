# rh403v611
Red Hat Satellite Administration - v 6.11


NOTE: At this time, only the Labs have been tested for CH1, CH2, CH3, CH4, CH9_Image_Ansible_Prep.yml (Good enough for passing grading, but ugly playbook). No GE testing has been completed (except as otherwise specified).

Setup Collections and Prepare the system
```
[student@workstation rh403v611]$ cd Ansible/Demo_Prep/

[student@workstation Demo_Prep]$ ansible-playbook SystemSetup.yml

[student@workstation Ansible]$ ansible-galaxy collections install -r collections/requirements.yml -p collections/
```

## Chapter 1

Need to run both **lab start* commands to leverage the playbooks.

```
lab start deploy-manifest
lab start deploy-review
```

**Running Playbooks**

Guided Exercise: Configure Organization and Content Manifests

```
ansible-playbook CH1_GE_deploy-manifest.yml
```

LAB: Plan and Deploy Red Hat Satellite

```
ansible-playbook CH1_Lab.yml
```

Can grade the lab after running playbook with

```
[student@workstation Ansible]$ lab grade deploy-review
```


## Chapter 2

**GE: Publish and Promote Content Views**
```
ansible-playbook CH2_GE_lifecycle-sync.yml
```


Need to run both **lab start* commands to leverage the playbooks.

**GE: Synchronize Red Hat Content**
```
lab start  lifecycles-create

ansible-playbook CH2_GE_lifecycles-create.yml
```

**GE: Publish and Promote Content Views**
```
lab start lifecycles-publish

ansible-playbook CH2_GE_lifecycles-publish.yml
```

**LAB: Manage Software Lifecycles**
```
ansible-playbook CH2_Lab.yml
lab grade lifecycles-review
```

## Chapter 3

GE playbooks in progress


**LAB: Register Hosts**
```
ansible-playbook CH3_Lab.yml
lab grade clients-review
```

## Chapter 4

GE playbooks (TBD)


**LAB: Deploy Software to Hosts**
```
ansible-playbook CH4_Lab.yml
lab grade software-review
```

## Chapter 5

**REPO Discovery**

https://packages.microsoft.com/yumrepos/edge/

https://packages.microsoft.com/yumrepos/  **Way more extensive list**

http://download1.rpmfusion.org/free/fedora/releases/40/   **For Fedora 40**


## Chapter 10

Before Demo run the Install JQ Playbook
```
CH10_Install_JQ.yml
```

**API Demo**

Commands are in the txt file **API_Commands.txt**

List hosts by Name
```
curl --request GET --user admin:redhat https://satellite.lab.example.com/api/v2/hosts | jq | grep '"name":'
```

List Orgs by Name
```
curl --request GET --user admin:redhat https://satellite.lab.example.com/api/v2/organizations | jq | grep '"name":'
```

Fancy JSON with JQ list hosts by name and ignore certificate with **-k** option
```
curl -k --request GET --user admin:redhat https://satellite.lab.example.com/api/v2/organizations | jq '.results[] | {name}'
```

Plus many more ...

There is also a playbook demo here showing the Ansible URI Module to leverage the API

List Orgs by Name
```
ansible-playbook CH10_API_Demo.yml
```

**Ansible Demo**

In order to use all the playbook features, the Ansible Satellite Collection and modules need installed as well as the python-jmespath package.

```
sudo -i dnf install python-jmespath
```

```
ansible-playbook CH10_Ansible_Org_Demo.yml
```
