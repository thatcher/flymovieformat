.. _fmf-format:

****************************************
FlyMovieFormat (.fmf) file specification
****************************************

This file type defines 8-bit grayscale image sequences where each
image is associated with a timestamp. There are currently two versions
implemented.

==============
File structure
==============

 * header (either version 1 or version 3)
 * arbitrary number of timestamp and frame pairs ("frame chunks")

.fmf header version 1
---------------------

======== ========= ===================================================
Typecode Name      Description
======== ========= ===================================================
I    	 version   Version number (1)
II   	 framesize Number of rows and columns in each frame
Q    	 chunksize Bytes per "chunk" (timestamp + frame)
Q    	 n_frames  Number of frames (0=unknown, read file to find out)
======== ========= ===================================================

.fmf header version 3
---------------------

======== ========= ===================================================
Typecode Name      Description
======== ========= ===================================================
I    	 version   Version number (3)
II   	 framesize Number of rows and columns in each frame
Q    	 chunksize Bytes per "chunk" (timestamp + frame)
Q    	 n_frames  Number of frames (0=unknown, read file to find out)
I        lenformat Length of the subsequent format string
*B       format    string containing format, e.g. 'MONO8' or 'YUV422'
I        bpp       Bits per pixel, e.g. 8
======== ========= ===================================================

.fmf frame chunks
-----------------

======== ========= ===================================================
d        timestamp Timestamp (seconds in current epoch)
*B       frame     Image data, rows*columns bytes, row major ordering
======== ========= ===================================================


Typecodes used above
--------------------

All numbers are little-endian (Intel standard).

======== =========== ===== =======================================
Typecode description bytes C type
======== =========== ===== =======================================
B    	 uint8       1	   unsigned char
I    	 uint32      4	   unsigned int
Q    	 uint64      8	   unsigned long long (__int64 on Windows)
d    	 double64    8	   double
======== =========== ===== =======================================