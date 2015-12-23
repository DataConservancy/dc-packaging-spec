# Data Conservancy Packaging Specification

### Version 1.0

Originally Published: 12/23/2015

Last Published: 12/23/2015

* * *

&ensp;&ensp;1. [What is a Data Conservancy Package?](#1)

&ensp;&ensp;2. [Requirements and terminology](#2)

&ensp;&ensp;&ensp;&ensp;2.1 [Requirements](#2.1)

&ensp;&ensp;&ensp;&ensp;2.2 [Terminology](#2.2)

&ensp;&ensp;3. [Package components and structure](#3)

&ensp;&ensp;&ensp;&ensp;3.1 [Package Serialization](#3.1)

&ensp;&ensp;&ensp;&ensp;3.2 [Specified RDF Resources](#3.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.1 [Resource Serialization](#3.2.1)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.2 [Domain Objects](#3.2.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.3 [Resource Manifest](#3.2.3)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.3.1 [Resource Manifest Model](#3.2.3.1)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.3.2 [Resource Manifest Discovery](#3.2.3.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3.2.4 [Ontologies](#3.2.4)

&ensp;&ensp;4. [Package URIs](#4)

&ensp;&ensp;&ensp;&ensp;4.1 [Bag URIs](#4.1)

* * *

<a name="#1"/>
# 1. What is a Data Conservancy Package?
A Data Conservancy Package is a format (described by this document) for encapsulating digital content (i.e., a payload) with defined semantics, and metadata used to describe technical aspects of the package as a whole.  

<a name="#2"/>
# 2. Requirements and terminology

<a name="#2.1"/>
## 2.1 Requirements
The meaning of  "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" are defined in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

<a name="#2.2"/>
## 2.2 Terminology

*Custodial Content*: The novel information contained within a package according to this specification, and described accordingly (i.e. via *Domain Objects*).  Also known as the package payload.

*Domain Object*: A package resource, modeled using RDF, describing the payload.

*Domain Object Manifest*: A package resource, [modeled as an OAI-ORE Resource Map](http://www.openarchives.org/ore/1.0/datamodel#Resource_Map), enumerating the domain objects in the package.

*Package*: A logical unit of digital content conforming to this specification.   It contains a payload, *Domain Objects* describing the payload, a manifest of *Domain Objects*, and additional package level metadata. 

*Payload*: equivalent to the custodial content of the package

*Serialized Package*: A concrete form of a package expressed as files and directories on a file system.

<a name="#3"/>
# 3. Package components and structure

<a name="#3.1"/>
## 3.1 Package Serialization
Serialized packages MUST conform to the Data Conservancy BagIt profile version 1.0 as specified here.

<a name="#3.2"/>
## 3.2 Specified RDF Resources

<a name="#3.2.1"/>
### 3.2.1 Resource Serialization

RDF resources specified below SHOULD be serialized using the same serialization format. One of the following serialization formats are RECOMMENDED: JSON-LD, RDF/XML, or Turtle. 

Serialization format for specified RDF resources MUST be reflected in filename extensions. Specifically, files serialized in JSON-LD, RDF/XML, and Turtle formats must have `.jsonld`, `.rdf`, and `.ttl` extensions respectively.

<a name="#3.2.2"/>
### 3.2.2 Domain Objects
Domain objects MUST be modeled as RDF resources, and are used to provide semantics for the package payload.  

Serialized domain object resources MUST use a file extension that indicates their serialization format.

<a name="#3.2.3"/>
### 3.2.3 Resource Manifest

<a name="#3.2.3.1"/>
#### 3.2.3.1 Resource Manifest Model
The Resource Manifest MUST be modeled as a single ORE Resource Map containing exactly one ORE Aggregation. The ORE Aggregation MUST enumerate the resources in the package payload that contain serializations of domain objects.  These resources MUST be referenced using a compliant URI ([see §4](#4)).

The serialized ORE-ReM MUST use a file extension that indicates its serialization format, per [§3.2.1](#3.2.1).  

<a name="#3.2.3.2"/>
#### 3.2.3.2 Resource Manifest Discovery
The BagIt metadata keyword Resource-Manifest MUST be present in bag-info.txt, and it’s value MUST be the location of the Resource Manifest serialization, referenced using a compliant URI ([§4](#4)).

This specification RECOMMENDS the use of the `/META-INF/org.dataconservancy.packaging/PKG-INFO/ORE-REM/ORE-REM.[ext]` bag resource for the location of the Resource Manifest, where `[ext]` indicates the extension of the serialization, per [§3.2.1](#3.2.1).

RDF resources specified herein MUST be identified with bag URIs, and MAY be additionally identified using local identifier schemes.

<a name="#3.2.4"/>
### 3.2.4 Ontologies 
It is RECOMMENDED that the package contain all ontologies necessary to interpret RDF resources in the package.  The serialized ontologies MUST use a file extension that indicates their serialization format, per [§3.2.1](#3.2.1).

This specification RECOMMENDS the use of the `/META-INF/org.dataconservancy.packaging/ONT` bag resource for containing ontology serializations.

<a name="#4"/>
# 4. Package URIs
Package URIs have the following characteristics:

* MUST be de-referenceable to a resource within a specific bag (i.e. package URIs have location semantics)
* Are meaningless outside of the context of a specific bag

Package URIs MUST use one of the supported schemes below:

* `bag://`

<a name="#4.1"/>
## 4.1 Bag URIs
This specification proposes a URI scheme for referencing bag resources, allowing resources in a specified bag to be addressed using URIs.  This scheme complies with the characteristics of a package URI, and MAY be used when the serialized package conforms to the Data Conservancy BagIt Profile.  The form of a bag URI is:

    bag://<bag-name>/data/resource.xml

A file containing multiple resources may reference individual resources using hash URIs (i.e. fragments):

    bag://<bag-name>/data/resource.xml#<fragment-id>

The bag URI scheme allows bag resources to be addressed independent of its location on the filesystem, independent of the platform being used and independent of the bag’s serialized form.     

Statements contained within domain objects or the resource manifest MAY have bag URIs as a subject or object.  A bag URI is resolvable within a bag, and signifies the bag creator’s intent that a given URI is intended to resolve to a specific resource.   Outside of the context of a specific bag, bag URIs are not meaningful.  

The following clauses capture the semantics of bag URIs in RDF documents specified herein:

* All bag URIs used in domain objects MUST resolve to a resource in the bag
* For bag URIs that contain hash fragments, the non-hashed portion of the URI MUST resolve to a resource in the bag
* RDF serializations MAY use relative URIs, which MUST be interpreted as being relative to the bag URI of the document containing it
* Absent a specified base URI in the document, the null relative URI (<> in turtle) MUST be interpreted as equivalent to the the bag URI of the file containing it.
