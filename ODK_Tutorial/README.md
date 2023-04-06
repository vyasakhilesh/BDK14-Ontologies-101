# ODK Tutorial

### Setting up ODK in Linux
```bash
# One time Step
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
sh seed-via-docker.sh -c -C cato-odk.yaml --outdir ../../odk_sample_repo
sudo chown -R <usrname> target
sudo chmod -R 775 target

# repo will be created under follow the instruction in the end of the command

####
NEXT STEPS:
 0. Examine target/cato and check it meets your expectations. If not blow it away and start again
 1. Go to: https://github.com/new
 2. The owner MUST be <username>. The Repository name MUST be odk_sample_repo
 3. Do not initialize with a README (you already have one)
 4. Click Create
 5. See the section under '…or push an existing repository from the command line'
    E.g.:
cd target/cato
git remote add origin git@github.com:<username>/odk_sample_repo.git
git branch -M main

git push -u origin main
```











