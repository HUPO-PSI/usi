# Universal Spectrum Identifiers from DIA datasets

Data-independent acquisition (DIA) workflows are widely used in the field of mass spectrometry proteomics as a technique that overcomes the limitations of data-dependent acquisition (DDA), primarily the stochastic nature of which ions are selected for fragmentation and which are not. In DIA, essentially all ions within a broad working range are fragmented in each MS run. The tradeoff is that DIA fragmentation spectra a highly multiplexed, with fragments of many different precursor ions present in each spectrum, whereas the typical goal (not always fully realized) of DDA is to isolate a single precursor ion at a time for fragmentation. DIA fragmentation spectrum are therefore substantially more challenging to interpret.

There are broadly two methods for analyzing DIA. The first method is to analyze the original spectra looking for signals
from a list of expected analytes in a mode somewhat analogous to selected reaction monitoring (SRM). This is sometimes
referred to as peptide-centric analysis ([see e.g. Ting et al. PMC4563716](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4563716)).
The second method is to attempt to extract fragmentation spectra from the DIA signals based on temporal shape of the elution
profiles (i.e. all fragment ion signals that exhibit an aligned rise and fall in time can be assumed to originate from the same
analyte), and process those extracted spectra with conventional search engines in a spectrum-centric mode.

The Universal Spectrum Identifier (USI) was developed by the HUPO Proteomics Standards Initiative (PSI) as a mechanism to uniquely identify and recall a specific spectrum that is held up as evidence of a particular identification or conclusion. For example, if detection of one of the Human Proteome Project (HPP) so-called “missing proteins” is claimed, the HPP MS Data Interpretation Guidelines 3.0 stipulate that claims via DDA data must be supported by a USI of the spectra be made available so that they may be examined and the validity of the claim assessed.

In principle the USI concept applies in the same way to DIA spectra. DIA MS2 spectra may be uniquely identified with the USI scheme and the interpretation provided. The only complication is that the resulting spectrum will mostly likely contain not just the purported analyte, but typically many others. This may confound the ability to infer correctness or plausibility based on inspection alone. Here we describe how USIs for DIA data can currently be used, as well as future enhancements that may improve their usability.



# Current functionality for accessing USIs for DIA data

Access to arbitrary spectra in ProteomeXchange repositories is currently provided via the ProteomeXchange Expression Interface (PROXI) as implemented by most of the ProteomeXchange repositories. The /spectra endpoint in the PROXI application programming interface (API) accepts a request with a USI and responds with the spectrum data if it is available. Any application may use this API to obtain spectra, but the currently most common application that supports spectrum access via USI is the ProteomeXchange ProteomeCentral USI interface at https://proteomecentral.proteomexchange.org/usi. There, users may paste in a USI (or it can be provided in the URL) to the interface, which in turn initiates a PROXI request to all repositories and displays results that are returned using the Lorikeet spectrum viewer and Quetzal spectrum annotation system.

An example of a USI for a DIA spectrum is: mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396:SAGQGEVLVYVEDPAGHQEEAK/3, which can be resolved with the URL https://proteomecentral.proteomexchange.org/usi/?usi=mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396:SAGQGEVLVYVEDPAGHQEEAK/3 as shown in Figure 1. Activating that hyperlink should cause the ProteomeCentral service to request that USI from all ProteomeXchange repositories and provide detailed information about the responses. At this time, MassIVE, PeptideAtlas, PRIDE, and ProteomeCentral all return a spectrum. The USI requests the spectrum generated as scan number 62396 in the MS run 20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000.raw in the ProteomeXchange dataset PXD019909. This was originally deposited in PRIDE, but PeptideAtlas and MassIVE also host the dataset and can furnish the spectrum. The spectrum from each repository are not guaranteed to be identical (some calibration or processing may have taken place), but generally are. The first spectrum to return is displayed by default, but the user may select which spectrum of all the returned ones to display. Figure 1 shows the Lorikeet representation of this spectrum (zoomed in slightly for a better figure).

<img src="https://raw.githubusercontent.com/HUPO-PSI/usi/refs/heads/master/Examples/USIs_from_DIA_Figure1.PNG"><br>
Figure 1. ProteomeCentral Lorikeet visualization of mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396:SAGQGEVLVYVEDPAGHQEEAK/3

Clearly the proposed peptide ion (SAGQGEVLVYVEDPAGHQEEAK/3) is not the dominant species in the multiplexed spectrum, but the y ion series and b ion series are extensive and lend substantial credibility to the veracity of this detection. A far weaker ion series would cause doubt. Note that different repositories return different amounts of metadata about the spectrum. PRIDE returns extensive metadata, including the filter line “FTMS + p NSI Full ms2 777.9000@hcd27.50 \[108.6667-1630.0000\]”, which provides fragmentation type, collision energy, scan range, and more. The isolation window offset terms show that the full width of the isolation window was 27 m/z.
A second example spectrum can be seen in Figure 2 via USI mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Keratinocytes_NN002:scan:4979:SHHSHSSSSSSSASTSGK/2 in the same dataset at the URL https://proteomecentral.proteomexchange.org/usi/?usi=mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Keratinocytes_NN002:scan:4979:SHHSHSSSSSSSASTSGK/2. There are a few ions matched, but these are all low-information ions, and there are insufficiently lengthy b and y series to believe this purported identification. We do note that DIA analysis software will often use multiple scans as well as a retention time delta to score an identification, and thus a single scan USI may not reveal the whole picture. Yet, the user may still be able to ascertain if the proposed identification is yielding nearly full backbone coverage, resulting is great confidence, or is relatively weak and perhaps more likely correct than incorrect, but not the outstanding evidence one would seek for an extraordinary claim.


<img src="https://raw.githubusercontent.com/HUPO-PSI/usi/refs/heads/master/Examples/USIs_from_DIA_Figure2.PNG"><br>
Figure 2. ProteomeCentral Lorikeet visualization of mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Keratinocytes_NN002:scan:4979:SHHSHSSSSSSSASTSGK/2


# Methods for generating USIs from DIA-NN analysis

DIA-NN is one of the most common data analysis tools for DIA data, but its default output does not report the scan numbers that can be used in USIs. The output does report retention times. It would be ideal to get DIA-NN output to directly report peak scan numbers for use in the USIs. Efforts are underway to do this. In the meantime or as an alternative, a method to convert retention times into scan numbers is possible, although would be more cumbersome for users. Another alternative is to extend the USI specification to accept a retention time directly and enable back-end tools to convert from the supplied retention time to scan numbers that can be used to access the spectra directly.


# Methods for generating USIs from Spectronaut analysis

Spectronaut is one of the most common data analysis tools for DIA data, but its default output does not report the scan numbers that can be used in USIs. The output does report retention times. It would be ideal to get Spectronaut output to directly report peak scan numbers for use in the USIs. Efforts are underway to do this. In the meantime or as an alternative, a method to convert retention times into scan numbers is possible, although would be more cumbersome for users. Another alternative is to extend the USI specification to accept a retention time directly and enable back-end tools to convert from the supplied retention time to scan numbers that can be used to access the spectra directly.



# Extensions for the USI for DIA concept

The current design of USIs provides for a single scan number. However, the concept could be extended to include a set of scan numbers in one MS run. For example, for the case of Figure 1, scan number 62396 provides good peaks for the proposed peptide ion. Since this MS run uses 1 MS1 scan followed by 32 MS2 scans, the next scans of this same window are 62429, 62462, 62495, 62528, 62561, etc. In fact, the latter scan provides an even better series of fragment ions, as seen in Figure 3.

<img src="https://raw.githubusercontent.com/HUPO-PSI/usi/refs/heads/master/Examples/USIs_from_DIA_Figure3.PNG"><br>
Figure 3. ProteomeCentral Lorikeet visualization of mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62561:SAGQGEVLVYVEDPAGHQEEAK/3, five scans of the same window after Figure 1, with even higher signal for this peptide ion.

We hypothesize a USI that provides the full list of scans with good signal for this peptide ion, perhaps such as mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396,62429,62462,62495,62528,62561:SAGQGEVLVYVEDPAGHQEEAK/3 that could provide a more complex visualization that tracks the peptide ion across a set of scans and displays relative fragment ions intensities with predictions such as from MS2PIP or Prosit.

