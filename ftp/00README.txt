SOFTWARE FOR CREATING REPROJECTED TRUE COLOR MODIS IMAGES
---------------------------------------------------------

Liam.Gumley@ssec.wisc.edu
19 November 2003

This document describes the software package that accompanies the document

"Creating Reprojected True Color MODIS Images: A Tutorial"

by Liam Gumley, Jacques Descloitres, and Jeffrey Schmaltz.

The purpose of this document is to describe how to install and run the software
necessary to create MODIS true color images from MODIS Level 1B image and
geolocation data. The software packages described here are designed to run
on UNIX systems, including Linux. Testing of the package was done on
Red Hat Intel Linux 7.3 and 8.0.

This document, along with source code and sample data, may be found at

ftp://origin.ssec.wisc.edu/pub/IMAPP/MODIS/TrueColor/

1.0 REQUIRED SOFTWARE
---------------------

The following software packages are required in order to run the examples.
Please download and install all of these packages before attempting to run
the examples.

MODIS Corrected Reflectance (look for“"NDVI" at the following site):
http://directreadout.gsfc.nasa.gov/download_technology/db_software.cfm

(The corrected reflectance program is named crefl.c)

MODIS Swath to Grid Toolbox (MS2GT):
http://nsidc.org/data/modis/ms2gt/

ImageMagick:
http://www.imagemagick.org/

Interactive Data Language (IDL):
http://www.rsinc.com/idl/
ftp://ftp.rsinc.com/pub/idl/unix/

If you do not have a license for IDL, you can still run the IDL Virtual Machine
(VM) to run pre-compiled versions of the IDL software described in this
document. The IDL VM is included in the IDL 6.0 distribution package available
for download at the website mentioned above. Simply install the IDL 6.0 package
on your system according to the instructions at the site above, and you will be
able to run the example code via IDL VM.

Note: The software described in this document has been tested with IDL versions
6.0 and 5.5 on Red Hat Intel Linux.

It is your responsibility to download and install these packages. Please direct
any questions about installation to the respective software providers.

2.0 INSTALLING THE SOURCE CODE AND SAMPLE DATA
----------------------------------------------

The source code is contained in the file named

modis_true_color_v1.0.tar.gz

To install the source code:

$ cd $HOME
$ gzip -dc modis_true_color_v1.0.tar.gz | tar xvf -

The sample data files are contained in the files named

MOD021KM.A2003021.1600.004.2003022113345.hdf.gz
MOD02HKM.A2003021.1600.004.2003022113345.hdf.gz
MOD02QKM.A2003021.1600.004.2003022113345.hdf.gz
MOD03.A2003021.1600.004.2003022060031.hdf.gz

To install the sample data files (assuming you downloaded them to $HOME):

$ cd $HOME/TrueColor/data
$ mv $HOME/MOD*.A2003021.1600.*.hdf.gz .
$ gzip -d *.gz

You should now have a 'TrueColor' directory containing the following files and
directories:

data		is a directory containing the sample MODIS Level 1B data
images		is a directory containing images created by the sample script
run		is a directory where you will run the example code
Script.csh	is a C shell script which runs the example code
Script.out	is a listing of the runtime standard output from Script
Script_VM.csh	is a C shell script which runs the example code via IDL VM
src		is a directory containing source code and scripts
             
3.0 RUNNING THE SAMPLE CODE
---------------------------

If you have a license for IDL, you can run the example via the C shell script
named Script.csh, e.g.,

$ cd $HOME/TrueColor
$ ./Script.csh

Note: You may need to edit the script to reflect your local installation
of MS2GT.

When running the example with licensed IDL, you do not need an X display. This
means the code can be run in the UNIX background.

If you do not have a license for IDL, but you have installed IDL 6.0, you can
run the example via the C shell script named Script_VM.csh, e.g.,

$ cd $HOME/TrueColor
$ ./Script_VM.csh

When running the example with IDL VM, you must have an X display active,
because IDL VM shows a splash screen before running the code. This means the
code cannot be run in the UNIX background under IDL VM.

4.0 OUTPUT FILES
----------------

When you run either script, the output files are written in the directory
named 'run'. The reprojected true color images are stored in the files named

true.tif		24-bit uncompressed TIFF image at 250 meter resolution
true_250m.jpg		24-bit enhanced JPEG image at 250 meter resolution
true_1000m.jpg		24-bit enhanced JPEG image at 1000 meter resolution
true_thumb.jpg		24-bit enhanced JPEG image at thumbnail resolution

See the tutorial document for more information on the other files which are
created in the 'run' directory.

5.0 CUSTOMIZATION
-----------------

Here are some suggestions for customizing the software:

(a) Use IMAPP MODIS Level 1B input instead of DAAC Level 1B

(b) Create a 1000 meter resolution image more quickly by using 1KM instead of
QKM input data in map_parameters.in, e.g.,
  
 25.5
-79.0
  1.0
1KM
1100
850
Florida

(b) Create a higher quality 1000 meter resolution image by using HKM instead of
1KM input data in map_parameters.in, e.g.,
  
 25.5
-79.0
  1.0
HKM
1100
850
Florida

(c) Speed up the corrected reflectance code by using more aggressive
optimization, e.g.,

gcc -O3 -funroll-all-loops -fomit-frame-pointer \
  -ffast-math -march=pentium4 -mfpmath=sse ...

6.0 END NOTES
-------------

(a) The current version of the software is limited to processing a single input
'scene' of MODIS data, whether the scene is a 5-minute DAAC granule, or a
direct broadcast pass of arbitrary size. A future version of the software will
be able to handle multiple input granules.

(b) The ability to overlay coastlines, political boundaries, city locations,
and other features will be added in a future version of the software.

(c) For a given set of input MODIS Level 1B data, the corrected reflectances
only need to be created once. If you wish to experiment with creating different
reprojected images from the same MODIS scene, simply move the call to the
corrected reflectance script (Crefl.csh) out of the sample run scripts
(Script.csh or Script_VM.csh).

(d) For examples of MODIS reprojected true color images created using the
code described here, please visit

http://terra.ssec.wisc.edu/~gumley/images.html

(e) For more information about IDL programming in general, please visit

http://www.gumley.com/
