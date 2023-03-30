## [Robot Tutorial](https://oboacademy.github.io/obook/tutorial/robot-tutorial-1/)

```bash
# Install docker
# Note: Execute this command only once
docker pull obolibrary/robot
# Set working directory and run bash
docker run -v $PWD/:/work -w /work --rm -ti obolibrary/robot bash
# check robot version
robot --version

# convert owl file into ttl
cd /work/Robot_Tutorial/basic-subclass
robot convert --input chromosome-parts.owl --format ttl --output chromosome-parts.ttl

# Extract subset of an ontology - Upper part Ontology of chromosome having id GO:0005694
# id is extracted using protege
robot extract --method MIREOT --input chromosome-parts.owl --lower-term GO:0005694 --output chromosome-full.owl

# Extraction between lower (chromosome id GO:0005694) and upper part (organelle id GO:0043226)
robot extract --method MIREOT \
  --input chromosome-parts.owl \
  --lower-term GO:0005694 \
  --upper-term GO:0043226 \
  --output chromosome.owl

# convert spreadsheet into OWL ontologies using template strings
robot template --template animals.tsv --output animals.owl

# Convert spreadsheet and getting reference with previous one
robot template --input animals.owl --template animals2.tsv --output animals2.owl

# Note:  Protege Importing an ontology without an IRI into another ontology without an IRI can cause some problems

# Annotating animal ontology with ontology-IRI
robot annotate --input animals.owl \
  --ontology-iri http://example.com/animals.owl \
  --output animals_ann.owl

robot annotate --input animals2.owl \
  --ontology-iri http://example.com/animals2.owl \
  --output animals2_ann.owl

# Adding Version IRI
robot annotate --input animals_ann.owl \
  --version-iri http://example.com/animals/2023-03-30/animals.owl \
  --output animals_ann_ver.owl

robot annotate --input animals2_ann.owl \
  --version-iri http://example.com/animals/2023-03-30/animals2.owl \
  --output animals2_ann_ver.owl

# Adding more metadata title, description and license to ontology
robot annotate --input animals_ann_ver.owl \
  --annotation dc11:title "Animal Ontology" \
  --annotation dc11:description "An ontology about animals" \
  --link-annotation dc:license https://creativecommons.org/licenses/by/4.0/ \
  --output animals_ann_ver_meta.owl

robot annotate --input animals2_ann_ver.owl \
  --annotation dc11:title "Animal Ontology" \
  --annotation dc11:description "An ontology about animals" \
  --link-annotation dc:license https://creativecommons.org/licenses/by/4.0/ \
  --output animals2_ann_ver_meta.owl

# Merging two separate files or merging all imports into current ontology file
cp animals_ann_ver_meta.owl animals-new.owl
cp animals2_ann_ver_meta.owl animals2-new.owl
robot merge --input animals.owl --input animals-new.owl --output animals-full.owl

robot merge --input animals2-new.owl --collapse-import-closure true --output animals-full-2.owl

# Note: animals-full.owl and animals-full-2.owl should same

# Reason
cd /work/Robot_Tutorial/basic-classification
cp ubiq-ligase-complex.owl unreasoned.owl
# Note: Edit and save unreasoned.owl using below steps in Protege
# 1. Find 'organelle' in the class hierarchy below 'cellular_component' (or just search for it by label)
# 2. Make 'organelle' disjoint with 'organelle part' (either use the class hierarchy or type it in the expression editor)
# 3. Find 'intracellular organelle part' below 'intracellular part' or 'organelle part' (or search for it by label)
# 4. Add 'organelle' as a parent class to 'intracellular organelle part' (remember that you only need to include the single quotes if the label has spaces)
robot reason --input unreasoned.owl --reasoner ELK --output unsatisfiable.owl
# In final output only upper terms of class 'intracellular organelle part' is included - asserted as owl:Nothing

# Reason on orginal file
robot reason --input ubiq-ligase-complex.owl --output reasoned.owl

# Diff - formats - plain, pretty, html, markdown
robot diff --left ubiq-ligase-complex.owl \
  --right reasoned.owl \
  --format html \
  --output diff.html

# Quality Control with Robot --Todo

# Generate SpARQL Table reports with Robot


```