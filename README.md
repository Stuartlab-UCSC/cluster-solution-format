# cluster-solution-format
This repo contains a draft specification of a json schema for cluster solutions created from single cell mRNA seq data. 
A cluster solution is loosely defined as the output of any clustering algorithm, e.g. louvain, k-means, or more domain 
specific algorithms such as SC3.  

The schema mirrors this data model:

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Data Model")


Along with metadata about the cluster solution, 3 major types of information can detail each cluster.
	
  * cell assignments: The categorical (or probabalistic) assignment of cells to clusters, i.e. the output of a cluster algorithm.
  *	markers: Gene markers for identifying individual clusters.
  *	cell type annotaion: A label that maps a cluster to a cell type.  

Cell assignments is the only type of information required for a valid cluster solution json object.

#### Some thoughts on other options for formats:

The three main formats that spring to mind are a json specification as represented here, .csv or .tsv files, and loom 
and other matrix annotation files.
 
The advantage of tab or comma seperated value files seems to be their ease and readiness to be pulled into analysis 
pipelines. Where these formats fail is the ability to track important metadata about the cluster solution, e.g. the 
algorithm that produced the cluster solution.

Other matrix file formats such as loom or more language specific formats such as Seurat and Scanpy objects are also 
easily integrated into analysis. While these formats are more general and can carry metadata for cluster solutions they 
are currently lacking standards to document and validate their schemas. Understanding the schema of Loom, Scanpy, or 
Suerat requires reading objects into memory and manually investigating their annotation fields. These types of objects 
are very good at "it just works" analysis pipelines, but problems with interoperability commonly arise due to a lack of 
standardization in their structure.

While json provides modeling of metadata and standards for documenting and validating the schemas, it requires knowledge
of the schema to transform the information into data structures ready for comparative analysis and visualization. This 
deficit is easy to code around as libraries for parsing the json into analysis structures can be written and tested with
relative ease.

A best of both worlds solution could implement something similar to [this effort to standardize the mapping of 
cell annotations to ontology terms](https://github.com/HumanCellAtlas/matrix_semantic_map). It gives an example of 
 integration between a well defined json schema loom files.

