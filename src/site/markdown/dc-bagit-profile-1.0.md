title: Data Conservancy BagIt Profile - 1.0
description: The Data Conservancy BagIt Profile refines the IETF BagIt
             specification in order to increase platform interoperability
             and provide mechanisms for describing the custodial content of 
             the Bag.             

# Data Conservancy BagIt Profile

### Version 1.0

Originally Published: 12/23/2015

Last Published: 12/23/2015

* * *

The current [BagIt specification][bagit-0.97] at the time of this writing is version 0.97, 
expiring Dec 25, 2015.  This document refers to it as the “BagIt 
specification”, or simply “BagIt”.

&ensp;&ensp;1. [Data Conservancy BagIt Profile](#1)

&ensp;&ensp;2. [Interoperability](#2)

&ensp;&ensp;&ensp;&ensp;2.1 [Interoperability With Previous Data Conservancy Profiles](#2.1)

&ensp;&ensp;&ensp;&ensp;2.2 [Interoperability With BagIt](#2.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.1 [Validity with regard to the BagIt Specification](#2.2.1)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.2 [Filename interoperability between platforms](#2.2.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.2.1 [Illegal characters](#2.2.2.1)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.2.2 [Illegal file names](#2.2.2.2)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.2.3 [Maximum path length](#2.2.2.3)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.3 [Fetch support](#2.2.3)

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2.2.4 [Reserved metadata names and cardinality](#2.2.4)

&ensp;&ensp;3. [Conforming Bag Structure](#3)

&ensp;&ensp;&ensp;&ensp;3.1 [Reserved directories and tag files](#3.1)

&ensp;&ensp;&ensp;&ensp;3.2 [Bag name](#3.2)

<a name="#1"/>
# 1. Data Conservancy BagIt Profile

This is version `1.0` of the Data Conservancy BagIt profile.  Conforming Bags will 
have the following metadata name and value in `bag-info.txt`:

    BagIt-Profile-Identifier:  http://dataconservancy.org/formats/data-conservancy-pkg-1.0
    
<a name="#2"/>    
# 2. Interoperability

<a name="#2.1"/>
## 2.1 Interoperability With Previous Data Conservancy Profiles

This profile specification is incompatible with previous versions of this profile. 
This profile supercedes [version `0.9`][bagit-profile-0.9] of the Data Conservancy BagIt profile, identified 
by the following metadata name and value in `bag-info.txt`:

    BagIt-Profile-Identifier:  http://dataconservancy.org/formats/data-conservancy-pkg-0.9
   
<a name="#2.2"/>   
## 2.2 Interoperability With BagIt

<a name="#2.2.1"/>
### 2.2.1 Validity with regard to the BagIt Specification

Bags conforming to this profile must be valid as defined by the BagIt specification.  
Therefore, a Bag conforming to Data Conservancy BagIt Profile 1.0 will be a 
_complete and valid_ bag per the BagIt specification.

<a name="#2.2.2"/>
### 2.2.2 Filename interoperability between platforms

Section 7 of the BagIt specification discusses practical concerns of Bag 
interoperability between platforms.  While [BagIt §7][bagit-7] is informative, this 
profile applies the following constraints to address platform interoperability.

<a name="#2.2.2.1"/>
#### 2.2.2.1 Illegal characters

The following characters are illegal, and are not to be used in path segments 
or file names, informed by [BagIt §7.2.2][bagit-722]:

* Unicode characters in the range of 0x00 - 0x1f
* “ (Quotation mark, 0x22)
* \* (Asterisk, 0x2a)
* / (Solidus, 0x2f)
* : (Colon, 0x3a)
* < (Less than sign, 0x3c)
* \> (Greater than sign, 0x3e)
* ? (Question mark, 0x3f)
* \ (Reverse Solidus, 0x5c)
* | (Vertical line, 0x7c)
* ~ (Tilde, 0x7e)
* (Delete, 0x7f)
* Any other Unicode characters outside of the Latin Code Block (0x80 and above) 

<a name="#2.2.2.2"/>
#### 2.2.2.2 Illegal file names

The following are not to be used as file names, informed by [BagIt §7.2.2][bagit-722], 
and [MSDN article][msdn]:

* CON 
* PRN
* AUX
* NUL
* COM1
* COM2
* COM3
* COM4
* COM5
* COM6
* COM7
* COM8
* COM9
* LPT1
* LPT2
* LPT3
* LPT4
* LPT5
* LPT6
* LPT7
* LPT8
* LPT9
* The above file names with any extension, e.g. `CON.txt`

<a name="#2.2.2.3"/>
#### 2.2.2.3 Maximum path length

The maximum allowed path length within the bag is 1024 bytes, and the maximum 
allowed file name length is 255 bytes.

In addition to the restrictions presented in [§2.2.2.1](#2.2.2.1), path segments (demarcated 
by ‘/’) in a manifest must not be equal to any of the following byte sequences:

* . (Full Stop, 0x2e)
* ./ (Full Stop, Solidus, 0x2e2f)
* ../ (Full Stop, Full Stop, Solidus, 0x2e2e2f)

<a name="#2.2.3"/>
### 2.2.3 Fetch support

Bags conforming to this profile must be _valid_ (and therefore _complete_) per 
[BagIt §3][bagit-3].  Our profile does not support _fetch.txt_ ([BagIt §2.2.3][bagit-223]), 
therefore bags with a non-empty fetch file will not be conformant with this profile.

<a name="#2.2.4"/>
### 2.2.4 Reserved metadata names and cardinality

This profile adds cardinality constraints on the reserved metadata names in [BagIt §2.2.2][bagit-222]:

    Source-Organization: minOccurs=0, maxOccurs=unlimited
    Organization-Address: minOccurs=0, maxOccurs=unlimited
    Contact-Name: minOccurs=0, maxOccurs=unlimited
    Contact-Phone: minOccurs=0, maxOccurs=unlimited
    Contact-Email: minOccurs=0, maxOccurs=unlimited
    External-Description: minOccurs=0, maxOccurs=1
    Bagging-Date: minOccurs=0, maxOccurs=1
    External-Identifier: minOccurs=0, maxOccurs=unlimited
    Bag-Size:minOccurs=0, maxOccurs=1
    Payload-Oxum: minOccurs=0, maxOccurs=1
    Bag-Group-Identifier: minOccurs=0, maxOccurs=1
    Bag-Count: minOccurs=0, maxOccurs=1
    Internal-Sender-Identifier: minOccurs=0, maxOccurs=unlimited
    Internal-Sender-Description: minOccurs=0, maxOccurs=1

This profile adds the following additional reserved metadata names:

    BagIt-Profile-Identifier: minOccurs=1, maxOccurs=1
    Resource-Manifest: minOccurs=1, maxOccurs=1

Metadata names with `minOccurs=0` should be considered optional, 
whereas names with `minOccurs=1` are required.

<a name="#3"/>
# 3. Conforming Bag Structure

<a name="#3.1"/>
## 3.1 Reserved directories and tag files

Any directories or filenames reserved by this profile are considered as 
“Other Tag Files” per [BagIt §2.2.4][bagit-224].  Tag files defined by this profile 
SHOULD have entries in the tag manifests as specified by [BagIt §2.2.1][bagit-221].

This profile reserves the directory `META-INF/org.dataconservancy.packaging`, 
its subdirectories, and any contained files, where the `META-INF` directory 
is a sibling of the `data` directory.  

The directory `META-INF/org.dataconservancy.packaging/ONT` is reserved 
specifically to distribute ontologies that are referenced by the package 
description or bag payload.

The directory `META-INF/org.dataconservancy.packaging/PKG-INFO` is 
reserved specifically to distribute any files (such as ORE 
Resource Map(s)) that describe the structure of the bag.

The nature of the files and structure under the `PKG-INFO` and `ONT` 
directories will be part of another specification.

<a name="#3.2"/>
## 3.2 Bag name

Bags conforming to this profile MUST name the single-file form of the 
bag (i.e. tar archive or zipped form) after the base directory of the bag.  
This changes the SHOULD in [BagIt §4][bagit-4] item #2 to a MUST.

[bagit-0.97]: http://tools.ietf.org/html/draft-kunze-bagit-11
[bagit-212]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-2.1.2
[bagit-221]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-2.2.1
[bagit-222]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-2.2.2
[bagit-223]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-2.2.3
[bagit-224]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-2.2.4
[bagit-3]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-3
[bagit-4]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-4
[bagit-7]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-7
[bagit-722]: http://tools.ietf.org/html/draft-kunze-bagit-11#section-7.2.2
[bagit-profile-0.9]: http://dataconservancy.org/wp-content/uploads/2013/08/Package-DCS-BagIt-Specification-DRAFT-2013-08-09.pdf
[msdn]: http://msdn.microsoft.com/en-us/library/aa365247.aspx
