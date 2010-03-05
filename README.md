
WARNING: this template is still under development and it might change every so often.

jsdoc-simple
============

jsdoc-simple is a modified jsdoc toolkit (Verion 2) template with support for 
additional documentation.

## Install ##

the whole template directory must be copied as is into jsdoc's template directory.

## Usage ##

In order to use 'jsdoc-simple' you have to tell jsdoc toolkit to use it via
the '-t' flag when calling jsdoc or prepare a jsdoc toolkit configuration file 
with option 't:' set to the template's directory.

You also may want to add some static documentation to the generated
documentation. To do so create a jsdoc toolkit configuration file and add the
option 'docs:' with the field 'content' being an array of files to add and
the optional field 'preprocess'.

Every Entry in the 'content' array MUST define the fields 'src' and 'title' plus
the optional field 'preprocess'.

The 'preprocess' field MUST be a shell command to be execute on the 'src' file. It
is assumed that the command will read the file's content from stdin and print
it's outcome to stdout.

for example this will add the files intro.pdc and tutorial.pdc to the
documentation, which are preprocessed using pandoc (Haskell based markdown
program) :

    {
        d: 'docs', // output directory 'docs'
        a: false,  // do not show all symbols
        docs: {
            preprocess: 'pandoc',   // preprocess all files with pandoc
            content: [ {src:'docsrc/intro.pdc',
                        title: 'Introduction' },
                       {src:'docsrc/tutorial.pdc',
                        title: 'Tutorial'}
                     ]
        }
    }

In the following example only the file intro.pdc is preprocessed using pandoc:

    {
        d: 'docs', // output directory 'docs'
        a: false,  // do not show all symbols
        docs: {
            content: [ {src:'docsrc/intro.pdc',
                        preprocess: 'pandoc',   // preprocess this file only with pandoc
                        title: 'Introduction' },
                       {src:'docsrc/tutorial.html',
                        title: 'Tutorial'}
                     ]
        }
    }

When using a global preprocessor for all documentations and a local one for a
file, the latter one is chosen for that file only whereas all others are
preprocessed using the former one.

Creating the documentation then will be as easy as (with *nix shell):

    $ run.sh -c='jsdoc.conf' -t="$JSDOCDIR/templates/jsdoc-simple" src

## Using the Symbol Index ##

The Symbol index page features a text field used for filtering. For filtering
the content of this text field is used as a regular expression. Thus typing the
expression "a|b|c" will find all symbols starting with a or b or c.
Furthermore the regular expressions are case insensitive. But if you have symbol
names using special characters like '$' proper escaping is needed. Meaning
that if you want to filter all symbols starting with '$' you have to type
"\$".

