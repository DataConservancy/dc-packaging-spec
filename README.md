# Data Conservancy Packaging Specification

This repository manages the official version(s) of the 
[Data Conservancy][dc] packaging specification.

Please see our [site][wiki] for specification documents.

# Developers Documentation

## Using GitHub Pages

This [site][wiki] is managed using GitHub Pages [pages].

To use [GitHub Pages] [pages], you will need to create a
GitHub [OAuth token](https://github.com/settings/tokens) that
has the following permissions:

* _repo_
* _user:email_

Then, add the following `<server>` entry to your Maven 
`settings.xml` file:

    <server>
      <id>github</id>
      <!-- no username -->
      <password><!-- token value --></password>
    </server>

## Site Management

The content of the site is in `src/site/markdown`.  Files ending 
in `.md` are parsed as Markdown documents, and converted 
to XHTML prior to publication.  

### Edits

To make edits to site content, clone this repository, and edit 
the files under `src/site/markdown`.  To preview your changes, run:

    mvn clean site -Dnopush

The output will be in the `target/site` directory.

When you are happy with your changes, use `git` to commit them,
**providing appropriate detail with your changes** (the entire
reason these documents are managed in git is to provide provenance).

Push your changes.  

### Peer Review

**If your changes require peer review**, STOP HERE.  Point your
colleagues to your changes and iterate over their feedback.

### Publishing the site

When the changes have been approved, publish them to the website by
running:

    mvn clean site

The site will be rendered and published to GitHub.

## Specifcation Update Guidelines

Specifications should be infrequently updated.

Updates that fix typographical or grammatical errors don't need to
be reviewed, and may be committed and published as needed.

However, changes to the information content of a specification document 
should be reviewed by the team prior to publication.  Publishing these
changes should be considered significant, and should at least involve
updating the `Last Published` date in the specification document, and
depending on the changes, increment the version of the specification.

[dc]: http://www.dataconservancy.org "Data Conservancy"
[wiki]: http://dataconservancy.github.io/dc-packaging-spec/ "Data Conservancy Packaging Specifications site"
[pages]: https://pages.github.com/
