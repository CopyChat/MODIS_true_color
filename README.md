# MODIS_true_color calculation
# une petite Instructions, ctang, Jeu 22 sep 2016 16:27:46 RET
==================================================

This file provides instructions for installing the required software.  
If you have any problems with the installation, please contact Chao.TANG
by email: chao.tang@univ-reunion.fr or official support page 
at the following location:

    https://modis.gsfc.nasa.gov

#CONTENTS
--------
        1. Obtaining HDF5
        2. Required softwares
        2.1. UNIX platforms
        2.2. HDF4 Library
        2.3. 



#****************************************************************************

1. General instruction
        The latest supported public release of HDF5 is available from
        ftp://ftp.hdfgroup.org/HDF5/current/src.  For Unix and UNIX-like 
        platforms, it is available in tar format compressed with gzip.  

        Attention:  All of the source code, scripts, and sample data files 
                    described in this document, as well as the latest version
                    of offical document, are available at the following FTP site:

                    ftp://ftp.ssec.wisc.edu/pub/IMAPP/MODIS/TrueColor/

                    You could start to downloand these data while reading 
                    these article. It takes time depending on your network.

2. Required softwares
2.1. UNIX platforms
        For those who don't like to use UNIX, c'est dommage pour Windows gay.

2.2. HDF4 Library 
        The HDF4 Library has to be builded, apart from hdf5. It's used to build
        NDVI in next section. To obtain the source code of HDF4, tu peux visiter:

            https://support.hdfgroup.org/release4/obtainsrc.html

        configure:

            ./configure --with-zlib=/usr/local/ --with-jpeg=/usr/local
            --with-szlib=/usr/local/ --prefix=/usr/local/
            --disable-netcdf

        Attention: "--disable-netcdf", c'est obligatoire to use HDF4 and HDF5
                    together.

                    To use the HDF/MFHDF libraries (libdf.a, libmfhdf.a) with the 
                    netCDF library (libnetcdf.a), the HDF4 distribution must be configured 
                    with the --disable-netcdf configuration flag. 

                    When this flag is used, the HDF versions of the C netCDF functions 
                    (as of netCDF version 2.3.2) are renamed from ncxxx to sd_ncxxx, 
                    and HDF Fortran netCDF wrappers are disabled to avoid name clashes with 
                    the netCDF C and Fortran functions from libnetcdf.a.

                    Please report all problems to help@hdfgroup.org.

2.3.MODIS Corrected Reflectance (look for “NDVI” at the following site):
    The code is in the ftp above.
        
        configure:  
                    make

2.4.ImageMagick
    That's easy. Maybe libjpeg, libpng are missing on your working platform, go ahead 
    and just install them. Then build the ImageMagick code depending on your platform:

        http://www.imagemagick.org/

        configure:  recommanded to build yourself, the binary executes do not work every time
                    ./configure 
                    make
                    make check
                    (sudo) make install
                    
2.5.Interactive Data Language (IDL):
            
            http://www.ittvis.com/idl/index.asp
            http://www.ittvis.com/download/download.asp

        If you do not have a license for IDL, you can still run the IDL Virtual Machine (VM) to
        run pre-compiled versions of the IDL software described in this document. The IDL VM
        is included in the IDL 6.0 distribution package available for download at the website
        mentioned above. Simply install the IDL 6.0 package on your system according to the
        instructions at the site above, and you will be able to run the example code via IDL VM.

        Attention: 
                    If you're working on Mac OS X, I could help with a licensed IDL7.1.

2.6.MODIS Swath to Grid Toolbox (MS2GT):

            http://nsidc.org/data/modis/ms2gt/

        I can't find this.







