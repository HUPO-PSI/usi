# USI Collection Identifiers

Universal Spectrum Identifier (USI) for Mass Spectrometry has as its second field a collection identifier.
The specification itself does not prescribe the complete list of allowable collection identifiers. Rather,
the list is maintained here at GitHub and is extensible in an open manner without changing the specification.

# Permitted Collection Identifiers:

1. PXDnnnnnn - The preferred collection identifier is of the form PXDnnnnnn, such as PXD017269
(http://proteomecentral.proteomexchange.org/dataset/PXD017269). The PXDnnnnnn SHOULD be used for all proteomics
mass spectrometry datasets that have been registered at ProteomeXchange.

2. MSVnnnnnnnnn - A collection identifier for a datasets contained at the MassIVE repsositorym such as MSV000078556. This type of 
identifier SHOULD only be used when there is not a corresponding PXDnnnnnn identifier for the dataset, as is often the case
for metabolomics datasets.

3. RPXDnnnnnn - a ProteomeXchange identifier for a reprocessed dataset of the form RPXDnnnnnn, such as RPXD006668
(http://proteomecentral.proteomexchange.org/dataset/RPXD006668). The RPXDnnnnnn SHOULD ONLY be used when there is no
corresponding PXDnnnnnn identifier available (as in the case where an RPXDnnnnnn dataset derives from a non-ProteomeXchange
dataset.) The PXDnnnnnn identifier should always be used when possible.

4. PXLnnnnnn - A ProteomeXchange spectral library identifier of the form PXLnnnnnn. All spectral libraries registered
through ProteomeCentral are given a PXLnnnnnn identifier. These collections contain representative spectra often aggregated
from several replicates, rather than original scan events in MS datasets as denoted by PXDnnnnnn identifiers.

There are no other approved collection identifiers at this time.

