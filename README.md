# cluster-solution-format
This repo contains a draft specification of a [json schema](https://github.com/Stuartlab-UCSC/cluster-solution-format/blob/master/cluster_solution_schema.json) for cluster solutions created from single cell mRNA seq data. 
A cluster solution is loosely defined as the output of any clustering algorithm, e.g. louvain, k-means, or more domain 
specific algorithms such as [SC3](https://www.nature.com/articles/nmeth.4236).  

The schema mirrors this data model:

![alt text](https://github.com/Stuartlab-UCSC/cluster-solution-format/blob/master/datamodel_slide.png "Data Model")


Along with metadata about the cluster solution, 3 major types of information can detail each cluster.
	
  * cell assignments: The categorical (or probabilistic) assignment of cells to clusters, i.e. the output of a cluster algorithm.
  *	markers: Arbitrary metrics for genes as markers that identify individual clusters.
  *	cell type annotation: A label that maps a cluster to a cell type.  

The cell assignments field is the only information required for a valid cluster solution json object.

#### Some thoughts on other options for formats:

Three classes of formats that spring to mind are a json specification as represented here, .csv or .tsv files, and loom 
and other matrix annotation files.
 
The advantage of tab or comma separated value files seems to be their simplicity, they are easy to pull into analysis 
pipelines and language indifferent. Where these formats fail is the ability to track important metadata about the cluster solution, e.g. the algorithm that produced the cluster solution.

Other matrix file formats such as loom or more language specific formats such as Seurat and Scanpy objects are also 
easily integrated into analysis. While these formats are more general and can carry metadata for cluster solutions they 
are currently lacking standards to document and validate their schemas. Understanding the schema of Loom, Scanpy, or 
Suerat often requires reading objects into memory and manually investigating their annotation fields. These types of objects 
are very good at "it just works" analysis pipelines, but problems with interoperability commonly arise due to a lack of 
standardization in their structure.

While json provides modeling of metadata and standards for documenting and validating the schemas, it requires knowledge
of the schema to transform the information into data structures ready for comparative analysis and visualization. This 
deficit is easy to code around as libraries for parsing the json into analysis structures can be written and tested with
relative ease.

A best of both worlds solution could implement something similar to [this effort to standardize the mapping of  annotations to ontology terms](https://github.com/HumanCellAtlas/matrix_semantic_map). It gives an example of 
 integration between a well defined json schema and loom files.

