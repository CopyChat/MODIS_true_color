
  Version 2.1 of the Modis Direct Broadcast NDVI/EVI algorithm
    directreadout.gsfc.nasa.gov

  The algorithm requires all three Level 1b MODIS files (1KM, HKM, QKM).
The output is Normalized Difference Vegetation and Enhanced Vegetation in
a single HDF file.  Processing require one ancillary input file, tbase.hdf
(included).

BUILD:
  Run 'make' in the src directory.

INSTALL:
  Place the binaries in any convienient directory.
  Place the tbase.hdf file in a accessible directory.

EXECUTION:
  A script is provided in the 'run' directory, 'run.csh', which demonstrates
the input requirements and calling sequence.


