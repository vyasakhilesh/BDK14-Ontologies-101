## BD2K Open Educational Resources: BDK14 Ontologies 101

**Introduction to OWL2 and data reasoning**

**Contributors:** Nicole Vasilevsky, Melissa Haendel, Chris Mungall, David Osumi-Sutherland, Matt Yoder, Carlo Torniai, and Simon Jupp

## Module Objectives:
At the completion of this component, the learner will be able to:
1. Describe logical inference and data classification strategies using ontologies
2. Understand the Web Ontology Language (OWL)
3. How to participate in ontology development communities

**Module Prerequisites:** None

## Module Units
**Unit 1: Controlled Vocabularies, Ontologies, and Data Linking**: Slides: [BDK14-1.pptx](https://github.com/OHSUBD2K/BDK14-Ontologies-101/blob/master/BDK14-1.pptx)

**Unit 2: An Introduction to OWL**: Slides: [BDK14-2.pptx](https://github.com/OHSUBD2K/BDK14-Ontologies-101/blob/master/BDK14-2.pptx)

**Unit 3: Ontology Community**: Slides: [BDK14-3.pptx](https://github.com/OHSUBD2K/BDK14-Ontologies-101/blob/master/BDK14-3.pptx)

**Exercise:**
[Ontology 101 Tutorial](http://ontology101tutorial.readthedocs.io/en/latest/)
Folders:
- basic-classification
- basic-disjoint
- basic-dl-query
- basic-restriction
- basic-subclass
- domain-range
- taxon-union

## [Robot Tutorial](https://oboacademy.github.io/obook/tutorial/robot-tutorial-1/)

**How to run using docker**
```bash
# Install docker
# Note: Execute this command only once
docker pull obolibrary/robot
# Set working directory and run bash
docker run -v $PWD/:/work -w /work --rm -ti obolibrary/robot bash
# check robot version
robot --version

# convert owl file into ttl
cd /work/BDK14_exercises/basic-subclass
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

# Annotating animal ontology with ontology-IRI
robot annotate --input animals2.owl \
  --ontology-iri http://example.com/animals2.owl \
  --output animals2_ann.owl

# Adding Version IRI
robot annotate --input animals_ann_ver.owl \
  --version-iri http://example.com/animals/2023-03-30/animals.owl \
  --output animals_ann_ver.owl
```



**Recommended readings:**
[BDK14_exercises/BDK14_RecommendedReadings.pdf](https://github.com/OHSUBD2K/BDK14-Ontologies-101/blob/master/BDK14_exercises/BDK14_RecommendedReadings.pdf)

## Additional resources

[OBO Tutorial](https://github.com/jamesaoverton/obo-tutorial) (by James Overton): A tutroial for building and using Open Biological and Biomedical Ontologies (OBO).

[Ontology Starter Kit](https://github.com/INCATools/ontology-starter-kit) (by Chris Mungall): Tooling for creating and managing OBO ontologies.

[HPO Workbench](http://hpo-workbench.readthedocs.io/en/latest/): The HPO Workbench is a Java app designed as a browser for the Human Phenotype Ontology (HPO) terms and annotated diseases. HPO Workbench has a series of functions that can be used by collaborators to review and make suggestions for extending, correcting, or otherwise revising the HPO or the disease annotations.

See additional ontology tutuorials and resources [here](https://tislab.org/ontologyResources.html)
