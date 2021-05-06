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

`-debug` outputs some information e.g. about the catalog operations. Without the `-debug` argument (and if a path to an XML document is provided), the program outputs nothing. Errors are written to stderr.

## References

See the [Libxml2 XmlTextReader Interface tutorial](http://xmlsoft.org/xmlreader.html) and [Catalog support](http://xmlsoft.org/catalog.html) for more information. Note that the libxml2 itself has a command line tool [xmllint](http://xmlsoft.org/xmllint.html).

libxml2 is maintained at [xmlsoft.org](http://www.xmlsoft.org) and can be used under the [MIT License](https://opensource.org/licenses/mit-license.html).