# MDXML
Markdown Extensible Markup Language

Version: 1.1

Tags
----

Tags are done with markdown H1 headers.

    # TagName

Attributes
----------

Attributes are done with markdown H2 headers

    ## Attribute

Attribute Values
----------------

Attribute Values are done with markdown H3 headers and must come immediately after an attribute

    ## Attribute
    ### AttributeValue

Namespaces
----------

Namespaces are done with markdown H4 and H5 headers. H4 headers specify tag namespace, H5 headers specify attribute namespace.

    # Tag
    #### TagNamespace
    ## Attribute
    ### AttributeValue
    ##### AttributeNamespace

Raw Data/CDATA
--------------

Raw Data are done with markdown code blocks

        this is raw data!

You need an empty line at the same depth to trigger a raw data block.

    depth 0
        this is not raw data
    
    depth 0
    
        but this is

Note that when using a raw data block with inner data you need to use 5 spaces instead of just 4

    >    not a raw data block
    >
    >     is a raw data block

Note that, as with inline data below, to get out of a raw data block you need an empty line.

        this is raw data!
    
    this is not raw data! putting it on the above line would keep it as raw data

Inner Data
----------

Inner Data are done with markdown quote blocks

    > this is inner data

Going a depth in is as simple as adding more >. Going one or more depths out requires at least 1 new depth indicator line.

    depth 0
    > depth 1
    > > depth 2
    > > > depth 3
    >
    > depth 1. putting it on the above line would keep it a depth 3
    
    depth 0. putting it on the above line would keep it at depth 1

This also means that:

    # root tag
    > # inner tag
    contents

Is valid and "contents" is the contents of `inner tag`.

Comments
--------

Comments are done with markdown inline code

    `this is a comment`

Multiline comments [Not Markdown Compatible]
--------------------------------------------

Multiline comments are done with [Github Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/)'s [fenced code blocks](https://help.github.com/articles/github-flavored-markdown/#fenced-code-blocks).

    ```
    this is a multiline comment
    ```

Version
-------

To add a version attribute, add it at the absolute start of the document

    ## version
    ### 1.0
    [ rest of the document here ]

Encoding
--------

As with version, encoding also goes at the absolute start of the document

    ## version
    ### 1.0
    ## encoding
    ### utf-8
    [ rest of the document here]

Case-Sensitivity
----------------

MDXML is case-sensitive.

Spaces
------

As with markdown, leading and trailing spaces are ignored except in a few specific situations.

    #something

is the same as

    #     something

which is the same as

       #        something

A note about raw data and inner data blocks:

    >>>>something

is the same as

    > > > > something

which is the same as

    >>>>    something

but is NOT the same as

    >>>>     something

(the latter is a code block with "something")

A line starting with 4 spaces is a code block. An inner data line starting with 5 spaces (">     ") is also a code block.

Escaping
--------

As with markdown, escaping can be done with `\`.

    \    this shows up with 4 spaces in a row
    \# this is not a tag
    \## this is not an attribute
    \`this isn't a comment\`

Unlike markdown, MDXML allows you to use `\n` to insert virtual newlines.

    #Tag\n##Attribute\n###Value\nContent

is equivalent to:

    #Tag
    ##Attribute
    ###Value
    Content

All other escapes are disallowed and should be implicitly unescaped. E.g. `\x` is converted to `x`.
Note that escapes don't work inside raw data blocks or comments (single-line or multi-line).

Compatibility with XML
----------------------

It *may* be possible to convert a MDXML document into an XML document if *at least* the following conditions are met:

- The document contains only properly encoded legal Unicode characters
- The tag names don't contain any of the characters `!"#$%&'()*+,/;<=>?@[\]^`{|}~`, nor a space character, and don't start with -, ., or a numeric digit.
- A single "root" element contains all the other elements.

An example of an XML-compatible MDXML document is available [here](/example.md).
