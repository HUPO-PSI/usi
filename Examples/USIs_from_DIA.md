# Universal Spectrum Identifiers from DIA datasets

There are broadly two methods for analyzing DIA. The first method is to analyze the original spectra looking for signals
from a list of expected analytes in a mode somewhat analogous to selected reaction monitoring (SRM). This is sometimes
referred to as peptide-centric analysis ([see e.g. Ting et al. PMC4563716](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4563716)).
The second method is to attempt to extract fragmentation spectra from the DIA signals based on temporal shape of the elution
profiles (i.e. all fragment ion signals that exhibit an aligned rise and fall in time can be assumed to originate from the same
analyte), and process those extracted spectra with conventional search engines in a spectrum-centric mode. Here we provide some
examples of USIs for both strategies.

# USIs for peptide-centric analysis of DIA data:

1. USI for SAGQGEVLVYVEDPAGHQEEAK: [mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396:SAGQGEVLVYVEDPAGHQEEAK/3](https://proteomecentral.proteomexchange.org/usi/?usi=mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Skin_Dendritic_cells_DC_MT_600000:scan:62396:SAGQGEVLVYVEDPAGHQEEAK/3)
This PSM clearly shows that while there are definitely other, more abundant analytes in the selection window, this peptide SAGQGEVLVYVEDPAGHQEEAK (3+) has
very good evidence of being one of the present analytes. There is a very long y ion series and long bio ion series with nearly every residue in the peptide having a y or b ion.
This USI was selected from a DIA-NN (ref) analysis of [PXD019909](https://proteomecentral.proteomexchange.org/cgi/GetDataset?ID=PXD019909)....
(It would be very nice to share of details about how this USI was constructed based on the DIA-NN output files).

1. USI for SHHSHSSSSSSSASTSGK: [mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Keratinocytes_NN002:scan:4979:SHHSHSSSSSSSASTSGK/2](https://proteomecentral.proteomexchange.org/usi/?usi=mzspec:PXD019909:20180914_QE8_nLC0_BDA_SA_DIA_Keratinocytes_NN002:scan:4979:SHHSHSSSSSSSASTSGK/2)
This PSM clearly shows a likely false positive identification. There are only identified peaks for b2, y1, y2 peaks, which would be a potential property of many of peptides, even within
a narrow retention time range. This USI was selected from a DIA-NN (ref) analysis of [PXD019909](https://proteomecentral.proteomexchange.org/cgi/GetDataset?ID=PXD019909)....
(It would be very nice to share of details about how this USI was constructed based on the DIA-NN output files).


# USIs for spectrum-centric analysis of DIA data:

Still to do..

