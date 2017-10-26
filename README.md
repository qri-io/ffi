# FFI

<!-- Repo Badges for: Github Project, Slack, License-->

[![GitHub](https://img.shields.io/badge/project-Data_Together-487b57.svg?style=flat-square)](http://github.com/datatogether)
[![Slack](https://img.shields.io/badge/slack-Archivers-b44e88.svg?style=flat-square)](https://archivers-slack.herokuapp.com/)
[![License](https://img.shields.io/github/license/mashape/apistatus.svg)](./LICENSE) 

FFI - File Format identification is a package for making sensible guesses about
file formats from Url strings. FFI is structured as a package to clear the way
for future improvements.

## License & Copyright

Copyright (C) <year> Data Together
This program is free software: you can redistribute it and/or modify it under
the terms of the GNU Affero General Public License as published by the Free Software
Foundation, version 3.0.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.

See the [`LICENSE`](./LICENSE) file for details.

## Getting Involved

We would love involvement from more people! If you notice any errors or would like to submit changes, please see our [Contributing Guidelines](./.github/CONTRIBUTING.md). 

We use GitHub issues for [tracking bugs and feature requests](https://github.com/datatogether/ffi/issues) and Pull Requests (PRs) for [submitting changes](https://github.com/datatogether/ffi/pulls)

## Usage

Add `ffi` to any golang project with `import "github.com/datatogether/ffi"`

`ffi` provides the following functions:

#### func  ExtensionMimeType

```go
func ExtensionMimeType(extenstion string) (string, error)
```
ExtensionMimeType returns a MIME-Type for a given file extension

#### func  FilenameFromUrlString

```go
func FilenameFromUrlString(rawUrl string) (string, error)
```
FilenameFromUrlString returns a file with extension if the url looks like it
resolves to a filename, otherwise it returns an empty string

#### func  FilenameMimeType

```go
func FilenameMimeType(filename string) (string, error)
```
FilenameMimeType gives the mimetype of filename

#### func  MimeType

```go
func MimeType(io.Reader) (string, error)
```
MimeType from an io.Reader is the magic we seek

#### func  MimeTypeExtension

```go
func MimeTypeExtension(mimeType string) (string, error)
```
MimeTypeExtension returns an extension for a given MIME-type

#### func  SetExtension

```go
func SetExtension(filename, mimeType string) (string, error)
```
SetExtension strips any current extension from filename, replacing it with
mimeType's corresponding extension


## Development

The biggest avenue for improvement may be through integration with [PRONOM](http://www.nationalarchives.gov.uk/PRONOM/Default.aspx#) or [File Information Tool Set from Harvard](http://projects.iq.harvard.edu/fits/home)

### PRONOM

PRONOM is a repository of file format signatures stored as XML. Currently the
best tool for working with PRONOM is DROID, which is ill-suited to being run in
web service oriented architectures.

As a suggested path for implementation, one could first focus on wrapping DROID
in a service that invokes droid-cli with a given set of bytes. This would happen
in a separate pacakge from this one. Later we could sit down & learn how to
properly parse PRONOM xml signature files & do byte comparison, which could bue
implemented in this package. Anyone investigating this avenue may wish to also
review some of the work accomplished translating the PRONOM registry:
http://the-fr.org


### FITS

> The File Information Tool Set (FITS) identifies, validates and extracts technical metadata for a  wide range of file formats. It acts as a wrapper, invoking and managing the output from several other open source tools. Output from these tools are converted into a common format, compared to one another and consolidated into a single XML output file. FITS is written in Java and is compatible with Java 1.7 or higher. (from the [project homepage](https://projects.iq.harvard.edu/fits))
