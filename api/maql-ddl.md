---
title: API Documentation
layout: default
---

# Modeling Data with MAQL DDL

**MAQL** (Multidimensional Query Language) is a simple yet powerful query language that provides an underpinning of GoodData's reporting capabilities. It's extension **MAQL DDL** (MAQL Data Definition Language) is used for building and adapting a data model.

# Getting Started

Similar to the core MAQL, DDL syntax is simple and reminiscent of SQL. At it's core, there are three most important commands to choose from: **CREATE**, **ALTER** and **DROP**. These commands can be applied to objects forming the data model:

* [datasets](#create-datasets) (dataset is one joint source of data and comprises of attributes and facts)
* attributes (attribute is container of data that cannot be added - typically all strings and some numeric columns, like ID or SSN)
* facts (a fact is a data column containing computational data - ie. prices, amounts etc.)
* folders (folders are used to organize attributes and facts visually for users)
* datatypes?



# CREATE syntax

_…work in progress…_

<a name="create-dataset">
### CREATE DATASET
</a>

        CREATE DATASET {dataset.csv2009} VISUAL(TITLE "Dataset for csv from 2009");

<a name="create-attribute">
### CREATE ATTRIBUTE
</a>

        CREATE ATTRIBUTE {attr.opportunity.category} VISUAL(TITLE "Category of opportunity", FOLDER {folder.opportunity}) AS {tab_cat.col_id};

<a name="create-fact">
### CREATE FACT
</a>

        CREATE FACT {fact.opportunity.sales} VISUAL( TITLE "Sales" ) AS {tab_opp.col_sales};

<a name="create-folder">
### CREATE FOLDER
</a>

        CREATE FOLDER {folder.one} VISUAL ( TITLE "folder one", DESCRIPTION "some description" ) TYPE ATTRIBUTE

# ALTER syntax

### ALTER DATASET
Dataset being a simple named container for attributes and facts, modifications are fairly straightforward:

1. add attribute/fact:

        ALTER FACT {a} ADD {table.column};

2. remove attribute/fact:

        ALTER FACT {a} DROP {table.column};

3. change the name of the dataset:

        ALTER FACT {a} VISUAL(TITLE "Internal Data");

### ALTER ATTRIBUTE