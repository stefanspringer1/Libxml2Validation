# Libxml2Validation

## About This Project

This is a (very) little C project for the validation of XML documents using libxml2. The resulting executable is to executed from the command line, but the code can easily be adjusted for other use cases.

There is currently only the one source file `main.c` in this repository, with is adapted from the XmlTextReader example of the libxml2 distribution (even most of the comments are retained, which might not be completely correct any more for the current use case).

For this project to be built, the library should be available on the system.

Windows: Download the binary from http://www.xmlsoft.org. Such a download should also contain the header files. Add those headers in a subdirectory `libxml` of the project and in-comment the line with `target_include_directories` in `CMakeLists.txt`. You might register the libxml2-DLL via `regsvr32` (but there mightj be better options).

Note that you might have to out-comment `set(CMAKE_EXE_LINKER_FLAGS -lxml2)` in `CMakeLists.txt`.

Note that newer `xmlReader` from is used here and not the SAX interface, since in libxml2 validation is only possible either by using `xmlReader` or by building the DOM tree.

## The Resulting Program

The binaries for some platforms are added in the subdirectory `Binaries`.

The current state is:

- Allow the validation of an XML document by its DTD using the system ID.
- Alternatively use an (XML-)catalog top resolve the DTD and other entities.

Of course, many more options could be added.

Current command line interface:

arguments: `<document> [-catalog=<catalog>] [-debug]`

`-debug` outputs some information e.g. about the catalog operations. Without the `-debug` argument (and if a path to an XML document is provided), the program only outputs the encoding in the form

`[ENCODING=<encoding>]`

e.g. `[ENCODING=us-ascii]`. Errors are written to stderr.

## On Referencing Catalog files

Instead of giving the `-catalog=...` argument, you can also set the environment variable `XML_CATALOG_FILES` to a list of paths to (XML-)catalog files, and to set the debug mode for the catalog processing (for outputting information about the resolution of those files) you can set the environment variable `XML_DEBUG_CATALOG` (the value does not matter). This is just what the program itself will do depending on the arguments `-catalog=...` and `-debug`.

## Running on Windows

Note that **on Windows, you have to set the environment variables `XML_CATALOG_FILES` and `XML_DEBUG_CATALOG` yourself before calling the program** (of course, you then do not need to set the according program arguments). To set `XML_DEBUG_CATALOG`, use a non-empty value (e.g. `YES`).

Also note that it might not be necessary to have all the libraries that you currently find in `Binaries/Windows.Intel`.

## Paths Containing Non-ASCII Characters

We currently do not know what happens with paths containing non-ASCII characters. We suspect that they might not work. That should then be fixed.

## References

See the [Libxml2 XmlTextReader Interface tutorial](http://xmlsoft.org/xmlreader.html) and [Catalog support](http://xmlsoft.org/catalog.html) for more information. Note that the libxml2 itself has a command line tool [xmllint](http://xmlsoft.org/xmllint.html).

libxml2 is maintained at [xmlsoft.org](http://www.xmlsoft.org) and can be used under the [MIT License](https://opensource.org/licenses/mit-license.html).