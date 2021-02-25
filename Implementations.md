# USI Implemenation Notes

There is an important distinction between the USI, which is just an identifier, and how it will be used in PROXI and other web services. We envision that the USI will eventually be implemented as part of the PROXI (ProteomeXchange eXpression Interface) API, which will enable, among other things:

- Request of a raw spectrum given a USI, returned in one of several formats
- Request of an annotated spectrum given a USI based on what the server thinks that spectrum might represent
- Request of an annotated spectrum given a USI including an interpretation from the user
- Visual interactive display of a raw or annotated spectrum given a USI
- Request of what identified peptide ion is putatively associated with a given USI
- A list of USIs from a server given the request of: what spectra do you have for peptide ion X?
- A list of USis from a server given the request of: what spectra do you have for peptide Y?
- The USI will also be used within spectrum libraries and spectral archives as a unique identifier within those collections, yet to be defined.
 
For the moment, it is recommended that we begin with some interactive interfaces to explore the fitness of this specification and explore how it should be amended.

Servers supporting the USI are expected to return a set of rich non-success messages to the user. One benefit of the multipart key USI design is that servers can parse the identifier and return one of the following error messages if the retrieval of the spectrum is not successful:

Inherent USI syntax problems:
- [MissingPreamble] USI does not begin with expected preamble 'mzspec:’
- [UnrecognizedDatasetIdentifierFormat] Identifier 'XXX’ does not conform to a known allowable identifier.
- [EmptyMsRun] Third field MS run is empty, which is not permitted.
- [UnrecognizedIndexFlag] Fourth field is supposed to be an index flag, but its value is 'ZZZ', which is not a permitted value. Only 'scan', ‘index’, or ‘nativeId’ are currently permitted.

Problems related to a server not finding the specified resource:
- [DatasetNotAvailable] Dataset identifier ‘XXX’ is recognized but not an available collection at this server.
- [InvalidMsRun] Specified MS run ‘YYY’ is not found within the dataset with identifier ‘XXX’, which is present on this server.
- [UnavailableIndex] Provided index ‘AAA’ appears to be an invalid index of type ‘ZZZ’ within dataset identifier ‘XXX’ and MS run ‘YYY’.
- [SpectrumUnavailable] Dataset, MSRun, and index appear valid and should be available here, but the spectrum could not be fetched from the data store (internal server data fetching error)
- Etc.


# Current Implementation

Since the notes on current implementation is likely to change frequently, while the specification should remain static, notes describing the current implementations are provided in a separate document available at http://psidev.info/USI.


# Reference Implementation

PSI Specifications are required to come with a reference implementation. What shall we say about a reference implementation? Shall we provide a reusable Java or Python class that performs USI parsing and encoding functionality and can be extended as desired to implement local functionality?
