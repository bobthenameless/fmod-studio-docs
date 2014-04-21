Firelight Technologies FMOD Studio API

FSBank API
==========

[Functions](fsbank_api_functions.html)\
 [Callbacks](fsbank_api_callbacks.html)\
 [Structures](fsbank_api_structures.html)\
 [Defines](fsbank_api_defines.html)\
 [Enumerations](fsbank_api_enumerations.html)\
 Firelight Technologies FMOD Studio API

Callbacks
=========

[FSBANK\_MEMORY\_ALLOC\_CALLBACK](FSBANK_MEMORY_ALLOC_CALLBACK.html)\
 [FSBANK\_MEMORY\_FREE\_CALLBACK](FSBANK_MEMORY_FREE_CALLBACK.html)\

[FSBANK\_MEMORY\_REALLOC\_CALLBACK](FSBANK_MEMORY_REALLOC_CALLBACK.html)\
 Firelight Technologies FMOD Studio API

Defines
=======

[FSBANK\_BUILDFLAGS](FSBANK_BUILDFLAGS.html)\
 [FSBANK\_INITFLAGS](FSBANK_INITFLAGS.html)\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FSBANK\_FORMAT](FSBANK_FORMAT.html)\
 [FSBANK\_FSBVERSION](FSBANK_FSBVERSION.html)\
 [FSBANK\_RESULT](FSBANK_RESULT.html)\
 [FSBANK\_SPEAKERMAP](FSBANK_SPEAKERMAP.html)\
 [FSBANK\_STATE](FSBANK_STATE.html)\
 Firelight Technologies FMOD Studio API

Functions
=========

[FSBank\_Build](FSBank_Build.html)\
 [FSBank\_BuildCancel](FSBank_BuildCancel.html)\
 [FSBank\_FetchNextProgressItem](FSBank_FetchNextProgressItem.html)\
 [FSBank\_Init](FSBank_Init.html)\
 [FSBank\_MemoryGetStats](FSBank_MemoryGetStats.html)\
 [FSBank\_MemoryInit](FSBank_MemoryInit.html)\
 [FSBank\_Release](FSBank_Release.html)\
 [FSBank\_ReleaseProgressItem](FSBank_ReleaseProgressItem.html)\
 Firelight Technologies FMOD Studio API

Structures
==========

[FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)\
 [FSBANK\_STATEDATA\_FAILED](FSBANK_STATEDATA_FAILED.html)\
 [FSBANK\_STATEDATA\_WARNING](FSBANK_STATEDATA_WARNING.html)\
 [FSBANK\_SUBSOUND](FSBANK_SUBSOUND.html)\
 Firelight Technologies FMOD Studio API

FSBank\_Build
=============

Begin the building process for the provided subsound descriptions,
function will block until complete.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_Build(
  const FSBANK_SUBSOUND *subSounds,
  unsigned int numSubSounds,
  FSBANK_FORMAT encodeFormat,
  FSBANK_BUILDFLAGS buildFlags,
  unsigned int quality,
  const char *encryptKey,
  const char *outputFileName
);
```

Parameters
----------

*subSounds*

An array of subsound descriptions each defining one subsound for the
final FSB.

*numSubSounds*

The number of elements in the 'subSounds' array.

*encodeFormat*

The format to be used for encoding the FSB.

*buildFlags*

Building flags which control how the sample data is encoded.

*quality*

Controls the quality level after compression. From 1 (high compression /
low quality) to 100 (high quality / low compression), use 0 for default
quality. See remarks for format specific usage.

*encryptKey*

Optional string 'key' used to encrypt the FSB, same key is required at
runtime for decryption.

*outputFileName*

Name (and path) of the FSB to produce.

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 Remarks -------

-   **AT9** - Bitrate (Kbps) depends on channel count, quality [1 to
    100] maps linearly to the available options
    -   1ch = [36, 48, 60, 72, 84, 96]
    -   2ch = [72, 96, 120, 144, 168, 192]
-   **CELT** - Bitrate (Kbps) = FMOD quality \* 3.2
-   **MPEG** - Bitrate (Kbps) = FMOD quality \* 3.2
-   **Vorbis** - Vorbis quality [-0.1 to 1.0] maps linearly to FMOD
    quality [1 to 100]
-   **XMA** - XMA quality = FMOD quality
-   **xWMA** - Bitrate (Kbps) depends on sample rate and channel count,
    quality [1 to 100] maps linearly to the available options
    -   1ch 22KHz = [20]
    -   1ch 32KHz = [20]
    -   1ch 44KHz = [32, 48]
    -   2ch 22Khz = [32]
    -   2ch 32Khz = [32, 48]
    -   2ch 44KHz = [32, 48, 96, 192]
    -   2ch 48KHz = [48, 64, 96, 160, 192]
    -   6ch 44KHz = [96, 192]
    -   6ch 48KHz = [48, 192]

See Also
--------

-   [FSBANK\_SUBSOUND](FSBANK_SUBSOUND.html)
-   [FSBANK\_FORMAT](FSBANK_FORMAT.html)
-   [FSBANK\_BUILDFLAGS](FSBANK_BUILDFLAGS.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_BuildCancel
===================

Halt the build in progress, must be called from a different thread to
[FSBank\_Build](FSBank_Build.html).

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_BuildCancel();
```

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 See Also --------

-   [FSBank\_Build](FSBank_Build.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_BUILDFLAGS
==================

Bit fields to use with [FSBank\_Build](FSBank_Build.html) and in
[FSBANK\_SUBSOUND](FSBANK_SUBSOUND.html) to control how subsounds are
encoded.

### Definition

``` {.syntax}
#define FSBANK_BUILD_DEFAULT 0x00000000
#define FSBANK_BUILD_DISABLESYNCPOINTS 0x00000001
#define FSBANK_BUILD_DONTLOOP 0x00000002
#define FSBANK_BUILD_FILTERHIGHFREQ 0x00000004
#define FSBANK_BUILD_DISABLESEEKING 0x00000008
#define FSBANK_BUILD_OPTIMIZESAMPLERATE 0x00000010
#define FSBANK_BUILD_DONTINTERLEAVE 0x00000020
#define FSBANK_BUILD_FSB4_USEBASICHEADERS 0x00000040
#define FSBANK_BUILD_FSB5_DONTWRITENAMES 0x00000080
#define FSBANK_BUILD_NOGUID 0x00000100
#define FSBANK_BUILD_WRITEPEAKVOLUME 0x00000200
#define FSBANK_BUILD_OVERRIDE_MASK (FSBANK_BUILD_DISABLESYNCPOINTS | FSBANK_BUILD_DONTLOOP | FSBANK_BUILD_FILTERHIGHFREQ | FSBANK_BUILD_DISABLESEEKING | FSBANK_BUILD_OPTIMIZESAMPLERATE | FSBANK_BUILD_DONTINTERLEAVE | FSBANK_BUILD_WRITEPEAKVOLUME)
#define FSBANK_BUILD_CACHE_VALIDATION_MASK (FSBANK_BUILD_DONTLOOP | FSBANK_BUILD_FILTERHIGHFREQ | FSBANK_BUILD_OPTIMIZESAMPLERATE | FSBANK_BUILD_DONTINTERLEAVE)
```

Values
------

*FSBANK\_BUILD\_DEFAULT*

Build with default settings.

*FSBANK\_BUILD\_DISABLESYNCPOINTS*

Disable the storing of syncpoints in the output

*FSBANK\_BUILD\_DONTLOOP*

Disable perfect loop encoding and sound stretching. Removes chirps from
the start of oneshot MP2, MP3 and IMAADPCM sounds.

*FSBANK\_BUILD\_FILTERHIGHFREQ*

XMA only. Enable high frequency filtering.

*FSBANK\_BUILD\_DISABLESEEKING*

XMA only. Disable seek tables to save memory.

*FSBANK\_BUILD\_OPTIMIZESAMPLERATE*

Attempt to optimize the sample rate down. Ignored if format is MP2, MP3
or CELT or if FSB4 basic headers flag is used.

*FSBANK\_BUILD\_DONTINTERLEAVE*

VAG and GCADPCM only. Don't interleave the data as LRLRLRLR... instead
use LLLLRRRR type encoding. Speeds up loading for samples (not streams,
streams must remained interleaved), allows
[FMOD\_OPENMEMORY\_POINT](FMOD_MODE.html).

*FSBANK\_BUILD\_FSB4\_USEBASICHEADERS*

FSB4 format only. Generate FSBs with small sample header data. They only
contain basic information such as sample length, and everything else has
its attributes inherited from the first sample (for example the default
frequency).

*FSBANK\_BUILD\_FSB5\_DONTWRITENAMES*

FSB5 format only. Do not write out a names chunk to the FSB to reduce
file size.

*FSBANK\_BUILD\_NOGUID*

FSB5 format only. Write out a null GUID for the FSB header. The runtime
will not use header caching for these FSB files.

*FSBANK\_BUILD\_WRITEPEAKVOLUME*

FSB5 format only. Write peak volume for all subsounds.

*FSBANK\_BUILD\_OVERRIDE\_MASK*

Build flag mask that specifies which settings can be overridden per
subsound.

*FSBANK\_BUILD\_CACHE\_VALIDATION\_MASK*

Build flag mask that specifies which settings (when changed) invalidate
a cache file.

See Also
--------

-   [FSBank\_Init](FSBank_Init.html)
-   [FSBANK\_SUBSOUND](FSBANK_SUBSOUND.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_FetchNextProgressItem
=============================

Fetch build progress items that describe the current state of the build.
Can be called while the build is in progress to get realtime updates or
after the build for a report. Call
[FSBank\_ReleaseProgressItem](FSBank_ReleaseProgressItem.html) to free
allocated memory.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_FetchNextProgressItem(
  const FSBANK_PROGRESSITEM **progressItem
);
```

Parameters
----------

*progressItem*

One status update about the progress of a particular subsound.

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 See Also --------

-   [FSBank\_ReleaseProgressItem](FSBank_ReleaseProgressItem.html)
-   [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_FORMAT
==============

Compression formats available for encoding

### Enumeration

``` {.syntax}
typedef enum {
  FSBANK_FORMAT_PCM,
  FSBANK_FORMAT_PCM_BIGENDIAN,
  FSBANK_FORMAT_IMAADPCM,
  FSBANK_FORMAT_MP2,
  FSBANK_FORMAT_MP3,
  FSBANK_FORMAT_XMA,
  FSBANK_FORMAT_CELT,
  FSBANK_FORMAT_AT9_PSVITA,
  FSBANK_FORMAT_AT9_PS4,
  FSBANK_FORMAT_XWMA,
  FSBANK_FORMAT_VORBIS,
  FSBANK_FORMAT_MAX
} FSBANK_FORMAT;
```

Values
------

*FSBANK\_FORMAT\_PCM*

PCM (1:1) All platforms.

*FSBANK\_FORMAT\_PCM\_BIGENDIAN*

PCM Big Endian (1:1) Xbox360 and PS3 only.

*FSBANK\_FORMAT\_IMAADPCM*

IMA ADPCM (3.5:1) All platforms.

*FSBANK\_FORMAT\_MP2*

MPEG Layer 2 (CBR) All platforms except PS3. Depends on toolame.

*FSBANK\_FORMAT\_MP3*

MPEG Layer 3 (CBR) All platforms. Depends on libmp3lame.

*FSBANK\_FORMAT\_XMA*

XMA (VBR) Xbox360 only (hardware). Depends on xmaencoder.

*FSBANK\_FORMAT\_CELT*

Constrained Energy Lapped Transform (CBR) All platforms. Depends on
celt\_encoder.

*FSBANK\_FORMAT\_AT9\_PSVITA*

ATRAC9 (CBR) PSVita only (hardware). Depends on libatrac9.

*FSBANK\_FORMAT\_AT9\_PS4*

ATRAC9 (CBR) PS4 only (hardware). Depends on libatrac9.

*FSBANK\_FORMAT\_XWMA*

XWMA (VBR) Xbox360 only. Depends on xwmaencoder.

*FSBANK\_FORMAT\_VORBIS*

Vorbis (VBR) All platforms. Depends on libvorbis.

*FSBANK\_FORMAT\_MAX*

Upper bound for this enumeration, for use with validation.

See Also
--------

-   [FSBank\_Build](FSBank_Build.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_FSBVERSION
==================

Version of FSB to write out.

### Enumeration

``` {.syntax}
typedef enum {
  FSBANK_FSBVERSION_FSB5,
  FSBANK_FSBVERSION_MAX
} FSBANK_FSBVERSION;
```

Values
------

*FSBANK\_FSBVERSION\_FSB5*

Produce FSB version 5 files.

*FSBANK\_FSBVERSION\_MAX*

Upper bound for this enumeration, for use with validation.

See Also
--------

-   [FSBank\_Init](FSBank_Init.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_Init
============

Initialize the FSBank system.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_Init(
  FSBANK_FSBVERSION version,
  FSBANK_INITFLAGS flags,
  unsigned int numSimultaneousJobs,
  const char *cacheDirectory
);
```

Parameters
----------

*version*

FSB version, currently only
[FSBANK\_FSBVERSION\_FSB5](FSBANK_FSBVERSION.html) is supported.

*flags*

Initialization flags which control how the system behaves.

*numSimultaneousJobs*

The maximum number of threads to create for parallel encoding. Set this
to your number of CPU 'cores' for best performance.

*cacheDirectory*

Optional location to store the temporary cache files, default is a
directory off the current working directory.

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 See Also --------

-   [FSBANK\_FSBVERSION](FSBANK_FSBVERSION.html)
-   [FSBANK\_INITFLAGS](FSBANK_INITFLAGS.html)
-   [FSBank\_Release](FSBank_Release.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_INITFLAGS
=================

Bit fields to use with [FSBank\_Init](FSBank_Init.html) to control the
general operation of the library.

### Definition

``` {.syntax}
#define FSBANK_INIT_NORMAL 0x00000000
#define FSBANK_INIT_IGNOREERRORS 0x00000001
#define FSBANK_INIT_WARNINGSASERRORS 0x00000002
#define FSBANK_INIT_CREATEINCLUDEHEADER 0x00000004
#define FSBANK_INIT_DONTLOADCACHEFILES 0x00000008
#define FSBANK_INIT_GENERATEPROGRESSITEMS 0x00000010
#define FSBANK_INIT_UNICODE 0x00000020
```

Values
------

*FSBANK\_INIT\_NORMAL*

Initialize normally.

*FSBANK\_INIT\_IGNOREERRORS*

Ignore individual subsound build errors, continue building for as long
as possible.

*FSBANK\_INIT\_WARNINGSASERRORS*

Treat any warnings issued as errors.

*FSBANK\_INIT\_CREATEINCLUDEHEADER*

Create C header files with \#defines defining indices for each member of
the FSB.

*FSBANK\_INIT\_DONTLOADCACHEFILES*

Ignore existing cache files.

*FSBANK\_INIT\_GENERATEPROGRESSITEMS*

Generate status items that can be queried by another thread to monitor
the build progress and give detailed error messages.

*FSBANK\_INIT\_UNICODE*

All file paths are treated as wide chars (Windows only).

See Also
--------

-   [FSBank\_Init](FSBank_Init.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_MemoryGetStats
======================

Query the current and maximum memory usage of the FSBank system.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_MemoryGetStats(
  unsigned int *currentAllocated,
  unsigned int *maximumAllocated
);
```

Parameters
----------

*currentAllocated*

Address of a variable that receives the currently allocated memory at
time of call. Optional. Specify 0 or NULL to ignore.

*maximumAllocated*

Address of a variable that receives the maximum allocated memory since
[FSBank\_Init](FSBank_Init.html). Optional. Specify 0 or NULL to ignore.

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_MemoryInit
==================

Specifies a method for FSBank to allocate memory through callbacks.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_MemoryInit(
  FSBANK_MEMORY_ALLOC_CALLBACK userAlloc,
  FSBANK_MEMORY_REALLOC_CALLBACK userRealloc,
  FSBANK_MEMORY_FREE_CALLBACK userFree
);
```

Parameters
----------

*userAlloc*

Overrides the internal calls to alloc. Compatible with ANSI malloc().

*userRealloc*

Overrides the internal calls to realloc. Compatible with ANSI realloc().

*userFree*

Overrides the internal calls to free. Compatible with ANSI free().

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 See Also --------

-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK](FSBANK_MEMORY_ALLOC_CALLBACK.html)
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK](FSBANK_MEMORY_REALLOC_CALLBACK.html)
-   [FSBANK\_MEMORY\_FREE\_CALLBACK](FSBANK_MEMORY_FREE_CALLBACK.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_MEMORY\_ALLOC\_CALLBACK
===============================

Callback to allocate a block of memory.

### C/C++ Syntax

``` {.syntax}
void * FSBANK_CALLBACK FSBANK_MEMORY_ALLOC_CALLBACK(
  unsigned int size,
  unsigned int type,
  const char *sourceStr
);
```

Parameters
----------

*size*

Size in bytes of the memory block to be allocated and returned.

*type*

Type of memory allocation.

*sourceStr*

Only valid (not null) in logging versions of FMOD. Gives a string with
the fmod source code filename and line number in it, for better resource
tracking.

Return Values
-------------

On success, a pointer to the newly allocated block of memory is
returned.\
 On failure, NULL is returned.\
\
 Remarks -------

Returning an aligned pointer, of 16 byte alignment is recommended for
speed purposes.

See Also
--------

-   [FSBank\_MemoryInit](FSBank_MemoryInit.html)
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK](FSBANK_MEMORY_REALLOC_CALLBACK.html)
-   [FSBANK\_MEMORY\_FREE\_CALLBACK](FSBANK_MEMORY_FREE_CALLBACK.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_MEMORY\_FREE\_CALLBACK
==============================

Callback to free a block of memory.

### C/C++ Syntax

``` {.syntax}
void FSBANK_CALLBACK FSBANK_MEMORY_FREE_CALLBACK(
  void *ptr,
  unsigned int type,
  const char *sourceStr
);
```

Parameters
----------

*ptr*

Pointer to a pre-existing block of memory to be freed.

*type*

Type of memory to be freed.

*sourceStr*

Only valid (not null) in logging versions of FMOD. Gives a string with
the fmod source code filename and line number in it, for better resource
tracking.

Return Values
-------------

void\
\
 See Also --------

-   [FSBank\_MemoryInit](FSBank_MemoryInit.html)
-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK](FSBANK_MEMORY_ALLOC_CALLBACK.html)
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK](FSBANK_MEMORY_REALLOC_CALLBACK.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_MEMORY\_REALLOC\_CALLBACK
=================================

Callback to re-allocate a block of memory to a different size.

### C/C++ Syntax

``` {.syntax}
void * FSBANK_CALLBACK FSBANK_MEMORY_REALLOC_CALLBACK(
  void *ptr,
  unsigned int size,
  char *sourceStr
);
```

Parameters
----------

*ptr*

Pointer to a block of memory to be resized. If this is NULL then a new
block of memory is simply allocated.

*size*

Size of the memory to be reallocated. The original memory must be
preserved.

*sourceStr*

Only valid (not null) in logging versions of FMOD. Gives a string with
the fmod source code filename and line number in it, for better resource
tracking.

Return Values
-------------

On success, a pointer to the newly re-allocated block of memory is
returned.\
 On failure, NULL is returned.\
\
 Remarks -------

Returning an aligned pointer, of 16 byte alignment is recommended for
speed purposes.

See Also
--------

-   [FSBank\_MemoryInit](FSBank_MemoryInit.html)
-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK](FSBANK_MEMORY_ALLOC_CALLBACK.html)
-   [FSBANK\_MEMORY\_FREE\_CALLBACK](FSBANK_MEMORY_FREE_CALLBACK.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_PROGRESSITEM
====================

Status information describing the progress of a build.

### Structure

``` {.syntax}
typedef struct {
  int subSoundIndex;
  int threadIndex;
  FSBANK_STATE state;
  const void *stateData;
} FSBANK_PROGRESSITEM;
```

Members
-------

*subSoundIndex*

Index into the subsound list passed to
[FSBank\_Build](FSBank_Build.html) that this update relates to (-1
indicates no specific subsound).

*threadIndex*

Which thread index is serving this update (-1 indicates
[FSBank\_Build](FSBank_Build.html) / main thread).

*state*

Progress through the encoding process.

*stateData*

Cast to state specific data structure for extra information.

See Also
--------

-   [FSBank\_Build](FSBank_Build.html)
-   [FSBank\_FetchNextProgressItem](FSBank_FetchNextProgressItem.html)
-   [FSBank\_ReleaseProgressItem](FSBank_ReleaseProgressItem.html)
-   [FSBANK\_STATE](FSBANK_STATE.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_Release
===============

Release the FSBank system, clean up used resources.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_Release();
```

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 Remarks -------

All progress items retrieved with
[FSBank\_FetchNextProgressItem](FSBank_FetchNextProgressItem.html) will
be released by this function.

See Also
--------

-   [FSBank\_Init](FSBank_Init.html)
-   [FSBank\_FetchNextProgressItem](FSBank_FetchNextProgressItem.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_ReleaseProgressItem
===========================

Release memory associated with a progress item.

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_ReleaseProgressItem(
  const FSBANK_PROGRESSITEM *progressItem
);
```

Parameters
----------

*progressItem*

One status update about the progress of a particular subsound.

Return Values
-------------

If the function succeeds then the return value is
[FSBANK\_OK](fsbank_result.html).\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT](fsbank_result.html) enumeration.\
 See Also --------

-   [FSBank\_FetchNextProgressItem](FSBank_FetchNextProgressItem.html)
-   [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_RESULT
==============

Error codes returned from every function.

### Enumeration

``` {.syntax}
typedef enum {
  FSBANK_OK,
  FSBANK_ERR_CACHE_CHUNKNOTFOUND,
  FSBANK_ERR_CANCELLED,
  FSBANK_ERR_CANNOT_CONTINUE,
  FSBANK_ERR_ENCODER,
  FSBANK_ERR_ENCODER_INIT,
  FSBANK_ERR_ENCODER_NOTSUPPORTED,
  FSBANK_ERR_FILE_OS,
  FSBANK_ERR_FILE_NOTFOUND,
  FSBANK_ERR_FMOD,
  FSBANK_ERR_INITIALIZED,
  FSBANK_ERR_INVALID_FORMAT,
  FSBANK_ERR_INVALID_FORMAT_PCMBITS,
  FSBANK_ERR_INVALID_PARAM,
  FSBANK_ERR_MEMORY,
  FSBANK_ERR_UNINITIALIZED,
  FSBANK_ERR_WRITER_FORMAT,
  FSBANK_WARN_CANNOTLOOP,
  FSBANK_WARN_IGNORED_OPTIMIZESAMPLERATE,
  FSBANK_WARN_IGNORED_FILTERHIGHFREQ,
  FSBANK_WARN_IGNORED_DISABLESEEKING,
  FSBANK_WARN_IGNORED_DONTINTERLEAVE
} FSBANK_RESULT;
```

Values
------

*FSBANK\_OK*

No errors.

*FSBANK\_ERR\_CACHE\_CHUNKNOTFOUND*

An expected chunk is missing from the cache, perhaps try deleting cache
files.

*FSBANK\_ERR\_CANCELLED*

The build process was cancelled during compilation by the user.

*FSBANK\_ERR\_CANNOT\_CONTINUE*

The build process cannot continue due to previously ignored errors.

*FSBANK\_ERR\_ENCODER*

Encoder for chosen format has encountered an unexpected error.

*FSBANK\_ERR\_ENCODER\_INIT*

Encoder initialization failed.

*FSBANK\_ERR\_ENCODER\_NOTSUPPORTED*

Encoder for chosen format is not supported on this platform.

*FSBANK\_ERR\_FILE\_OS*

An operating system based file error was encountered.

*FSBANK\_ERR\_FILE\_NOTFOUND*

A specified file could not be found.

*FSBANK\_ERR\_FMOD*

Internal error from FMOD sub-system.

*FSBANK\_ERR\_INITIALIZED*

Already initialized.

*FSBANK\_ERR\_INVALID\_FORMAT*

The format of the source file is invalid, see output for details.

*FSBANK\_ERR\_INVALID\_FORMAT\_PCMBITS*

The format of the source file is invalid, the source bit formats (i.e.
PCM8, PCM16, etc) must match for all sub-sounds

*FSBANK\_ERR\_INVALID\_PARAM*

An invalid parameter has been passed to this function.

*FSBANK\_ERR\_MEMORY*

Ran out of memory.

*FSBANK\_ERR\_UNINITIALIZED*

Not initialized yet.

*FSBANK\_ERR\_WRITER\_FORMAT*

Chosen encode format is not supported by this FSB version.

*FSBANK\_WARN\_CANNOTLOOP*

Source file is too short for seamless looping. Looping disabled.

*FSBANK\_WARN\_IGNORED\_OPTIMIZESAMPLERATE*

[FSBANK\_BUILD\_OPTIMIZESAMPLERATE](FSBANK_BUILDFLAGS.html) flag
ignored: MP2, MP3 and CELT formats, and the USEBASICHEADERS flag make
this option irrelevant.

*FSBANK\_WARN\_IGNORED\_FILTERHIGHFREQ*

[FSBANK\_BUILD\_FILTERHIGHFREQ](FSBANK_BUILDFLAGS.html) flag ignored:
feature only supported by XMA format.

*FSBANK\_WARN\_IGNORED\_DISABLESEEKING*

[FSBANK\_BUILD\_DISABLESEEKING](FSBANK_BUILDFLAGS.html) flag ignored:
feature only supported by XMA format.

*FSBANK\_WARN\_IGNORED\_DONTINTERLEAVE*

[FSBANK\_BUILD\_DONTINTERLEAVE](FSBANK_BUILDFLAGS.html) flag ignored:
feature only supported by VAG and GCADPCM formats.

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_SPEAKERMAP
==================

Speaker maps to define the layout of multichannel subsounds.

### Enumeration

``` {.syntax}
typedef enum {
  FSBANK_SPEAKERMAP_DEFAULT,
  FSBANK_SPEAKERMAP_ALLMONO,
  FSBANK_SPEAKERMAP_ALLSTEREO,
  FSBANK_SPEAKERMAP_PROTOOLS,
  FSBANK_SPEAKERMAP_MAX
} FSBANK_SPEAKERMAP;
```

Values
------

*FSBANK\_SPEAKERMAP\_DEFAULT*

Sample uses default FMOD speaker mapping.

*FSBANK\_SPEAKERMAP\_ALLMONO*

Sample is a collection of mono channels.

*FSBANK\_SPEAKERMAP\_ALLSTEREO*

Sample is a collection of stereo channel pairs.

*FSBANK\_SPEAKERMAP\_PROTOOLS*

Sample is 6ch and uses L C R LS RS LFE standard.

*FSBANK\_SPEAKERMAP\_MAX*

Upper bound for this enumeration, for use with validation.

See Also
--------

-   [FSBANK\_SUBSOUND](FSBANK_SUBSOUND.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_STATE
=============

Current state during the build process.

### Enumeration

``` {.syntax}
typedef enum {
  FSBANK_STATE_DECODING,
  FSBANK_STATE_ANALYSING,
  FSBANK_STATE_PREPROCESSING,
  FSBANK_STATE_ENCODING,
  FSBANK_STATE_WRITING,
  FSBANK_STATE_FINISHED,
  FSBANK_STATE_FAILED,
  FSBANK_STATE_WARNING
} FSBANK_STATE;
```

Values
------

*FSBANK\_STATE\_DECODING*

Decode a file to usable raw sample data.

*FSBANK\_STATE\_ANALYSING*

Scan sound data for details (such as optimized sample rate).

*FSBANK\_STATE\_PREPROCESSING*

Prepares sound data for encoder.

*FSBANK\_STATE\_ENCODING*

Pass the sample data to the chosen encoder.

*FSBANK\_STATE\_WRITING*

Write encoded data into an FSB.

*FSBANK\_STATE\_FINISHED*

Process complete.

*FSBANK\_STATE\_FAILED*

An error has occurred, check data (as
[FSBANK\_STATEDATA\_FAILED](FSBANK_STATEDATA_FAILED.html)) for details.

*FSBANK\_STATE\_WARNING*

A warning has been issued, check data (as
[FSBANK\_STATEDATA\_WARNING](FSBANK_STATEDATA_WARNING.html)) for
details.

See Also
--------

-   [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_STATEDATA\_FAILED
=========================

Extra state data for [FSBANK\_STATE\_FAILED](FSBANK_STATE.html)

### Structure

``` {.syntax}
typedef struct {
  FSBANK_RESULT errorCode;
  char errorString[256];
} FSBANK_STATEDATA_FAILED;
```

Members
-------

*errorCode*

Error result code.

*errorString*

Description for error code.

Remarks
-------

Cast stateData in [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html) to
this struct if the state is [FSBANK\_STATE\_FAILED](FSBANK_STATE.html)

See Also
--------

-   [FSBANK\_STATE\_FAILED](FSBANK_STATE.html)
-   [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_STATEDATA\_WARNING
==========================

Extra state data for
[FSBANK\_STATEDATA\_WARNING](FSBANK_STATEDATA_WARNING.html)

### Structure

``` {.syntax}
typedef struct {
  FSBANK_RESULT warnCode;
  char warningString[256];
} FSBANK_STATEDATA_WARNING;
```

Members
-------

*warnCode*

Warning result code.

*warningString*

Description for warning code.

Remarks
-------

Cast stateData in [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html) to
this struct if the state is [FSBANK\_STATE\_WARNING](FSBANK_STATE.html)

See Also
--------

-   [FSBANK\_STATE\_WARNING](FSBANK_STATE.html)
-   [FSBANK\_PROGRESSITEM](FSBANK_PROGRESSITEM.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_SUBSOUND
================

Representation of how to encode a single subsound in the final FSB.

### Structure

``` {.syntax}
typedef struct {
  const char* const *fileNames;
  unsigned int numFileNames;
  FSBANK_SPEAKERMAP speakerMap;
  FSBANK_BUILDFLAGS overrideFlags;
  unsigned int overrideQuality;
  float desiredSampleRate;
  float percentOptimizedRate;
} FSBANK_SUBSOUND;
```

Members
-------

*fileNames*

List of file names used to produce an interleaved sound.

*numFileNames*

Number of files in above file name list, up to 16.

*speakerMap*

Setting to define the mapping and order of channels.

*overrideFlags*

Flags that will reverse the equivalent flags passed to
[FSBank\_Build](FSBank_Build.html).

*overrideQuality*

Override the quality setting passed to
[FSBank\_Build](FSBank_Build.html).

*desiredSampleRate*

Resample to this sample rate (ignores optimize sample rate setting), up
to 192000Hz.

*percentOptimizedRate*

If using [FSBANK\_BUILD\_OPTIMIZESAMPLERATE](FSBANK_BUILDFLAGS.html),
this is the percentage of that rate to be used, up to 100.0%.

See Also
--------

-   [FSBank\_Build](FSBank_Build.html)
-   [FSBANK\_BUILD\_OPTIMIZESAMPLERATE](FSBANK_BUILDFLAGS.html)
-   [FSBANK\_SPEAKERMAP](FSBANK_SPEAKERMAP.html)
-   [FSBANK\_BUILDFLAGS](FSBANK_BUILDFLAGS.html)

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\

Firelight Technologies FMOD Studio API

Low Level API
=============

[C++ interfaces](lowlevel_api_interfaces.html)\
 [Functions](lowlevel_api_functions.html)\
 [Callbacks](lowlevel_api_callbacks.html)\
 [Structures](lowlevel_api_structures.html)\
 [Defines](lowlevel_api_defines.html)\
 [Enumerations](lowlevel_api_enumerations.html)\
 Firelight Technologies FMOD Studio API

Callbacks
=========

[FMOD\_3D\_ROLLOFF\_CALLBACK](FMOD_3D_ROLLOFF_CALLBACK.html)\
 [FMOD\_CHANNELCONTROL\_CALLBACK](FMOD_CHANNELCONTROL_CALLBACK.html)\
 [FMOD\_CODEC\_CLOSE\_CALLBACK](FMOD_CODEC_CLOSE_CALLBACK.html)\
 [FMOD\_CODEC\_GETLENGTH\_CALLBACK](FMOD_CODEC_GETLENGTH_CALLBACK.html)\

[FMOD\_CODEC\_GETPOSITION\_CALLBACK](FMOD_CODEC_GETPOSITION_CALLBACK.html)\
 [FMOD\_CODEC\_METADATA\_CALLBACK](FMOD_CODEC_METADATA_CALLBACK.html)\
 [FMOD\_CODEC\_OPEN\_CALLBACK](FMOD_CODEC_OPEN_CALLBACK.html)\
 [FMOD\_CODEC\_READ\_CALLBACK](FMOD_CODEC_READ_CALLBACK.html)\

[FMOD\_CODEC\_SETPOSITION\_CALLBACK](FMOD_CODEC_SETPOSITION_CALLBACK.html)\

[FMOD\_CODEC\_SOUNDCREATE\_CALLBACK](FMOD_CODEC_SOUNDCREATE_CALLBACK.html)\
 [FMOD\_DSP\_CREATE\_CALLBACK](FMOD_DSP_CREATE_CALLBACK.html)\
 [FMOD\_DSP\_DIALOG\_CALLBACK](FMOD_DSP_DIALOG_CALLBACK.html)\

[FMOD\_DSP\_GETPARAM\_BOOL\_CALLBACK](FMOD_DSP_GETPARAM_BOOL_CALLBACK.html)\

[FMOD\_DSP\_GETPARAM\_DATA\_CALLBACK](FMOD_DSP_GETPARAM_DATA_CALLBACK.html)\

[FMOD\_DSP\_GETPARAM\_FLOAT\_CALLBACK](FMOD_DSP_GETPARAM_FLOAT_CALLBACK.html)\

[FMOD\_DSP\_GETPARAM\_INT\_CALLBACK](FMOD_DSP_GETPARAM_INT_CALLBACK.html)\
 [FMOD\_DSP\_PROCESS\_CALLBACK](FMOD_DSP_PROCESS_CALLBACK.html)\
 [FMOD\_DSP\_READ\_CALLBACK](FMOD_DSP_READ_CALLBACK.html)\
 [FMOD\_DSP\_RELEASE\_CALLBACK](FMOD_DSP_RELEASE_CALLBACK.html)\
 [FMOD\_DSP\_RESET\_CALLBACK](FMOD_DSP_RESET_CALLBACK.html)\

[FMOD\_DSP\_SETPARAM\_BOOL\_CALLBACK](FMOD_DSP_SETPARAM_BOOL_CALLBACK.html)\

[FMOD\_DSP\_SETPARAM\_DATA\_CALLBACK](FMOD_DSP_SETPARAM_DATA_CALLBACK.html)\

[FMOD\_DSP\_SETPARAM\_FLOAT\_CALLBACK](FMOD_DSP_SETPARAM_FLOAT_CALLBACK.html)\

[FMOD\_DSP\_SETPARAM\_INT\_CALLBACK](FMOD_DSP_SETPARAM_INT_CALLBACK.html)\
 [FMOD\_DSP\_SETPOSITION\_CALLBACK](FMOD_DSP_SETPOSITION_CALLBACK.html)\

[FMOD\_DSP\_SHOULDIPROCESS\_CALLBACK](FMOD_DSP_SHOULDIPROCESS_CALLBACK.html)\

[FMOD\_FILE\_ASYNCCANCEL\_CALLBACK](FMOD_FILE_ASYNCCANCEL_CALLBACK.html)\
 [FMOD\_FILE\_ASYNCREAD\_CALLBACK](FMOD_FILE_ASYNCREAD_CALLBACK.html)\
 [FMOD\_FILE\_CLOSE\_CALLBACK](FMOD_FILE_CLOSE_CALLBACK.html)\
 [FMOD\_FILE\_OPEN\_CALLBACK](FMOD_FILE_OPEN_CALLBACK.html)\
 [FMOD\_FILE\_READ\_CALLBACK](FMOD_FILE_READ_CALLBACK.html)\
 [FMOD\_FILE\_SEEK\_CALLBACK](FMOD_FILE_SEEK_CALLBACK.html)\
 [FMOD\_MEMORY\_ALLOC\_CALLBACK](FMOD_MEMORY_ALLOC_CALLBACK.html)\
 [FMOD\_MEMORY\_FREE\_CALLBACK](FMOD_MEMORY_FREE_CALLBACK.html)\
 [FMOD\_MEMORY\_REALLOC\_CALLBACK](FMOD_MEMORY_REALLOC_CALLBACK.html)\
 [FMOD\_OUTPUT\_CLOSE\_CALLBACK](FMOD_OUTPUT_CLOSE_CALLBACK.html)\

[FMOD\_OUTPUT\_GETDRIVERINFO\_CALLBACK](FMOD_OUTPUT_GETDRIVERINFO_CALLBACK.html)\

[FMOD\_OUTPUT\_GETHANDLE\_CALLBACK](FMOD_OUTPUT_GETHANDLE_CALLBACK.html)\

[FMOD\_OUTPUT\_GETNUMDRIVERS\_CALLBACK](FMOD_OUTPUT_GETNUMDRIVERS_CALLBACK.html)\

[FMOD\_OUTPUT\_GETPOSITION\_CALLBACK](FMOD_OUTPUT_GETPOSITION_CALLBACK.html)\
 [FMOD\_OUTPUT\_INIT\_CALLBACK](FMOD_OUTPUT_INIT_CALLBACK.html)\
 [FMOD\_OUTPUT\_LOCK\_CALLBACK](FMOD_OUTPUT_LOCK_CALLBACK.html)\
 [FMOD\_OUTPUT\_READFROMMIXER](FMOD_OUTPUT_READFROMMIXER.html)\
 [FMOD\_OUTPUT\_UNLOCK\_CALLBACK](FMOD_OUTPUT_UNLOCK_CALLBACK.html)\
 [FMOD\_OUTPUT\_UPDATE\_CALLBACK](FMOD_OUTPUT_UPDATE_CALLBACK.html)\
 [FMOD\_SOUND\_NONBLOCK\_CALLBACK](FMOD_SOUND_NONBLOCK_CALLBACK.html)\
 [FMOD\_SOUND\_PCMREAD\_CALLBACK](FMOD_SOUND_PCMREAD_CALLBACK.html)\
 [FMOD\_SOUND\_PCMSETPOS\_CALLBACK](FMOD_SOUND_PCMSETPOS_CALLBACK.html)\
 [FMOD\_SYSTEM\_CALLBACK](FMOD_SYSTEM_CALLBACK.html)\
 Firelight Technologies FMOD Studio API

Channel
=======

Functions
---------

[Channel::addDSP](FMOD_Channel_AddDSP.html)\
 [Channel::addFadePoint](FMOD_Channel_AddFadePoint.html)\
 [Channel::get3DAttributes](FMOD_Channel_Get3DAttributes.html)\

[Channel::get3DConeOrientation](FMOD_Channel_Get3DConeOrientation.html)\
 [Channel::get3DConeSettings](FMOD_Channel_Get3DConeSettings.html)\
 [Channel::get3DCustomRolloff](FMOD_Channel_Get3DCustomRolloff.html)\
 [Channel::get3DDistanceFilter](FMOD_Channel_Get3DDistanceFilter.html)\
 [Channel::get3DDopplerLevel](FMOD_Channel_Get3DDopplerLevel.html)\
 [Channel::get3DLevel](FMOD_Channel_Get3DLevel.html)\
 [Channel::get3DMinMaxDistance](FMOD_Channel_Get3DMinMaxDistance.html)\
 [Channel::get3DOcclusion](FMOD_Channel_Get3DOcclusion.html)\
 [Channel::get3DSpread](FMOD_Channel_Get3DSpread.html)\
 [Channel::getAudibility](FMOD_Channel_GetAudibility.html)\
 [Channel::getChannelGroup](FMOD_Channel_GetChannelGroup.html)\
 [Channel::getCurrentSound](FMOD_Channel_GetCurrentSound.html)\
 [Channel::getDSP](FMOD_Channel_GetDSP.html)\
 [Channel::getDSPClock](FMOD_Channel_GetDSPClock.html)\
 [Channel::getDelay](FMOD_Channel_GetDelay.html)\
 [Channel::getFadePoints](FMOD_Channel_GetFadePoints.html)\
 [Channel::getFrequency](FMOD_Channel_GetFrequency.html)\
 [Channel::getIndex](FMOD_Channel_GetIndex.html)\
 [Channel::getLoopCount](FMOD_Channel_GetLoopCount.html)\
 [Channel::getLoopPoints](FMOD_Channel_GetLoopPoints.html)\
 [Channel::getLowPassGain](FMOD_Channel_GetLowPassGain.html)\
 [Channel::getMixMatrix](FMOD_Channel_GetMixMatrix.html)\
 [Channel::getMode](FMOD_Channel_GetMode.html)\
 [Channel::getMute](FMOD_Channel_GetMute.html)\
 [Channel::getNumDSPs](FMOD_Channel_GetNumDSPs.html)\
 [Channel::getPaused](FMOD_Channel_GetPaused.html)\
 [Channel::getPitch](FMOD_Channel_GetPitch.html)\
 [Channel::getPosition](FMOD_Channel_GetPosition.html)\
 [Channel::getPriority](FMOD_Channel_GetPriority.html)\
 [Channel::getReverbProperties](FMOD_Channel_GetReverbProperties.html)\
 [Channel::getSystemObject](FMOD_Channel_GetSystemObject.html)\
 [Channel::getUserData](FMOD_Channel_GetUserData.html)\
 [Channel::getVolume](FMOD_Channel_GetVolume.html)\
 [Channel::getVolumeRamp](FMOD_Channel_GetVolumeRamp.html)\
 [Channel::isPlaying](FMOD_Channel_IsPlaying.html)\
 [Channel::isVirtual](FMOD_Channel_IsVirtual.html)\
 [Channel::removeDSP](FMOD_Channel_RemoveDSP.html)\
 [Channel::removeFadePoints](FMOD_Channel_RemoveFadePoints.html)\
 [Channel::set3DAttributes](FMOD_Channel_Set3DAttributes.html)\

[Channel::set3DConeOrientation](FMOD_Channel_Set3DConeOrientation.html)\
 [Channel::set3DConeSettings](FMOD_Channel_Set3DConeSettings.html)\
 [Channel::set3DCustomRolloff](FMOD_Channel_Set3DCustomRolloff.html)\
 [Channel::set3DDistanceFilter](FMOD_Channel_Set3DDistanceFilter.html)\
 [Channel::set3DDopplerLevel](FMOD_Channel_Set3DDopplerLevel.html)\
 [Channel::set3DLevel](FMOD_Channel_Set3DLevel.html)\
 [Channel::set3DMinMaxDistance](FMOD_Channel_Set3DMinMaxDistance.html)\
 [Channel::set3DOcclusion](FMOD_Channel_Set3DOcclusion.html)\
 [Channel::set3DSpread](FMOD_Channel_Set3DSpread.html)\
 [Channel::setCallback](FMOD_Channel_SetCallback.html)\
 [Channel::setChannelGroup](FMOD_Channel_SetChannelGroup.html)\
 [Channel::setDelay](FMOD_Channel_SetDelay.html)\
 [Channel::setFrequency](FMOD_Channel_SetFrequency.html)\
 [Channel::setLoopCount](FMOD_Channel_SetLoopCount.html)\
 [Channel::setLoopPoints](FMOD_Channel_SetLoopPoints.html)\
 [Channel::setLowPassGain](FMOD_Channel_SetLowPassGain.html)\
 [Channel::setMixLevelsInput](FMOD_Channel_SetMixLevelsInput.html)\
 [Channel::setMixLevelsOutput](FMOD_Channel_SetMixLevelsOutput.html)\
 [Channel::setMixMatrix](FMOD_Channel_SetMixMatrix.html)\
 [Channel::setMode](FMOD_Channel_SetMode.html)\
 [Channel::setMute](FMOD_Channel_SetMute.html)\
 [Channel::setPan](FMOD_Channel_SetPan.html)\
 [Channel::setPaused](FMOD_Channel_SetPaused.html)\
 [Channel::setPitch](FMOD_Channel_SetPitch.html)\
 [Channel::setPosition](FMOD_Channel_SetPosition.html)\
 [Channel::setPriority](FMOD_Channel_SetPriority.html)\
 [Channel::setReverbProperties](FMOD_Channel_SetReverbProperties.html)\
 [Channel::setUserData](FMOD_Channel_SetUserData.html)\
 [Channel::setVolume](FMOD_Channel_SetVolume.html)\
 [Channel::setVolumeRamp](FMOD_Channel_SetVolumeRamp.html)\
 [Channel::stop](FMOD_Channel_Stop.html)\
 Firelight Technologies FMOD Studio API

ChannelControl
==============

The base class for both Channels and Channel Groups.

Functions
---------

[ChannelControl::addDSP](FMOD_ChannelControl_AddDSP.html)\
 [ChannelControl::addFadePoint](FMOD_ChannelControl_AddFadePoint.html)\

[ChannelControl::get3DAttributes](FMOD_ChannelControl_Get3DAttributes.html)\

[ChannelControl::get3DConeOrientation](FMOD_ChannelControl_Get3DConeOrientation.html)\

[ChannelControl::get3DConeSettings](FMOD_ChannelControl_Get3DConeSettings.html)\

[ChannelControl::get3DCustomRolloff](FMOD_ChannelControl_Get3DCustomRolloff.html)\

[ChannelControl::get3DDistanceFilter](FMOD_ChannelControl_Get3DDistanceFilter.html)\

[ChannelControl::get3DDopplerLevel](FMOD_ChannelControl_Get3DDopplerLevel.html)\
 [ChannelControl::get3DLevel](FMOD_ChannelControl_Get3DLevel.html)\

[ChannelControl::get3DMinMaxDistance](FMOD_ChannelControl_Get3DMinMaxDistance.html)\

[ChannelControl::get3DOcclusion](FMOD_ChannelControl_Get3DOcclusion.html)\
 [ChannelControl::get3DSpread](FMOD_ChannelControl_Get3DSpread.html)\

[ChannelControl::getAudibility](FMOD_ChannelControl_GetAudibility.html)\
 [ChannelControl::getDSP](FMOD_ChannelControl_GetDSP.html)\
 [ChannelControl::getDSPClock](FMOD_ChannelControl_GetDSPClock.html)\
 [ChannelControl::getDelay](FMOD_ChannelControl_GetDelay.html)\

[ChannelControl::getFadePoints](FMOD_ChannelControl_GetFadePoints.html)\

[ChannelControl::getLowPassGain](FMOD_ChannelControl_GetLowPassGain.html)\
 [ChannelControl::getMixMatrix](FMOD_ChannelControl_GetMixMatrix.html)\
 [ChannelControl::getMute](FMOD_ChannelControl_GetMute.html)\
 [ChannelControl::getNumDSPs](FMOD_ChannelControl_GetNumDSPs.html)\
 [ChannelControl::getPaused](FMOD_ChannelControl_GetPaused.html)\
 [ChannelControl::getPitch](FMOD_ChannelControl_GetPitch.html)\

[ChannelControl::getReverbProperties](FMOD_ChannelControl_GetReverbProperties.html)\

[ChannelControl::getSystemObject](FMOD_ChannelControl_GetSystemObject.html)\
 [ChannelControl::getUserData](FMOD_ChannelControl_GetUserData.html)\
 [ChannelControl::getVolume](FMOD_ChannelControl_GetVolume.html)\

[ChannelControl::getVolumeRamp](FMOD_ChannelControl_GetVolumeRamp.html)\
 [ChannelControl::isPlaying](FMOD_ChannelControl_IsPlaying.html)\
 [ChannelControl::removeDSP](FMOD_ChannelControl_RemoveDSP.html)\

[ChannelControl::removeFadePoints](FMOD_ChannelControl_RemoveFadePoints.html)\

[ChannelControl::set3DAttributes](FMOD_ChannelControl_Set3DAttributes.html)\

[ChannelControl::set3DConeOrientation](FMOD_ChannelControl_Set3DConeOrientation.html)\

[ChannelControl::set3DConeSettings](FMOD_ChannelControl_Set3DConeSettings.html)\

[ChannelControl::set3DCustomRolloff](FMOD_ChannelControl_Set3DCustomRolloff.html)\

[ChannelControl::set3DDistanceFilter](FMOD_ChannelControl_Set3DDistanceFilter.html)\

[ChannelControl::set3DDopplerLevel](FMOD_ChannelControl_Set3DDopplerLevel.html)\
 [ChannelControl::set3DLevel](FMOD_ChannelControl_Set3DLevel.html)\

[ChannelControl::set3DMinMaxDistance](FMOD_ChannelControl_Set3DMinMaxDistance.html)\

[ChannelControl::set3DOcclusion](FMOD_ChannelControl_Set3DOcclusion.html)\
 [ChannelControl::set3DSpread](FMOD_ChannelControl_Set3DSpread.html)\
 [ChannelControl::setCallback](FMOD_ChannelControl_SetCallback.html)\
 [ChannelControl::setDelay](FMOD_ChannelControl_SetDelay.html)\

[ChannelControl::setLowPassGain](FMOD_ChannelControl_SetLowPassGain.html)\

[ChannelControl::setMixLevelsInput](FMOD_ChannelControl_SetMixLevelsInput.html)\

[ChannelControl::setMixLevelsOutput](FMOD_ChannelControl_SetMixLevelsOutput.html)\
 [ChannelControl::setMixMatrix](FMOD_ChannelControl_SetMixMatrix.html)\
 [ChannelControl::setMute](FMOD_ChannelControl_SetMute.html)\
 [ChannelControl::setPan](FMOD_ChannelControl_SetPan.html)\
 [ChannelControl::setPaused](FMOD_ChannelControl_SetPaused.html)\
 [ChannelControl::setPitch](FMOD_ChannelControl_SetPitch.html)\

[ChannelControl::setReverbProperties](FMOD_ChannelControl_SetReverbProperties.html)\
 [ChannelControl::setUserData](FMOD_ChannelControl_SetUserData.html)\
 [ChannelControl::setVolume](FMOD_ChannelControl_SetVolume.html)\

[ChannelControl::setVolumeRamp](FMOD_ChannelControl_SetVolumeRamp.html)\
 [ChannelControl::stop](FMOD_ChannelControl_Stop.html)\
 Firelight Technologies FMOD Studio API

ChannelGroup
============

Functions
---------

[ChannelGroup::addDSP](FMOD_ChannelGroup_AddDSP.html)\
 [ChannelGroup::addFadePoint](FMOD_ChannelGroup_AddFadePoint.html)\
 [ChannelGroup::addGroup](FMOD_ChannelGroup_AddGroup.html)\

[ChannelGroup::get3DAttributes](FMOD_ChannelGroup_Get3DAttributes.html)\

[ChannelGroup::get3DConeOrientation](FMOD_ChannelGroup_Get3DConeOrientation.html)\

[ChannelGroup::get3DConeSettings](FMOD_ChannelGroup_Get3DConeSettings.html)\

[ChannelGroup::get3DCustomRolloff](FMOD_ChannelGroup_Get3DCustomRolloff.html)\

[ChannelGroup::get3DDistanceFilter](FMOD_ChannelGroup_Get3DDistanceFilter.html)\

[ChannelGroup::get3DDopplerLevel](FMOD_ChannelGroup_Get3DDopplerLevel.html)\
 [ChannelGroup::get3DLevel](FMOD_ChannelGroup_Get3DLevel.html)\

[ChannelGroup::get3DMinMaxDistance](FMOD_ChannelGroup_Get3DMinMaxDistance.html)\
 [ChannelGroup::get3DOcclusion](FMOD_ChannelGroup_Get3DOcclusion.html)\
 [ChannelGroup::get3DSpread](FMOD_ChannelGroup_Get3DSpread.html)\
 [ChannelGroup::getAudibility](FMOD_ChannelGroup_GetAudibility.html)\
 [ChannelGroup::getChannel](FMOD_ChannelGroup_GetChannel.html)\
 [ChannelGroup::getDSP](FMOD_ChannelGroup_GetDSP.html)\
 [ChannelGroup::getDSPClock](FMOD_ChannelGroup_GetDSPClock.html)\
 [ChannelGroup::getDSPIndex](FMOD_ChannelGroup_GetDSPIndex.html)\
 [ChannelGroup::getDelay](FMOD_ChannelGroup_GetDelay.html)\
 [ChannelGroup::getFadePoints](FMOD_ChannelGroup_GetFadePoints.html)\
 [ChannelGroup::getGroup](FMOD_ChannelGroup_GetGroup.html)\
 [ChannelGroup::getLowPassGain](FMOD_ChannelGroup_GetLowPassGain.html)\
 [ChannelGroup::getMixMatrix](FMOD_ChannelGroup_GetMixMatrix.html)\
 [ChannelGroup::getMute](FMOD_ChannelGroup_GetMute.html)\
 [ChannelGroup::getName](FMOD_ChannelGroup_GetName.html)\
 [ChannelGroup::getNumChannels](FMOD_ChannelGroup_GetNumChannels.html)\
 [ChannelGroup::getNumDSPs](FMOD_ChannelGroup_GetNumDSPs.html)\
 [ChannelGroup::getNumGroups](FMOD_ChannelGroup_GetNumGroups.html)\
 [ChannelGroup::getParentGroup](FMOD_ChannelGroup_GetParentGroup.html)\
 [ChannelGroup::getPaused](FMOD_ChannelGroup_GetPaused.html)\
 [ChannelGroup::getPitch](FMOD_ChannelGroup_GetPitch.html)\

[ChannelGroup::getReverbProperties](FMOD_ChannelGroup_GetReverbProperties.html)\

[ChannelGroup::getSystemObject](FMOD_ChannelGroup_GetSystemObject.html)\
 [ChannelGroup::getUserData](FMOD_ChannelGroup_GetUserData.html)\
 [ChannelGroup::getVolume](FMOD_ChannelGroup_GetVolume.html)\
 [ChannelGroup::getVolumeRamp](FMOD_ChannelGroup_GetVolumeRamp.html)\
 [ChannelGroup::isPlaying](FMOD_ChannelGroup_IsPlaying.html)\
 [ChannelGroup::release](FMOD_ChannelGroup_Release.html)\
 [ChannelGroup::removeDSP](FMOD_ChannelGroup_RemoveDSP.html)\

[ChannelGroup::removeFadePoints](FMOD_ChannelGroup_RemoveFadePoints.html)\

[ChannelGroup::set3DAttributes](FMOD_ChannelGroup_Set3DAttributes.html)\

[ChannelGroup::set3DConeOrientation](FMOD_ChannelGroup_Set3DConeOrientation.html)\

[ChannelGroup::set3DConeSettings](FMOD_ChannelGroup_Set3DConeSettings.html)\

[ChannelGroup::set3DCustomRolloff](FMOD_ChannelGroup_Set3DCustomRolloff.html)\

[ChannelGroup::set3DDistanceFilter](FMOD_ChannelGroup_Set3DDistanceFilter.html)\

[ChannelGroup::set3DDopplerLevel](FMOD_ChannelGroup_Set3DDopplerLevel.html)\
 [ChannelGroup::set3DLevel](FMOD_ChannelGroup_Set3DLevel.html)\

[ChannelGroup::set3DMinMaxDistance](FMOD_ChannelGroup_Set3DMinMaxDistance.html)\
 [ChannelGroup::set3DOcclusion](FMOD_ChannelGroup_Set3DOcclusion.html)\
 [ChannelGroup::set3DSpread](FMOD_ChannelGroup_Set3DSpread.html)\
 [ChannelGroup::setCallback](FMOD_ChannelGroup_SetCallback.html)\
 [ChannelGroup::setDSPIndex](FMOD_ChannelGroup_SetDSPIndex.html)\
 [ChannelGroup::setDelay](FMOD_ChannelGroup_SetDelay.html)\
 [ChannelGroup::setLowPassGain](FMOD_ChannelGroup_SetLowPassGain.html)\

[ChannelGroup::setMixLevelsInput](FMOD_ChannelGroup_SetMixLevelsInput.html)\

[ChannelGroup::setMixLevelsOutput](FMOD_ChannelGroup_SetMixLevelsOutput.html)\
 [ChannelGroup::setMixMatrix](FMOD_ChannelGroup_SetMixMatrix.html)\
 [ChannelGroup::setMute](FMOD_ChannelGroup_SetMute.html)\
 [ChannelGroup::setPan](FMOD_ChannelGroup_SetPan.html)\
 [ChannelGroup::setPaused](FMOD_ChannelGroup_SetPaused.html)\
 [ChannelGroup::setPitch](FMOD_ChannelGroup_SetPitch.html)\

[ChannelGroup::setReverbProperties](FMOD_ChannelGroup_SetReverbProperties.html)\
 [ChannelGroup::setUserData](FMOD_ChannelGroup_SetUserData.html)\
 [ChannelGroup::setVolume](FMOD_ChannelGroup_SetVolume.html)\
 [ChannelGroup::setVolumeRamp](FMOD_ChannelGroup_SetVolumeRamp.html)\
 [ChannelGroup::stop](FMOD_ChannelGroup_Stop.html)\
 Firelight Technologies FMOD Studio API

Defines
=======

[FMOD\_CHANNELMASK](FMOD_CHANNELMASK.html)\
 [FMOD\_CODEC\_WAVEFORMAT\_VERSION](FMOD_CODEC_WAVEFORMAT_VERSION.html)\
 [FMOD\_DEBUGLEVEL](FMOD_DEBUGLEVEL.html)\
 [FMOD\_INITFLAGS](FMOD_INITFLAGS.html)\
 [FMOD\_MEMORY\_TYPE](FMOD_MEMORY_TYPE.html)\
 [FMOD\_MODE](FMOD_MODE.html)\
 [FMOD\_PORT\_INDEX](FMOD_PORT_INDEX.html)\
 [FMOD\_REVERB\_PRESETS](FMOD_REVERB_PRESETS.html)\
 [FMOD\_SYSTEM\_CALLBACK\_TYPE](FMOD_SYSTEM_CALLBACK_TYPE.html)\
 [FMOD\_TIMEUNIT](FMOD_TIMEUNIT.html)\
 Firelight Technologies FMOD Studio API

DSP
===

Functions
---------

[DSP::addInput](FMOD_DSP_AddInput.html)\
 [DSP::disconnectAll](FMOD_DSP_DisconnectAll.html)\
 [DSP::disconnectFrom](FMOD_DSP_DisconnectFrom.html)\
 [DSP::getActive](FMOD_DSP_GetActive.html)\
 [DSP::getBypass](FMOD_DSP_GetBypass.html)\
 [DSP::getChannelFormat](FMOD_DSP_GetChannelFormat.html)\
 [DSP::getDataParameterIndex](FMOD_DSP_GetDataParameterIndex.html)\
 [DSP::getIdle](FMOD_DSP_GetIdle.html)\
 [DSP::getInfo](FMOD_DSP_GetInfo.html)\
 [DSP::getInput](FMOD_DSP_GetInput.html)\
 [DSP::getMeteringEnabled](FMOD_DSP_GetMeteringEnabled.html)\
 [DSP::getMeteringInfo](FMOD_DSP_GetMeteringInfo.html)\
 [DSP::getNumInputs](FMOD_DSP_GetNumInputs.html)\
 [DSP::getNumOutputs](FMOD_DSP_GetNumOutputs.html)\
 [DSP::getNumParameters](FMOD_DSP_GetNumParameters.html)\
 [DSP::getOutput](FMOD_DSP_GetOutput.html)\
 [DSP::getOutputChannelFormat](FMOD_DSP_GetOutputChannelFormat.html)\
 [DSP::getParameterBool](FMOD_DSP_GetParameterBool.html)\
 [DSP::getParameterData](FMOD_DSP_GetParameterData.html)\
 [DSP::getParameterFloat](FMOD_DSP_GetParameterFloat.html)\
 [DSP::getParameterInfo](FMOD_DSP_GetParameterInfo.html)\
 [DSP::getParameterInt](FMOD_DSP_GetParameterInt.html)\
 [DSP::getSystemObject](FMOD_DSP_GetSystemObject.html)\
 [DSP::getType](FMOD_DSP_GetType.html)\
 [DSP::getUserData](FMOD_DSP_GetUserData.html)\
 [DSP::release](FMOD_DSP_Release.html)\
 [DSP::reset](FMOD_DSP_Reset.html)\
 [DSP::setActive](FMOD_DSP_SetActive.html)\
 [DSP::setBypass](FMOD_DSP_SetBypass.html)\
 [DSP::setChannelFormat](FMOD_DSP_SetChannelFormat.html)\
 [DSP::setMeteringEnabled](FMOD_DSP_SetMeteringEnabled.html)\
 [DSP::setParameterBool](FMOD_DSP_SetParameterBool.html)\
 [DSP::setParameterData](FMOD_DSP_SetParameterData.html)\
 [DSP::setParameterFloat](FMOD_DSP_SetParameterFloat.html)\
 [DSP::setParameterInt](FMOD_DSP_SetParameterInt.html)\
 [DSP::setUserData](FMOD_DSP_SetUserData.html)\
 [DSP::showConfigDialog](FMOD_DSP_ShowConfigDialog.html)\
 Firelight Technologies FMOD Studio API

DSPConnection
=============

Functions
---------

[DSPConnection::getInput](FMOD_DSPConnection_GetInput.html)\
 [DSPConnection::getMix](FMOD_DSPConnection_GetMix.html)\
 [DSPConnection::getMixMatrix](FMOD_DSPConnection_GetMixMatrix.html)\
 [DSPConnection::getOutput](FMOD_DSPConnection_GetOutput.html)\
 [DSPConnection::getType](FMOD_DSPConnection_GetType.html)\
 [DSPConnection::getUserData](FMOD_DSPConnection_GetUserData.html)\
 [DSPConnection::setMix](FMOD_DSPConnection_SetMix.html)\
 [DSPConnection::setMixMatrix](FMOD_DSPConnection_SetMixMatrix.html)\
 [DSPConnection::setUserData](FMOD_DSPConnection_SetUserData.html)\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FMOD\_CHANNELCONTROL\_CALLBACK\_TYPE](FMOD_CHANNELCONTROL_CALLBACK_TYPE.html)\
 [FMOD\_CHANNELCONTROL\_DSP\_INDEX](FMOD_CHANNELCONTROL_DSP_INDEX.html)\
 [FMOD\_CHANNELCONTROL\_TYPE](FMOD_CHANNELCONTROL_TYPE.html)\
 [FMOD\_CHANNELORDER](FMOD_CHANNELORDER.html)\
 [FMOD\_DSPCONNECTION\_TYPE](FMOD_DSPCONNECTION_TYPE.html)\
 [FMOD\_DSP\_CHORUS](FMOD_DSP_CHORUS.html)\
 [FMOD\_DSP\_COMPRESSOR](FMOD_DSP_COMPRESSOR.html)\
 [FMOD\_DSP\_DELAY](FMOD_DSP_DELAY.html)\
 [FMOD\_DSP\_DISTORTION](FMOD_DSP_DISTORTION.html)\
 [FMOD\_DSP\_ECHO](FMOD_DSP_ECHO.html)\
 [FMOD\_DSP\_ENVELOPEFOLLOWER](FMOD_DSP_ENVELOPEFOLLOWER.html)\
 [FMOD\_DSP\_FFT](FMOD_DSP_FFT.html)\
 [FMOD\_DSP\_FFT\_WINDOW](FMOD_DSP_FFT_WINDOW.html)\
 [FMOD\_DSP\_FLANGE](FMOD_DSP_FLANGE.html)\
 [FMOD\_DSP\_HIGHPASS](FMOD_DSP_HIGHPASS.html)\
 [FMOD\_DSP\_HIGHPASS\_SIMPLE](FMOD_DSP_HIGHPASS_SIMPLE.html)\
 [FMOD\_DSP\_ITECHO](FMOD_DSP_ITECHO.html)\
 [FMOD\_DSP\_ITLOWPASS](FMOD_DSP_ITLOWPASS.html)\
 [FMOD\_DSP\_LIMITER](FMOD_DSP_LIMITER.html)\
 [FMOD\_DSP\_LOWPASS](FMOD_DSP_LOWPASS.html)\
 [FMOD\_DSP\_LOWPASS\_SIMPLE](FMOD_DSP_LOWPASS_SIMPLE.html)\
 [FMOD\_DSP\_NORMALIZE](FMOD_DSP_NORMALIZE.html)\
 [FMOD\_DSP\_OSCILLATOR](FMOD_DSP_OSCILLATOR.html)\
 [FMOD\_DSP\_PAN](FMOD_DSP_PAN.html)\

[FMOD\_DSP\_PAN\_3D\_EXTENT\_MODE\_TYPE](FMOD_DSP_PAN_3D_EXTENT_MODE_TYPE.html)\
 [FMOD\_DSP\_PAN\_3D\_ROLLOFF\_TYPE](FMOD_DSP_PAN_3D_ROLLOFF_TYPE.html)\

[FMOD\_DSP\_PAN\_SURROUND\_FROM\_STEREO\_MODE\_TYPE](FMOD_DSP_PAN_SURROUND_FROM_STEREO_MODE_TYPE.html)\
 [FMOD\_DSP\_PARAMEQ](FMOD_DSP_PARAMEQ.html)\
 [FMOD\_DSP\_PARAMETER\_DATA\_TYPE](FMOD_DSP_PARAMETER_DATA_TYPE.html)\

[FMOD\_DSP\_PARAMETER\_FLOAT\_MAPPING\_TYPE](FMOD_DSP_PARAMETER_FLOAT_MAPPING_TYPE.html)\
 [FMOD\_DSP\_PARAMETER\_TYPE](FMOD_DSP_PARAMETER_TYPE.html)\
 [FMOD\_DSP\_PITCHSHIFT](FMOD_DSP_PITCHSHIFT.html)\
 [FMOD\_DSP\_PROCESS\_OPERATION](FMOD_DSP_PROCESS_OPERATION.html)\
 [FMOD\_DSP\_RESAMPLER](FMOD_DSP_RESAMPLER.html)\
 [FMOD\_DSP\_RETURN](FMOD_DSP_RETURN.html)\
 [FMOD\_DSP\_SEND](FMOD_DSP_SEND.html)\
 [FMOD\_DSP\_SFXREVERB](FMOD_DSP_SFXREVERB.html)\
 [FMOD\_DSP\_THREE\_EQ](FMOD_DSP_THREE_EQ.html)\

[FMOD\_DSP\_THREE\_EQ\_CROSSOVERSLOPE\_TYPE](FMOD_DSP_THREE_EQ_CROSSOVERSLOPE_TYPE.html)\
 [FMOD\_DSP\_TREMOLO](FMOD_DSP_TREMOLO.html)\
 [FMOD\_DSP\_TYPE](FMOD_DSP_TYPE.html)\

[FMOD\_ERRORCALLBACK\_INSTANCETYPE](FMOD_ERRORCALLBACK_INSTANCETYPE.html)\
 [FMOD\_OPENSTATE](FMOD_OPENSTATE.html)\
 [FMOD\_OUTPUTTYPE](FMOD_OUTPUTTYPE.html)\
 [FMOD\_PLUGINTYPE](FMOD_PLUGINTYPE.html)\
 [FMOD\_RESULT](FMOD_RESULT.html)\
 [FMOD\_SOUNDGROUP\_BEHAVIOR](FMOD_SOUNDGROUP_BEHAVIOR.html)\
 [FMOD\_SOUND\_FORMAT](FMOD_SOUND_FORMAT.html)\
 [FMOD\_SOUND\_TYPE](FMOD_SOUND_TYPE.html)\
 [FMOD\_SPEAKER](FMOD_SPEAKER.html)\
 [FMOD\_SPEAKERMODE](FMOD_SPEAKERMODE.html)\
 [FMOD\_TAGDATATYPE](FMOD_TAGDATATYPE.html)\
 [FMOD\_TAGTYPE](FMOD_TAGTYPE.html)\
 Firelight Technologies FMOD Studio API

Functions
=========

[Debug\_GetLevel](FMOD_Debug_GetLevel.html)\
 [Debug\_SetLevel](FMOD_Debug_SetLevel.html)\
 [File\_GetDiskBusy](FMOD_File_GetDiskBusy.html)\
 [File\_SetDiskBusy](FMOD_File_SetDiskBusy.html)\
 [Memory\_GetStats](FMOD_Memory_GetStats.html)\
 [Memory\_Initialize](FMOD_Memory_Initialize.html)\
 [System\_Create](FMOD_System_Create.html)\
 Firelight Technologies FMOD Studio API

Geometry
========

Functions
---------

[Geometry::addPolygon](FMOD_Geometry_AddPolygon.html)\
 [Geometry::getActive](FMOD_Geometry_GetActive.html)\
 [Geometry::getMaxPolygons](FMOD_Geometry_GetMaxPolygons.html)\
 [Geometry::getNumPolygons](FMOD_Geometry_GetNumPolygons.html)\

[Geometry::getPolygonAttributes](FMOD_Geometry_GetPolygonAttributes.html)\

[Geometry::getPolygonNumVertices](FMOD_Geometry_GetPolygonNumVertices.html)\
 [Geometry::getPolygonVertex](FMOD_Geometry_GetPolygonVertex.html)\
 [Geometry::getPosition](FMOD_Geometry_GetPosition.html)\
 [Geometry::getRotation](FMOD_Geometry_GetRotation.html)\
 [Geometry::getScale](FMOD_Geometry_GetScale.html)\
 [Geometry::getUserData](FMOD_Geometry_GetUserData.html)\
 [Geometry::release](FMOD_Geometry_Release.html)\
 [Geometry::save](FMOD_Geometry_Save.html)\
 [Geometry::setActive](FMOD_Geometry_SetActive.html)\

[Geometry::setPolygonAttributes](FMOD_Geometry_SetPolygonAttributes.html)\
 [Geometry::setPolygonVertex](FMOD_Geometry_SetPolygonVertex.html)\
 [Geometry::setPosition](FMOD_Geometry_SetPosition.html)\
 [Geometry::setRotation](FMOD_Geometry_SetRotation.html)\
 [Geometry::setScale](FMOD_Geometry_SetScale.html)\
 [Geometry::setUserData](FMOD_Geometry_SetUserData.html)\
 Firelight Technologies FMOD Studio API

C++ interfaces
==============

[System](lowlevel_api_System.html)\
 [Sound](lowlevel_api_Sound.html)\
 [ChannelControl](lowlevel_api_ChannelControl.html)\
 [Channel](lowlevel_api_Channel.html)\
 [ChannelGroup](lowlevel_api_ChannelGroup.html)\
 [SoundGroup](lowlevel_api_SoundGroup.html)\
 [DSP](lowlevel_api_DSP.html)\
 [DSPConnection](lowlevel_api_DSPConnection.html)\
 [Geometry](lowlevel_api_Geometry.html)\
 [Reverb3D](lowlevel_api_Reverb3D.html)\
 Firelight Technologies FMOD Studio API

Reverb3D
========

Functions
---------

[Reverb3D::get3DAttributes](FMOD_Reverb3D_Get3DAttributes.html)\
 [Reverb3D::getActive](FMOD_Reverb3D_GetActive.html)\
 [Reverb3D::getProperties](FMOD_Reverb3D_GetProperties.html)\
 [Reverb3D::getUserData](FMOD_Reverb3D_GetUserData.html)\
 [Reverb3D::release](FMOD_Reverb3D_Release.html)\
 [Reverb3D::set3DAttributes](FMOD_Reverb3D_Set3DAttributes.html)\
 [Reverb3D::setActive](FMOD_Reverb3D_SetActive.html)\
 [Reverb3D::setProperties](FMOD_Reverb3D_SetProperties.html)\
 [Reverb3D::setUserData](FMOD_Reverb3D_SetUserData.html)\
 Firelight Technologies FMOD Studio API

Sound
=====

Functions
---------

[Sound::addSyncPoint](FMOD_Sound_AddSyncPoint.html)\
 [Sound::deleteSyncPoint](FMOD_Sound_DeleteSyncPoint.html)\
 [Sound::get3DConeSettings](FMOD_Sound_Get3DConeSettings.html)\
 [Sound::get3DCustomRolloff](FMOD_Sound_Get3DCustomRolloff.html)\
 [Sound::get3DMinMaxDistance](FMOD_Sound_Get3DMinMaxDistance.html)\
 [Sound::getDefaults](FMOD_Sound_GetDefaults.html)\
 [Sound::getFormat](FMOD_Sound_GetFormat.html)\
 [Sound::getLength](FMOD_Sound_GetLength.html)\
 [Sound::getLoopCount](FMOD_Sound_GetLoopCount.html)\
 [Sound::getLoopPoints](FMOD_Sound_GetLoopPoints.html)\
 [Sound::getMode](FMOD_Sound_GetMode.html)\
 [Sound::getMusicChannelVolume](FMOD_Sound_GetMusicChannelVolume.html)\
 [Sound::getMusicNumChannels](FMOD_Sound_GetMusicNumChannels.html)\
 [Sound::getMusicSpeed](FMOD_Sound_GetMusicSpeed.html)\
 [Sound::getName](FMOD_Sound_GetName.html)\
 [Sound::getNumSubSounds](FMOD_Sound_GetNumSubSounds.html)\
 [Sound::getNumSyncPoints](FMOD_Sound_GetNumSyncPoints.html)\
 [Sound::getNumTags](FMOD_Sound_GetNumTags.html)\
 [Sound::getOpenState](FMOD_Sound_GetOpenState.html)\
 [Sound::getSoundGroup](FMOD_Sound_GetSoundGroup.html)\
 [Sound::getSubSound](FMOD_Sound_GetSubSound.html)\
 [Sound::getSubSoundParent](FMOD_Sound_GetSubSoundParent.html)\
 [Sound::getSyncPoint](FMOD_Sound_GetSyncPoint.html)\
 [Sound::getSyncPointInfo](FMOD_Sound_GetSyncPointInfo.html)\
 [Sound::getSystemObject](FMOD_Sound_GetSystemObject.html)\
 [Sound::getTag](FMOD_Sound_GetTag.html)\
 [Sound::getUserData](FMOD_Sound_GetUserData.html)\
 [Sound::lock](FMOD_Sound_Lock.html)\
 [Sound::readData](FMOD_Sound_ReadData.html)\
 [Sound::release](FMOD_Sound_Release.html)\
 [Sound::seekData](FMOD_Sound_SeekData.html)\
 [Sound::set3DConeSettings](FMOD_Sound_Set3DConeSettings.html)\
 [Sound::set3DCustomRolloff](FMOD_Sound_Set3DCustomRolloff.html)\
 [Sound::set3DMinMaxDistance](FMOD_Sound_Set3DMinMaxDistance.html)\
 [Sound::setDefaults](FMOD_Sound_SetDefaults.html)\
 [Sound::setLoopCount](FMOD_Sound_SetLoopCount.html)\
 [Sound::setLoopPoints](FMOD_Sound_SetLoopPoints.html)\
 [Sound::setMode](FMOD_Sound_SetMode.html)\
 [Sound::setMusicChannelVolume](FMOD_Sound_SetMusicChannelVolume.html)\
 [Sound::setMusicSpeed](FMOD_Sound_SetMusicSpeed.html)\
 [Sound::setSoundGroup](FMOD_Sound_SetSoundGroup.html)\
 [Sound::setSubSound](FMOD_Sound_SetSubSound.html)\
 [Sound::setUserData](FMOD_Sound_SetUserData.html)\
 [Sound::unlock](FMOD_Sound_Unlock.html)\
 Firelight Technologies FMOD Studio API

SoundGroup
==========

Functions
---------

[SoundGroup::getMaxAudible](FMOD_SoundGroup_GetMaxAudible.html)\

[SoundGroup::getMaxAudibleBehavior](FMOD_SoundGroup_GetMaxAudibleBehavior.html)\
 [SoundGroup::getMuteFadeSpeed](FMOD_SoundGroup_GetMuteFadeSpeed.html)\
 [SoundGroup::getName](FMOD_SoundGroup_GetName.html)\
 [SoundGroup::getNumPlaying](FMOD_SoundGroup_GetNumPlaying.html)\
 [SoundGroup::getNumSounds](FMOD_SoundGroup_GetNumSounds.html)\
 [SoundGroup::getSound](FMOD_SoundGroup_GetSound.html)\
 [SoundGroup::getSystemObject](FMOD_SoundGroup_GetSystemObject.html)\
 [SoundGroup::getUserData](FMOD_SoundGroup_GetUserData.html)\
 [SoundGroup::getVolume](FMOD_SoundGroup_GetVolume.html)\
 [SoundGroup::release](FMOD_SoundGroup_Release.html)\
 [SoundGroup::setMaxAudible](FMOD_SoundGroup_SetMaxAudible.html)\

[SoundGroup::setMaxAudibleBehavior](FMOD_SoundGroup_SetMaxAudibleBehavior.html)\
 [SoundGroup::setMuteFadeSpeed](FMOD_SoundGroup_SetMuteFadeSpeed.html)\
 [SoundGroup::setUserData](FMOD_SoundGroup_SetUserData.html)\
 [SoundGroup::setVolume](FMOD_SoundGroup_SetVolume.html)\
 [SoundGroup::stop](FMOD_SoundGroup_Stop.html)\
 Firelight Technologies FMOD Studio API

Structures
==========

[FMOD\_3D\_ATTRIBUTES](FMOD_3D_ATTRIBUTES.html)\
 [FMOD\_ADVANCEDSETTINGS](FMOD_ADVANCEDSETTINGS.html)\
 [FMOD\_ASYNCREADINFO](FMOD_ASYNCREADINFO.html)\
 [FMOD\_CODEC\_DESCRIPTION](FMOD_CODEC_DESCRIPTION.html)\
 [FMOD\_CODEC\_STATE](FMOD_CODEC_STATE.html)\
 [FMOD\_CODEC\_WAVEFORMAT](FMOD_CODEC_WAVEFORMAT.html)\
 [FMOD\_CREATESOUNDEXINFO](FMOD_CREATESOUNDEXINFO.html)\
 [FMOD\_DSP\_BUFFER\_ARRAY](FMOD_DSP_BUFFER_ARRAY.html)\
 [FMOD\_DSP\_DESCRIPTION](FMOD_DSP_DESCRIPTION.html)\
 [FMOD\_DSP\_METERING\_INFO](FMOD_DSP_METERING_INFO.html)\

[FMOD\_DSP\_PARAMETER\_3DATTRIBUTES](FMOD_DSP_PARAMETER_3DATTRIBUTES.html)\
 [FMOD\_DSP\_PARAMETER\_DESC](FMOD_DSP_PARAMETER_DESC.html)\
 [FMOD\_DSP\_PARAMETER\_DESC\_BOOL](FMOD_DSP_PARAMETER_DESC_BOOL.html)\
 [FMOD\_DSP\_PARAMETER\_DESC\_DATA](FMOD_DSP_PARAMETER_DESC_DATA.html)\

[FMOD\_DSP\_PARAMETER\_DESC\_FLOAT](FMOD_DSP_PARAMETER_DESC_FLOAT.html)\
 [FMOD\_DSP\_PARAMETER\_DESC\_INT](FMOD_DSP_PARAMETER_DESC_INT.html)\

[FMOD\_DSP\_PARAMETER\_OVERALLGAIN](FMOD_DSP_PARAMETER_OVERALLGAIN.html)\
 [FMOD\_DSP\_PARAMETER\_SIDECHAIN](FMOD_DSP_PARAMETER_SIDECHAIN.html)\
 [FMOD\_DSP\_STATE](FMOD_DSP_STATE.html)\

[FMOD\_DSP\_STATE\_SYSTEMCALLBACKS](FMOD_DSP_STATE_SYSTEMCALLBACKS.html)\
 [FMOD\_ERRORCALLBACK\_INFO](FMOD_ERRORCALLBACK_INFO.html)\
 [FMOD\_GUID](FMOD_GUID.html)\
 [FMOD\_OUTPUT\_DESCRIPTION](FMOD_OUTPUT_DESCRIPTION.html)\
 [FMOD\_OUTPUT\_STATE](FMOD_OUTPUT_STATE.html)\
 [FMOD\_REVERB\_PROPERTIES](FMOD_REVERB_PROPERTIES.html)\
 [FMOD\_TAG](FMOD_TAG.html)\
 [FMOD\_VECTOR](FMOD_VECTOR.html)\
 [piecewiselinearmapping](piecewiselinearmapping.html)\
 Firelight Technologies FMOD Studio API

System
======

The main object for the FMOD Low Level System.

Functions
---------

[System::attachChannelGroupToPort](FMOD_System_AttachChannelGroupToPort.html)\
 [System::attachFileSystem](FMOD_System_AttachFileSystem.html)\
 [System::close](FMOD_System_Close.html)\
 [System::createChannelGroup](FMOD_System_CreateChannelGroup.html)\
 [System::createDSP](FMOD_System_CreateDSP.html)\
 [System::createDSPByPlugin](FMOD_System_CreateDSPByPlugin.html)\
 [System::createDSPByType](FMOD_System_CreateDSPByType.html)\
 [System::createGeometry](FMOD_System_CreateGeometry.html)\
 [System::createReverb3D](FMOD_System_CreateReverb3D.html)\
 [System::createSound](FMOD_System_CreateSound.html)\
 [System::createSoundGroup](FMOD_System_CreateSoundGroup.html)\
 [System::createStream](FMOD_System_CreateStream.html)\

[System::detachChannelGroupFromPort](FMOD_System_DetachChannelGroupFromPort.html)\

[System::get3DListenerAttributes](FMOD_System_Get3DListenerAttributes.html)\
 [System::get3DNumListeners](FMOD_System_Get3DNumListeners.html)\
 [System::get3DSettings](FMOD_System_Get3DSettings.html)\
 [System::getAdvancedSettings](FMOD_System_GetAdvancedSettings.html)\
 [System::getCPUUsage](FMOD_System_GetCPUUsage.html)\
 [System::getChannel](FMOD_System_GetChannel.html)\
 [System::getChannelsPlaying](FMOD_System_GetChannelsPlaying.html)\
 [System::getDSPBufferSize](FMOD_System_GetDSPBufferSize.html)\
 [System::getDSPInfoByPlugin](FMOD_System_GetDSPInfoByPlugin.html)\
 [System::getDriver](FMOD_System_GetDriver.html)\
 [System::getDriverInfo](FMOD_System_GetDriverInfo.html)\
 [System::getGeometryOcclusion](FMOD_System_GetGeometryOcclusion.html)\
 [System::getGeometrySettings](FMOD_System_GetGeometrySettings.html)\

[System::getMasterChannelGroup](FMOD_System_GetMasterChannelGroup.html)\
 [System::getMasterSoundGroup](FMOD_System_GetMasterSoundGroup.html)\
 [System::getNetworkProxy](FMOD_System_GetNetworkProxy.html)\
 [System::getNetworkTimeout](FMOD_System_GetNetworkTimeout.html)\
 [System::getNumDrivers](FMOD_System_GetNumDrivers.html)\
 [System::getNumPlugins](FMOD_System_GetNumPlugins.html)\
 [System::getOutput](FMOD_System_GetOutput.html)\
 [System::getOutputByPlugin](FMOD_System_GetOutputByPlugin.html)\
 [System::getOutputHandle](FMOD_System_GetOutputHandle.html)\
 [System::getPluginHandle](FMOD_System_GetPluginHandle.html)\
 [System::getPluginInfo](FMOD_System_GetPluginInfo.html)\
 [System::getRecordDriverInfo](FMOD_System_GetRecordDriverInfo.html)\
 [System::getRecordNumDrivers](FMOD_System_GetRecordNumDrivers.html)\
 [System::getRecordPosition](FMOD_System_GetRecordPosition.html)\
 [System::getReverbProperties](FMOD_System_GetReverbProperties.html)\
 [System::getSoftwareChannels](FMOD_System_GetSoftwareChannels.html)\
 [System::getSoftwareFormat](FMOD_System_GetSoftwareFormat.html)\
 [System::getSoundRAM](FMOD_System_GetSoundRAM.html)\
 [System::getSpeakerPosition](FMOD_System_GetSpeakerPosition.html)\
 [System::getStreamBufferSize](FMOD_System_GetStreamBufferSize.html)\
 [System::getUserData](FMOD_System_GetUserData.html)\
 [System::getVersion](FMOD_System_GetVersion.html)\
 [System::init](FMOD_System_Init.html)\
 [System::isRecording](FMOD_System_IsRecording.html)\
 [System::loadGeometry](FMOD_System_LoadGeometry.html)\
 [System::loadPlugin](FMOD_System_LoadPlugin.html)\
 [System::lockDSP](FMOD_System_LockDSP.html)\
 [System::mixerResume](FMOD_System_MixerResume.html)\
 [System::mixerSuspend](FMOD_System_MixerSuspend.html)\
 [System::playDSP](FMOD_System_PlayDSP.html)\
 [System::playSound](FMOD_System_PlaySound.html)\
 [System::recordStart](FMOD_System_RecordStart.html)\
 [System::recordStop](FMOD_System_RecordStop.html)\
 [System::registerCodec](FMOD_System_RegisterCodec.html)\
 [System::registerDSP](FMOD_System_RegisterDSP.html)\
 [System::release](FMOD_System_Release.html)\

[System::set3DListenerAttributes](FMOD_System_Set3DListenerAttributes.html)\
 [System::set3DNumListeners](FMOD_System_Set3DNumListeners.html)\
 [System::set3DRolloffCallback](FMOD_System_Set3DRolloffCallback.html)\
 [System::set3DSettings](FMOD_System_Set3DSettings.html)\
 [System::setAdvancedSettings](FMOD_System_SetAdvancedSettings.html)\
 [System::setCallback](FMOD_System_SetCallback.html)\
 [System::setDSPBufferSize](FMOD_System_SetDSPBufferSize.html)\
 [System::setDriver](FMOD_System_SetDriver.html)\
 [System::setFileSystem](FMOD_System_SetFileSystem.html)\
 [System::setGeometrySettings](FMOD_System_SetGeometrySettings.html)\
 [System::setNetworkProxy](FMOD_System_SetNetworkProxy.html)\
 [System::setNetworkTimeout](FMOD_System_SetNetworkTimeout.html)\
 [System::setOutput](FMOD_System_SetOutput.html)\
 [System::setOutputByPlugin](FMOD_System_SetOutputByPlugin.html)\
 [System::setPluginPath](FMOD_System_SetPluginPath.html)\
 [System::setReverbProperties](FMOD_System_SetReverbProperties.html)\
 [System::setSoftwareChannels](FMOD_System_SetSoftwareChannels.html)\
 [System::setSoftwareFormat](FMOD_System_SetSoftwareFormat.html)\
 [System::setSpeakerPosition](FMOD_System_SetSpeakerPosition.html)\
 [System::setStreamBufferSize](FMOD_System_SetStreamBufferSize.html)\
 [System::setUserData](FMOD_System_SetUserData.html)\
 [System::unloadPlugin](FMOD_System_UnloadPlugin.html)\
 [System::unlockDSP](FMOD_System_UnlockDSP.html)\
 [System::update](FMOD_System_Update.html)\
 Remarks -------

When using FMOD Studio, this system object will be automatically
instantiated as part of
[Studio::System::initialize](FMOD_Studio_System_Initialize.html).

See Also
--------

-   [Studio::System::getLowLevelSystem](FMOD_Studio_System_GetLowLevelSystem.html)

Firelight Technologies FMOD Studio API

Studio API
==========

[C++ interfaces](studio_api_interfaces.html)\
 [Functions](studio_api_functions.html)\
 [Structures](studio_api_structures.html)\
 [Defines](studio_api_defines.html)\
 [Enumerations](studio_api_enumerations.html)\
 Firelight Technologies FMOD Studio API

Studio::Bank
============

A bank contains FMOD Studio Event data as well as the actual sound data
for all events in that bank.

Functions
---------

[Studio::Bank::getEventCount](FMOD_Studio_Bank_GetEventCount.html)\
 [Studio::Bank::getEventList](FMOD_Studio_Bank_GetEventList.html)\
 [Studio::Bank::getID](FMOD_Studio_Bank_GetID.html)\
 [Studio::Bank::getLoadingState](FMOD_Studio_Bank_GetLoadingState.html)\

[Studio::Bank::getMixerStripCount](FMOD_Studio_Bank_GetMixerStripCount.html)\

[Studio::Bank::getMixerStripList](FMOD_Studio_Bank_GetMixerStripList.html)\
 [Studio::Bank::getPath](FMOD_Studio_Bank_GetPath.html)\

[Studio::Bank::getSampleLoadingState](FMOD_Studio_Bank_GetSampleLoadingState.html)\
 [Studio::Bank::loadSampleData](FMOD_Studio_Bank_LoadSampleData.html)\
 [Studio::Bank::unload](FMOD_Studio_Bank_Unload.html)\

[Studio::Bank::unloadSampleData](FMOD_Studio_Bank_UnloadSampleData.html)\
 See Also --------

-   [Studio::System::loadBankFile](FMOD_Studio_System_LoadBankFile.html)
-   [Studio::System::loadBankMemory](FMOD_Studio_System_LoadBankMemory.html)
-   [Studio::System::loadBankCustom](FMOD_Studio_System_LoadBankCustom.html)

Firelight Technologies FMOD Studio API

Callbacks
=========

[FMOD\_STUDIO\_EVENT\_CALLBACK](FMOD_STUDIO_EVENT_CALLBACK.html)\
 Firelight Technologies FMOD Studio API

Studio::CueInstance
===================

A trigger for an FMOD Studio Event.

Functions
---------

[Studio::CueInstance::trigger](FMOD_Studio_CueInstance_Trigger.html)\
 Remarks -------

Cues can be set into events to pause the timeline at a certain point
until the game activates the cue. Currently there is only a single cue
type supported, with a name "keyOff".

See Also
--------

-   [Studio::EventInstance::getCue](FMOD_Studio_EventInstance_GetCue.html)
-   [Studio::EventInstance::getCueByIndex](FMOD_Studio_EventInstance_GetCueByIndex.html)
-   [Studio::EventInstance::getCueCount](FMOD_Studio_EventInstance_GetCueCount.html)

Firelight Technologies FMOD Studio API

Defines
=======

[FMOD\_STUDIO\_INITFLAGS](FMOD_STUDIO_INITFLAGS.html)\
 [FMOD\_STUDIO\_LOAD\_BANK\_FLAGS](FMOD_STUDIO_LOAD_BANK_FLAGS.html)\

[FMOD\_STUDIO\_RECORD\_COMMANDS\_FLAGS](FMOD_STUDIO_RECORD_COMMANDS_FLAGS.html)\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FMOD\_STUDIO\_EVENT\_CALLBACK\_TYPE](FMOD_STUDIO_EVENT_CALLBACK_TYPE.html)\
 [FMOD\_STUDIO\_LOADING\_MODE](FMOD_STUDIO_LOADING_MODE.html)\
 [FMOD\_STUDIO\_LOADING\_STATE](FMOD_STUDIO_LOADING_STATE.html)\
 [FMOD\_STUDIO\_LOAD\_MEMORY\_MODE](FMOD_STUDIO_LOAD_MEMORY_MODE.html)\
 [FMOD\_STUDIO\_PARAMETER\_TYPE](FMOD_STUDIO_PARAMETER_TYPE.html)\
 [FMOD\_STUDIO\_PLAYBACK\_STATE](FMOD_STUDIO_PLAYBACK_STATE.html)\
 [FMOD\_STUDIO\_STOP\_MODE](FMOD_STUDIO_STOP_MODE.html)\

[FMOD\_STUDIO\_USER\_PROPERTY\_TYPE](FMOD_STUDIO_USER_PROPERTY_TYPE.html)\
 Firelight Technologies FMOD Studio API

Studio::EventDescription
========================

The description for a FMOD Studio Event.

Functions
---------

[Studio::EventDescription::createInstance](FMOD_Studio_EventDescription_CreateInstance.html)\

[Studio::EventDescription::getID](FMOD_Studio_EventDescription_GetID.html)\

[Studio::EventDescription::getInstanceCount](FMOD_Studio_EventDescription_GetInstanceCount.html)\

[Studio::EventDescription::getInstanceList](FMOD_Studio_EventDescription_GetInstanceList.html)\

[Studio::EventDescription::getLength](FMOD_Studio_EventDescription_GetLength.html)\

[Studio::EventDescription::getMaximumDistance](FMOD_Studio_EventDescription_GetMaximumDistance.html)\

[Studio::EventDescription::getMinimumDistance](FMOD_Studio_EventDescription_GetMinimumDistance.html)\

[Studio::EventDescription::getParameter](FMOD_Studio_EventDescription_GetParameter.html)\

[Studio::EventDescription::getParameterByIndex](FMOD_Studio_EventDescription_GetParameterByIndex.html)\

[Studio::EventDescription::getParameterCount](FMOD_Studio_EventDescription_GetParameterCount.html)\

[Studio::EventDescription::getPath](FMOD_Studio_EventDescription_GetPath.html)\

[Studio::EventDescription::getSampleLoadingState](FMOD_Studio_EventDescription_GetSampleLoadingState.html)\

[Studio::EventDescription::getUserData](FMOD_Studio_EventDescription_GetUserData.html)\

[Studio::EventDescription::getUserProperty](FMOD_Studio_EventDescription_GetUserProperty.html)\

[Studio::EventDescription::getUserPropertyByIndex](FMOD_Studio_EventDescription_GetUserPropertyByIndex.html)\

[Studio::EventDescription::getUserPropertyCount](FMOD_Studio_EventDescription_GetUserPropertyCount.html)\

[Studio::EventDescription::is3D](FMOD_Studio_EventDescription_Is3D.html)\

[Studio::EventDescription::isOneshot](FMOD_Studio_EventDescription_IsOneshot.html)\

[Studio::EventDescription::isStream](FMOD_Studio_EventDescription_IsStream.html)\

[Studio::EventDescription::loadSampleData](FMOD_Studio_EventDescription_LoadSampleData.html)\

[Studio::EventDescription::releaseAllInstances](FMOD_Studio_EventDescription_ReleaseAllInstances.html)\

[Studio::EventDescription::setCallback](FMOD_Studio_EventDescription_SetCallback.html)\

[Studio::EventDescription::setUserData](FMOD_Studio_EventDescription_SetUserData.html)\

[Studio::EventDescription::unloadSampleData](FMOD_Studio_EventDescription_UnloadSampleData.html)\
 Remarks -------

Event Descriptions belong to banks and can be queried after the relevant
bank has been loaded. Event Descriptions can be found either by looking
up by GUID or by querying all descriptions as part of a bank.

See Also
--------

-   [Studio::System::loadBankFile](FMOD_Studio_System_LoadBankFile.html)
-   [Studio::System::loadBankMemory](FMOD_Studio_System_LoadBankMemory.html)
-   [Studio::System::loadBankCustom](FMOD_Studio_System_LoadBankCustom.html)
-   [Studio::System::getEvent](FMOD_Studio_System_GetEvent.html)
-   [Studio::Bank::getEventCount](FMOD_Studio_Bank_GetEventCount.html)
-   [Studio::Bank::getEventList](FMOD_Studio_Bank_GetEventList.html)

Firelight Technologies FMOD Studio API

Studio::EventInstance
=====================

An instance of an FMOD Studio Event.

Functions
---------

[Studio::EventInstance::createSubEvent](FMOD_Studio_EventInstance_CreateSubEvent.html)\

[Studio::EventInstance::get3DAttributes](FMOD_Studio_EventInstance_Get3DAttributes.html)\

[Studio::EventInstance::getChannelGroup](FMOD_Studio_EventInstance_GetChannelGroup.html)\
 [Studio::EventInstance::getCue](FMOD_Studio_EventInstance_GetCue.html)\

[Studio::EventInstance::getCueByIndex](FMOD_Studio_EventInstance_GetCueByIndex.html)\

[Studio::EventInstance::getCueCount](FMOD_Studio_EventInstance_GetCueCount.html)\

[Studio::EventInstance::getDescription](FMOD_Studio_EventInstance_GetDescription.html)\

[Studio::EventInstance::getLoadingState](FMOD_Studio_EventInstance_GetLoadingState.html)\

[Studio::EventInstance::getParameter](FMOD_Studio_EventInstance_GetParameter.html)\

[Studio::EventInstance::getParameterByIndex](FMOD_Studio_EventInstance_GetParameterByIndex.html)\

[Studio::EventInstance::getParameterCount](FMOD_Studio_EventInstance_GetParameterCount.html)\

[Studio::EventInstance::getPaused](FMOD_Studio_EventInstance_GetPaused.html)\

[Studio::EventInstance::getPitch](FMOD_Studio_EventInstance_GetPitch.html)\

[Studio::EventInstance::getPlaybackState](FMOD_Studio_EventInstance_GetPlaybackState.html)\

[Studio::EventInstance::getTimelinePosition](FMOD_Studio_EventInstance_GetTimelinePosition.html)\

[Studio::EventInstance::getUserData](FMOD_Studio_EventInstance_GetUserData.html)\

[Studio::EventInstance::getVolume](FMOD_Studio_EventInstance_GetVolume.html)\

[Studio::EventInstance::isVirtual](FMOD_Studio_EventInstance_IsVirtual.html)\

[Studio::EventInstance::release](FMOD_Studio_EventInstance_Release.html)\

[Studio::EventInstance::set3DAttributes](FMOD_Studio_EventInstance_Set3DAttributes.html)\

[Studio::EventInstance::setCallback](FMOD_Studio_EventInstance_SetCallback.html)\

[Studio::EventInstance::setParameterValue](FMOD_Studio_EventInstance_SetParameterValue.html)\

[Studio::EventInstance::setParameterValueByIndex](FMOD_Studio_EventInstance_SetParameterValueByIndex.html)\

[Studio::EventInstance::setPaused](FMOD_Studio_EventInstance_SetPaused.html)\

[Studio::EventInstance::setPitch](FMOD_Studio_EventInstance_SetPitch.html)\

[Studio::EventInstance::setTimelinePosition](FMOD_Studio_EventInstance_SetTimelinePosition.html)\

[Studio::EventInstance::setUserData](FMOD_Studio_EventInstance_SetUserData.html)\

[Studio::EventInstance::setVolume](FMOD_Studio_EventInstance_SetVolume.html)\
 [Studio::EventInstance::start](FMOD_Studio_EventInstance_Start.html)\
 [Studio::EventInstance::stop](FMOD_Studio_EventInstance_Stop.html)\
 See Also --------

-   [Studio::EventDescription::createInstance](FMOD_Studio_EventDescription_CreateInstance.html)

Firelight Technologies FMOD Studio API

Functions
=========

[ParseID](FMOD_Studio_ParseID.html)\
 Firelight Technologies FMOD Studio API

C++ interfaces
==============

[System](studio_api_System.html)\
 [EventDescription](studio_api_EventDescription.html)\
 [EventInstance](studio_api_EventInstance.html)\
 [CueInstance](studio_api_CueInstance.html)\
 [ParameterInstance](studio_api_ParameterInstance.html)\
 [MixerStrip](studio_api_MixerStrip.html)\
 [Bank](studio_api_Bank.html)\
 Firelight Technologies FMOD Studio API

Studio::MixerStrip
==================

Represents either a VCA or a bus.

Functions
---------

[Studio::MixerStrip::getChannelGroup](FMOD_Studio_MixerStrip_GetChannelGroup.html)\

[Studio::MixerStrip::getFaderLevel](FMOD_Studio_MixerStrip_GetFaderLevel.html)\
 [Studio::MixerStrip::getID](FMOD_Studio_MixerStrip_GetID.html)\

[Studio::MixerStrip::getLoadingState](FMOD_Studio_MixerStrip_GetLoadingState.html)\
 [Studio::MixerStrip::getMute](FMOD_Studio_MixerStrip_GetMute.html)\
 [Studio::MixerStrip::getPath](FMOD_Studio_MixerStrip_GetPath.html)\
 [Studio::MixerStrip::getPaused](FMOD_Studio_MixerStrip_GetPaused.html)\
 [Studio::MixerStrip::release](FMOD_Studio_MixerStrip_Release.html)\

[Studio::MixerStrip::setFaderLevel](FMOD_Studio_MixerStrip_SetFaderLevel.html)\
 [Studio::MixerStrip::setMute](FMOD_Studio_MixerStrip_SetMute.html)\
 [Studio::MixerStrip::setPaused](FMOD_Studio_MixerStrip_SetPaused.html)\

[Studio::MixerStrip::stopAllEvents](FMOD_Studio_MixerStrip_StopAllEvents.html)\
 See Also --------

-   [Studio::System::getMixerStrip](FMOD_Studio_System_GetMixerStrip.html)

Firelight Technologies FMOD Studio API

Studio::ParameterInstance
=========================

A parameter instance for an FMOD Studio Event.

Functions
---------

[Studio::ParameterInstance::getDescription](FMOD_Studio_ParameterInstance_GetDescription.html)\

[Studio::ParameterInstance::getValue](FMOD_Studio_ParameterInstance_GetValue.html)\

[Studio::ParameterInstance::setValue](FMOD_Studio_ParameterInstance_SetValue.html)\
 See Also --------

-   [Studio::EventInstance::getParameter](FMOD_Studio_EventInstance_GetParameter.html)
-   [Studio::EventInstance::getParameterByIndex](FMOD_Studio_EventInstance_GetParameterByIndex.html)
-   [Studio::EventInstance::getParameterCount](FMOD_Studio_EventInstance_GetParameterCount.html)

Firelight Technologies FMOD Studio API

Structures
==========

[FMOD\_STUDIO\_ADVANCEDSETTINGS](FMOD_STUDIO_ADVANCEDSETTINGS.html)\
 [FMOD\_STUDIO\_BANK\_INFO](FMOD_STUDIO_BANK_INFO.html)\
 [FMOD\_STUDIO\_BUFFER\_INFO](FMOD_STUDIO_BUFFER_INFO.html)\
 [FMOD\_STUDIO\_BUFFER\_USAGE](FMOD_STUDIO_BUFFER_USAGE.html)\
 [FMOD\_STUDIO\_CPU\_USAGE](FMOD_STUDIO_CPU_USAGE.html)\

[FMOD\_STUDIO\_PARAMETER\_DESCRIPTION](FMOD_STUDIO_PARAMETER_DESCRIPTION.html)\

[FMOD\_STUDIO\_PROGRAMMER\_SOUND\_PROPERTIES](FMOD_STUDIO_PROGRAMMER_SOUND_PROPERTIES.html)\
 [FMOD\_STUDIO\_USER\_PROPERTY](FMOD_STUDIO_USER_PROPERTY.html)\
 Firelight Technologies FMOD Studio API

Studio::System
==============

The main system object for FMOD Studio.

Functions
---------

[Studio::System::create](FMOD_Studio_System_Create.html)\
 [Studio::System::flushCommands](FMOD_Studio_System_FlushCommands.html)\

[Studio::System::getAdvancedSettings](FMOD_Studio_System_GetAdvancedSettings.html)\
 [Studio::System::getBank](FMOD_Studio_System_GetBank.html)\
 [Studio::System::getBankCount](FMOD_Studio_System_GetBankCount.html)\
 [Studio::System::getBankList](FMOD_Studio_System_GetBankList.html)\

[Studio::System::getBufferUsage](FMOD_Studio_System_GetBufferUsage.html)\
 [Studio::System::getCPUUsage](FMOD_Studio_System_GetCPUUsage.html)\
 [Studio::System::getEvent](FMOD_Studio_System_GetEvent.html)\

[Studio::System::getListenerAttributes](FMOD_Studio_System_GetListenerAttributes.html)\

[Studio::System::getLowLevelSystem](FMOD_Studio_System_GetLowLevelSystem.html)\
 [Studio::System::getMixerStrip](FMOD_Studio_System_GetMixerStrip.html)\
 [Studio::System::initialize](FMOD_Studio_System_Initialize.html)\

[Studio::System::loadBankCustom](FMOD_Studio_System_LoadBankCustom.html)\
 [Studio::System::loadBankFile](FMOD_Studio_System_LoadBankFile.html)\

[Studio::System::loadBankMemory](FMOD_Studio_System_LoadBankMemory.html)\
 [Studio::System::lookupID](FMOD_Studio_System_LookupID.html)\
 [Studio::System::lookupPath](FMOD_Studio_System_LookupPath.html)\

[Studio::System::playbackCommands](FMOD_Studio_System_PlaybackCommands.html)\

[Studio::System::registerPlugin](FMOD_Studio_System_RegisterPlugin.html)\
 [Studio::System::release](FMOD_Studio_System_Release.html)\

[Studio::System::resetBufferUsage](FMOD_Studio_System_ResetBufferUsage.html)\

[Studio::System::setAdvancedSettings](FMOD_Studio_System_SetAdvancedSettings.html)\

[Studio::System::setListenerAttributes](FMOD_Studio_System_SetListenerAttributes.html)\

[Studio::System::startRecordCommands](FMOD_Studio_System_StartRecordCommands.html)\

[Studio::System::stopRecordCommands](FMOD_Studio_System_StopRecordCommands.html)\
 [Studio::System::unloadAll](FMOD_Studio_System_UnloadAll.html)\

[Studio::System::unregisterPlugin](FMOD_Studio_System_UnregisterPlugin.html)\
 [Studio::System::update](FMOD_Studio_System_Update.html)\
 Remarks -------

Initializing the FMOD Studio System object will also initialise the low
level System object.

See Also
--------

-   [Studio::System::create](FMOD_Studio_System_Create.html)
-   [Studio::System::initialize](FMOD_Studio_System_Initialize.html)

