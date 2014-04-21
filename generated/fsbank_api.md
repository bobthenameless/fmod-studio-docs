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

Remarks
-------

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

See Also
--------

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

See Also
--------

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

See Also
--------

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

See Also
--------

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

Remarks
-------

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

See Also
--------

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

Remarks
-------

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

Remarks
-------

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

See Also
--------

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

