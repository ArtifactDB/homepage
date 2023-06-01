---
title: "Key concepts"
description: ""
lead: ""
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 110
toc: true
---

## Applications

An ArtifactDB _application_ is a specific deployment of the ArtifactDB system.
For example, Genentech maintains several deployments of ArtifactDB - one for datasets, one for genome annotations, and another for analysis results - and each one is considered as a separate application.
This is not strictly necessary as we could have combined everything into a single application...
but, by separating the use cases, we can set different metadata standards for each application without confusing our users.

## File organization

An ArtifactDB _project_ is just a grouping of related files.
The nature of this grouping is application-specific;
for example, one ArtifactDB deployment may define the outputs of an analysis pipeline as a single project,
while another deployment may consider a project to contain all files associated with a published study.

Each project will contain zero, one or more _files_.
Each file is defined by its "path" inside the project, i.e., the relative file path if the project were treated as a directory of files.
Each application may apply its own constraints on the expected format and contents of each file.

Each project has one or more _versions_, e.g., corresponding to different analysis runs.
Different versions of the same project may share some, all or no files;
the choice between creating a new version of a project (as opposed to a new project altogether) is again application-specific.

Finally, each file has some accompanying _metadata_ in the form of a JSON document.
This should specify the format of the file along with any additional information needed to use the file and interpret its contents.
Each application sets metadata standards by defining one or more JSON schemas to validate each file's metadata document.

## Metadata schemas

The metadata document associated with each file should include a specification for a schema.
Here, the schema specification serves two purposes:

1. It defines the type of resource that is contained within the file.
Depending on the application, this may be as general as "this is a text file", or it may be as specific as "this is a Gzip-compressed CSV file containing this specific analysis result".
2. It defines the metadata standards for each file of that type.
This includes required or optional fields, the types of the fields, and the contents of those fields.
Applications can customize these requirements, e.g., to enforce the presence of a non-empty title and description string in each file's metadata.

We use [JSON schemas](https://json-schema.org) to create the schema for each file type.
This is a powerful framework for defining metadata standards that is both human-readable and machine-parseable,
enabling automated validation with easy development/modification.


