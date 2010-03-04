
WARNING: this template is still under development and things might change every so often.

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

You may want to add some static documentation to the generated documentation. To do
so create a jsdoc toolkit configuration file and add the option 'docs:' with
the 'content' being an array of files to add and optionally 'preprocess'.

Every Entry in the 'content' array must have the fields 'src' and 'title' plus
the optional field 'preprocess'.

The 'preprocess' field gives a shell command to be execute on the 'src' file. It
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

Creating the documentation then will be as easy as (with *nix shell):

    $ run.sh -c='jsdoc.conf' -t="$JSDOCDIR/templates/jsdoc-simple" src

