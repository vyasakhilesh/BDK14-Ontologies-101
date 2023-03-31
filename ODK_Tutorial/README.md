# ODK Tutorial

### Setting up ODK in Linux
```bash
docker pull obolibrary/odkfull

# check robot version
mkdir ODK_Tutorial
cd ODK_Tutorial

# download odk.sh
sh odk.sh robot --version

# Access ODK container
sh odk.sh bash
# Or if you have ODK Ontology Repo, run.sh and odk.sh are same 
# sh src/ontology/run.sh bash

# Set memory in case of problem 
# robot_java_args: '-Xmx8G' in odk.sh or src/ontology/run.sh
# or src/ontology/cl-odk.yaml
```

### [Setting up repo](https://oboacademy.github.io/obook/tutorial/setting-up-project-odk/)
Download [Cato-odl.yaml](https://github.com/INCATools/ontology-development-kit/tree/master/configs) basic file for ODK configuration.

### [Generate Repo]
```bash
cd ODK_Tutorial
sh seed-via-docker.sh -c -C cato-odk.yaml

# follow the instruction in the end of the command
```











