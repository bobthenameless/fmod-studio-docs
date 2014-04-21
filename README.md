This is a project to strip the FMOD Studio API out of the .chm file and into md files. Currently very messy. FMOD can be downloaded/purchased at http://www.fmod.org/ and the .chm file can be found in API_INSTALL_DIRECTORY/docs.

FSBank API
==========

[Functions][]\
 [Callbacks][]\
 [Structures][]\
 [Defines][]\
 [Enumerations][]\
 Firelight Technologies FMOD Studio API

Callbacks
=========

[FSBANK\_MEMORY\_ALLOC\_CALLBACK][]\
 [FSBANK\_MEMORY\_FREE\_CALLBACK][]\
 [FSBANK\_MEMORY\_REALLOC\_CALLBACK][]\
 Firelight Technologies FMOD Studio API

Defines
=======

[FSBANK\_BUILDFLAGS][]\
 [FSBANK\_INITFLAGS][]\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FSBANK\_FORMAT][]\
 [FSBANK\_FSBVERSION][]\
 [FSBANK\_RESULT][]\
 [FSBANK\_SPEAKERMAP][]\
 [FSBANK\_STATE][]\
 Firelight Technologies FMOD Studio API

Functions
=========

[FSBank\_Build][] [FSBank\_BuildCancel][]
[FSBank\_FetchNextProgressItem][] [FSBank\_Init][]
[FSBank\_MemoryGetStats][] [FSBank\_MemoryInit][] [FSBank\_Release][]
[FSBank\_ReleaseProgressItem][]

Firelight Technologies FMOD Studio API

Structures
==========

[FSBANK\_PROGRESSITEM][]\
 [FSBANK\_STATEDATA\_FAILED][]\
 [FSBANK\_STATEDATA\_WARNING][]\
 [FSBANK\_SUBSOUND][]\
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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
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

-   [FSBANK\_SUBSOUND][]
-   [FSBANK\_FORMAT][]
-   [FSBANK\_BUILDFLAGS][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBank\_BuildCancel
===================

Halt the build in progress, must be called from a different thread to
[FSBank\_Build][].

### C Syntax

``` {.syntax}
FSBANK_RESULT FSBank_BuildCancel();
```

Return Values
-------------

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 See Also --------

-   [FSBank\_Build][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_BUILDFLAGS
==================

Bit fields to use with [FSBank\_Build][] and in [FSBANK\_SUBSOUND][] to
control how subsounds are encoded.

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
streams must remained interleaved), allows [FMOD\_OPENMEMORY\_POINT][].

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

-   [FSBank\_Init][]
-   [FSBANK\_SUBSOUND][]

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
after the build for a report. Call [FSBank\_ReleaseProgressItem][] to
free allocated memory.

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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 See Also --------

-   [FSBank\_ReleaseProgressItem][]
-   [FSBANK\_PROGRESSITEM][]

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

-   [FSBank\_Build][]

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

-   [FSBank\_Init][]

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
[FSBANK\_FSBVERSION\_FSB5][FSBANK\_FSBVERSION] is supported.

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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 See Also --------

-   [FSBANK\_FSBVERSION][]
-   [FSBANK\_INITFLAGS][]
-   [FSBank\_Release][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_INITFLAGS
=================

Bit fields to use with [FSBank\_Init][] to control the general operation
of the library.

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

-   [FSBank\_Init][]

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
[FSBank\_Init][]. Optional. Specify 0 or NULL to ignore.

Return Values
-------------

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 See Also --------

-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK][]
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK][]
-   [FSBANK\_MEMORY\_FREE\_CALLBACK][]

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

-   [FSBank\_MemoryInit][]
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK][]
-   [FSBANK\_MEMORY\_FREE\_CALLBACK][]

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

-   [FSBank\_MemoryInit][]
-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK][]
-   [FSBANK\_MEMORY\_REALLOC\_CALLBACK][]

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

-   [FSBank\_MemoryInit][]
-   [FSBANK\_MEMORY\_ALLOC\_CALLBACK][]
-   [FSBANK\_MEMORY\_FREE\_CALLBACK][]

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

Index into the subsound list passed to [FSBank\_Build][] that this
update relates to (-1 indicates no specific subsound).

*threadIndex*

Which thread index is serving this update (-1 indicates
[FSBank\_Build][] / main thread).

*state*

Progress through the encoding process.

*stateData*

Cast to state specific data structure for extra information.

See Also
--------

-   [FSBank\_Build][]
-   [FSBank\_FetchNextProgressItem][]
-   [FSBank\_ReleaseProgressItem][]
-   [FSBANK\_STATE][]

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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 Remarks -------

All progress items retrieved with [FSBank\_FetchNextProgressItem][] will
be released by this function.

See Also
--------

-   [FSBank\_Init][]
-   [FSBank\_FetchNextProgressItem][]

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

If the function succeeds then the return value is [FSBANK\_OK][].\
 If the function fails then the return value will be one of the values
defined in the [FSBANK\_RESULT][FSBANK\_OK] enumeration.\
 See Also --------

-   [FSBank\_FetchNextProgressItem][]
-   [FSBANK\_PROGRESSITEM][]

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

[FSBANK\_BUILD\_OPTIMIZESAMPLERATE][FSBANK\_BUILDFLAGS] flag ignored:
MP2, MP3 and CELT formats, and the USEBASICHEADERS flag make this option
irrelevant.

*FSBANK\_WARN\_IGNORED\_FILTERHIGHFREQ*

[FSBANK\_BUILD\_FILTERHIGHFREQ][FSBANK\_BUILDFLAGS] flag ignored:
feature only supported by XMA format.

*FSBANK\_WARN\_IGNORED\_DISABLESEEKING*

[FSBANK\_BUILD\_DISABLESEEKING][FSBANK\_BUILDFLAGS] flag ignored:
feature only supported by XMA format.

*FSBANK\_WARN\_IGNORED\_DONTINTERLEAVE*

[FSBANK\_BUILD\_DONTINTERLEAVE][FSBANK\_BUILDFLAGS] flag ignored:
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

-   [FSBANK\_SUBSOUND][]

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

An error has occurred, check data (as [FSBANK\_STATEDATA\_FAILED][]) for
details.

*FSBANK\_STATE\_WARNING*

A warning has been issued, check data (as
[FSBANK\_STATEDATA\_WARNING][]) for details.

See Also
--------

-   [FSBANK\_PROGRESSITEM][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_STATEDATA\_FAILED
=========================

Extra state data for [FSBANK\_STATE\_FAILED][FSBANK\_STATE]

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

Cast stateData in [FSBANK\_PROGRESSITEM][] to this struct if the state
is [FSBANK\_STATE\_FAILED][FSBANK\_STATE]

See Also
--------

-   [FSBANK\_STATE\_FAILED][FSBANK\_STATE]
-   [FSBANK\_PROGRESSITEM][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\
 Firelight Technologies FMOD Studio API

FSBANK\_STATEDATA\_WARNING
==========================

Extra state data for [FSBANK\_STATEDATA\_WARNING][]

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

Cast stateData in [FSBANK\_PROGRESSITEM][] to this struct if the state
is [FSBANK\_STATE\_WARNING][FSBANK\_STATE]

See Also
--------

-   [FSBANK\_STATE\_WARNING][FSBANK\_STATE]
-   [FSBANK\_PROGRESSITEM][]

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
[FSBank\_Build][].

*overrideQuality*

Override the quality setting passed to [FSBank\_Build][].

*desiredSampleRate*

Resample to this sample rate (ignores optimize sample rate setting), up
to 192000Hz.

*percentOptimizedRate*

If using [FSBANK\_BUILD\_OPTIMIZESAMPLERATE][FSBANK\_BUILDFLAGS], this
is the percentage of that rate to be used, up to 100.0%.

See Also
--------

-   [FSBank\_Build][]
-   [FSBANK\_BUILD\_OPTIMIZESAMPLERATE][FSBANK\_BUILDFLAGS]
-   [FSBANK\_SPEAKERMAP][]
-   [FSBANK\_BUILDFLAGS][]

\
\
\
 Version 1.03.06 Built on Apr 17, 2014

\

Firelight Technologies FMOD Studio API

Low Level API
=============

[C++ interfaces][]\
 [Functions][1]\
 [Callbacks][2]\
 [Structures][3]\
 [Defines][4]\
 [Enumerations][5]\
 Firelight Technologies FMOD Studio API

Callbacks
=========

[FMOD\_3D\_ROLLOFF\_CALLBACK][]\
 [FMOD\_CHANNELCONTROL\_CALLBACK][]\
 [FMOD\_CODEC\_CLOSE\_CALLBACK][]\
 [FMOD\_CODEC\_GETLENGTH\_CALLBACK][]\
 [FMOD\_CODEC\_GETPOSITION\_CALLBACK][]\
 [FMOD\_CODEC\_METADATA\_CALLBACK][]\
 [FMOD\_CODEC\_OPEN\_CALLBACK][]\
 [FMOD\_CODEC\_READ\_CALLBACK][]\
 [FMOD\_CODEC\_SETPOSITION\_CALLBACK][]\
 [FMOD\_CODEC\_SOUNDCREATE\_CALLBACK][]\
 [FMOD\_DSP\_CREATE\_CALLBACK][]\
 [FMOD\_DSP\_DIALOG\_CALLBACK][]\
 [FMOD\_DSP\_GETPARAM\_BOOL\_CALLBACK][]\
 [FMOD\_DSP\_GETPARAM\_DATA\_CALLBACK][]\
 [FMOD\_DSP\_GETPARAM\_FLOAT\_CALLBACK][]\
 [FMOD\_DSP\_GETPARAM\_INT\_CALLBACK][]\
 [FMOD\_DSP\_PROCESS\_CALLBACK][]\
 [FMOD\_DSP\_READ\_CALLBACK][]\
 [FMOD\_DSP\_RELEASE\_CALLBACK][]\
 [FMOD\_DSP\_RESET\_CALLBACK][]\
 [FMOD\_DSP\_SETPARAM\_BOOL\_CALLBACK][]\
 [FMOD\_DSP\_SETPARAM\_DATA\_CALLBACK][]\
 [FMOD\_DSP\_SETPARAM\_FLOAT\_CALLBACK][]\
 [FMOD\_DSP\_SETPARAM\_INT\_CALLBACK][]\
 [FMOD\_DSP\_SETPOSITION\_CALLBACK][]\
 [FMOD\_DSP\_SHOULDIPROCESS\_CALLBACK][]\
 [FMOD\_FILE\_ASYNCCANCEL\_CALLBACK][]\
 [FMOD\_FILE\_ASYNCREAD\_CALLBACK][]\
 [FMOD\_FILE\_CLOSE\_CALLBACK][]\
 [FMOD\_FILE\_OPEN\_CALLBACK][]\
 [FMOD\_FILE\_READ\_CALLBACK][]\
 [FMOD\_FILE\_SEEK\_CALLBACK][]\
 [FMOD\_MEMORY\_ALLOC\_CALLBACK][]\
 [FMOD\_MEMORY\_FREE\_CALLBACK][]\
 [FMOD\_MEMORY\_REALLOC\_CALLBACK][]\
 [FMOD\_OUTPUT\_CLOSE\_CALLBACK][]\
 [FMOD\_OUTPUT\_GETDRIVERINFO\_CALLBACK][]\
 [FMOD\_OUTPUT\_GETHANDLE\_CALLBACK][]\
 [FMOD\_OUTPUT\_GETNUMDRIVERS\_CALLBACK][]\
 [FMOD\_OUTPUT\_GETPOSITION\_CALLBACK][]\
 [FMOD\_OUTPUT\_INIT\_CALLBACK][]\
 [FMOD\_OUTPUT\_LOCK\_CALLBACK][]\
 [FMOD\_OUTPUT\_READFROMMIXER][]\
 [FMOD\_OUTPUT\_UNLOCK\_CALLBACK][]\
 [FMOD\_OUTPUT\_UPDATE\_CALLBACK][]\
 [FMOD\_SOUND\_NONBLOCK\_CALLBACK][]\
 [FMOD\_SOUND\_PCMREAD\_CALLBACK][]\
 [FMOD\_SOUND\_PCMSETPOS\_CALLBACK][]\
 [FMOD\_SYSTEM\_CALLBACK][]\
 Firelight Technologies FMOD Studio API

Channel
=======

Functions
---------

[Channel::addDSP][]\
 [Channel::addFadePoint][]\
 [Channel::get3DAttributes][]\
 [Channel::get3DConeOrientation][]\
 [Channel::get3DConeSettings][]\
 [Channel::get3DCustomRolloff][]\
 [Channel::get3DDistanceFilter][]\
 [Channel::get3DDopplerLevel][]\
 [Channel::get3DLevel][]\
 [Channel::get3DMinMaxDistance][]\
 [Channel::get3DOcclusion][]\
 [Channel::get3DSpread][]\
 [Channel::getAudibility][]\
 [Channel::getChannelGroup][]\
 [Channel::getCurrentSound][]\
 [Channel::getDSP][]\
 [Channel::getDSPClock][]\
 [Channel::getDelay][]\
 [Channel::getFadePoints][]\
 [Channel::getFrequency][]\
 [Channel::getIndex][]\
 [Channel::getLoopCount][]\
 [Channel::getLoopPoints][]\
 [Channel::getLowPassGain][]\
 [Channel::getMixMatrix][]\
 [Channel::getMode][]\
 [Channel::getMute][]\
 [Channel::getNumDSPs][]\
 [Channel::getPaused][]\
 [Channel::getPitch][]\
 [Channel::getPosition][]\
 [Channel::getPriority][]\
 [Channel::getReverbProperties][]\
 [Channel::getSystemObject][]\
 [Channel::getUserData][]\
 [Channel::getVolume][]\
 [Channel::getVolumeRamp][]\
 [Channel::isPlaying][]\
 [Channel::isVirtual][]\
 [Channel::removeDSP][]\
 [Channel::removeFadePoints][]\
 [Channel::set3DAttributes][]\
 [Channel::set3DConeOrientation][]\
 [Channel::set3DConeSettings][]\
 [Channel::set3DCustomRolloff][]\
 [Channel::set3DDistanceFilter][]\
 [Channel::set3DDopplerLevel][]\
 [Channel::set3DLevel][]\
 [Channel::set3DMinMaxDistance][]\
 [Channel::set3DOcclusion][]\
 [Channel::set3DSpread][]\
 [Channel::setCallback][]\
 [Channel::setChannelGroup][]\
 [Channel::setDelay][]\
 [Channel::setFrequency][]\
 [Channel::setLoopCount][]\
 [Channel::setLoopPoints][]\
 [Channel::setLowPassGain][]\
 [Channel::setMixLevelsInput][]\
 [Channel::setMixLevelsOutput][]\
 [Channel::setMixMatrix][]\
 [Channel::setMode][]\
 [Channel::setMute][]\
 [Channel::setPan][]\
 [Channel::setPaused][]\
 [Channel::setPitch][]\
 [Channel::setPosition][]\
 [Channel::setPriority][]\
 [Channel::setReverbProperties][]\
 [Channel::setUserData][]\
 [Channel::setVolume][]\
 [Channel::setVolumeRamp][]\
 [Channel::stop][]\
 Firelight Technologies FMOD Studio API

ChannelControl
==============

The base class for both Channels and Channel Groups.

Functions
---------

[ChannelControl::addDSP][]\
 [ChannelControl::addFadePoint][]\
 [ChannelControl::get3DAttributes][]\
 [ChannelControl::get3DConeOrientation][]\
 [ChannelControl::get3DConeSettings][]\
 [ChannelControl::get3DCustomRolloff][]\
 [ChannelControl::get3DDistanceFilter][]\
 [ChannelControl::get3DDopplerLevel][]\
 [ChannelControl::get3DLevel][]\
 [ChannelControl::get3DMinMaxDistance][]\
 [ChannelControl::get3DOcclusion][]\
 [ChannelControl::get3DSpread][]\
 [ChannelControl::getAudibility][]\
 [ChannelControl::getDSP][]\
 [ChannelControl::getDSPClock][]\
 [ChannelControl::getDelay][]\
 [ChannelControl::getFadePoints][]\
 [ChannelControl::getLowPassGain][]\
 [ChannelControl::getMixMatrix][]\
 [ChannelControl::getMute][]\
 [ChannelControl::getNumDSPs][]\
 [ChannelControl::getPaused][]\
 [ChannelControl::getPitch][]\
 [ChannelControl::getReverbProperties][]\
 [ChannelControl::getSystemObject][]\
 [ChannelControl::getUserData][]\
 [ChannelControl::getVolume][]\
 [ChannelControl::getVolumeRamp][]\
 [ChannelControl::isPlaying][]\
 [ChannelControl::removeDSP][]\
 [ChannelControl::removeFadePoints][]\
 [ChannelControl::set3DAttributes][]\
 [ChannelControl::set3DConeOrientation][]\
 [ChannelControl::set3DConeSettings][]\
 [ChannelControl::set3DCustomRolloff][]\
 [ChannelControl::set3DDistanceFilter][]\
 [ChannelControl::set3DDopplerLevel][]\
 [ChannelControl::set3DLevel][]\
 [ChannelControl::set3DMinMaxDistance][]\
 [ChannelControl::set3DOcclusion][]\
 [ChannelControl::set3DSpread][]\
 [ChannelControl::setCallback][]\
 [ChannelControl::setDelay][]\
 [ChannelControl::setLowPassGain][]\
 [ChannelControl::setMixLevelsInput][]\
 [ChannelControl::setMixLevelsOutput][]\
 [ChannelControl::setMixMatrix][]\
 [ChannelControl::setMute][]\
 [ChannelControl::setPan][]\
 [ChannelControl::setPaused][]\
 [ChannelControl::setPitch][]\
 [ChannelControl::setReverbProperties][]\
 [ChannelControl::setUserData][]\
 [ChannelControl::setVolume][]\
 [ChannelControl::setVolumeRamp][]\
 [ChannelControl::stop][]\
 Firelight Technologies FMOD Studio API

ChannelGroup
============

Functions
---------

[ChannelGroup::addDSP][]\
 [ChannelGroup::addFadePoint][]\
 [ChannelGroup::addGroup][]\
 [ChannelGroup::get3DAttributes][]\
 [ChannelGroup::get3DConeOrientation][]\
 [ChannelGroup::get3DConeSettings][]\
 [ChannelGroup::get3DCustomRolloff][]\
 [ChannelGroup::get3DDistanceFilter][]\
 [ChannelGroup::get3DDopplerLevel][]\
 [ChannelGroup::get3DLevel][]\
 [ChannelGroup::get3DMinMaxDistance][]\
 [ChannelGroup::get3DOcclusion][]\
 [ChannelGroup::get3DSpread][]\
 [ChannelGroup::getAudibility][]\
 [ChannelGroup::getChannel][]\
 [ChannelGroup::getDSP][]\
 [ChannelGroup::getDSPClock][]\
 [ChannelGroup::getDSPIndex][]\
 [ChannelGroup::getDelay][]\
 [ChannelGroup::getFadePoints][]\
 [ChannelGroup::getGroup][]\
 [ChannelGroup::getLowPassGain][]\
 [ChannelGroup::getMixMatrix][]\
 [ChannelGroup::getMute][]\
 [ChannelGroup::getName][]\
 [ChannelGroup::getNumChannels][]\
 [ChannelGroup::getNumDSPs][]\
 [ChannelGroup::getNumGroups][]\
 [ChannelGroup::getParentGroup][]\
 [ChannelGroup::getPaused][]\
 [ChannelGroup::getPitch][]\
 [ChannelGroup::getReverbProperties][]\
 [ChannelGroup::getSystemObject][]\
 [ChannelGroup::getUserData][]\
 [ChannelGroup::getVolume][]\
 [ChannelGroup::getVolumeRamp][]\
 [ChannelGroup::isPlaying][]\
 [ChannelGroup::release][]\
 [ChannelGroup::removeDSP][]\
 [ChannelGroup::removeFadePoints][]\
 [ChannelGroup::set3DAttributes][]\
 [ChannelGroup::set3DConeOrientation][]\
 [ChannelGroup::set3DConeSettings][]\
 [ChannelGroup::set3DCustomRolloff][]\
 [ChannelGroup::set3DDistanceFilter][]\
 [ChannelGroup::set3DDopplerLevel][]\
 [ChannelGroup::set3DLevel][]\
 [ChannelGroup::set3DMinMaxDistance][]\
 [ChannelGroup::set3DOcclusion][]\
 [ChannelGroup::set3DSpread][]\
 [ChannelGroup::setCallback][]\
 [ChannelGroup::setDSPIndex][]\
 [ChannelGroup::setDelay][]\
 [ChannelGroup::setLowPassGain][]\
 [ChannelGroup::setMixLevelsInput][]\
 [ChannelGroup::setMixLevelsOutput][]\
 [ChannelGroup::setMixMatrix][]\
 [ChannelGroup::setMute][]\
 [ChannelGroup::setPan][]\
 [ChannelGroup::setPaused][]\
 [ChannelGroup::setPitch][]\
 [ChannelGroup::setReverbProperties][]\
 [ChannelGroup::setUserData][]\
 [ChannelGroup::setVolume][]\
 [ChannelGroup::setVolumeRamp][]\
 [ChannelGroup::stop][]\
 Firelight Technologies FMOD Studio API

Defines
=======

[FMOD\_CHANNELMASK][]\
 [FMOD\_CODEC\_WAVEFORMAT\_VERSION][]\
 [FMOD\_DEBUGLEVEL][]\
 [FMOD\_INITFLAGS][]\
 [FMOD\_MEMORY\_TYPE][]\
 [FMOD\_MODE][FMOD\_OPENMEMORY\_POINT]\
 [FMOD\_PORT\_INDEX][]\
 [FMOD\_REVERB\_PRESETS][]\
 [FMOD\_SYSTEM\_CALLBACK\_TYPE][]\
 [FMOD\_TIMEUNIT][]\
 Firelight Technologies FMOD Studio API

DSP
===

Functions
---------

[DSP::addInput][]\
 [DSP::disconnectAll][]\
 [DSP::disconnectFrom][]\
 [DSP::getActive][]\
 [DSP::getBypass][]\
 [DSP::getChannelFormat][]\
 [DSP::getDataParameterIndex][]\
 [DSP::getIdle][]\
 [DSP::getInfo][]\
 [DSP::getInput][]\
 [DSP::getMeteringEnabled][]\
 [DSP::getMeteringInfo][]\
 [DSP::getNumInputs][]\
 [DSP::getNumOutputs][]\
 [DSP::getNumParameters][]\
 [DSP::getOutput][]\
 [DSP::getOutputChannelFormat][]\
 [DSP::getParameterBool][]\
 [DSP::getParameterData][]\
 [DSP::getParameterFloat][]\
 [DSP::getParameterInfo][]\
 [DSP::getParameterInt][]\
 [DSP::getSystemObject][]\
 [DSP::getType][]\
 [DSP::getUserData][]\
 [DSP::release][]\
 [DSP::reset][]\
 [DSP::setActive][]\
 [DSP::setBypass][]\
 [DSP::setChannelFormat][]\
 [DSP::setMeteringEnabled][]\
 [DSP::setParameterBool][]\
 [DSP::setParameterData][]\
 [DSP::setParameterFloat][]\
 [DSP::setParameterInt][]\
 [DSP::setUserData][]\
 [DSP::showConfigDialog][]\
 Firelight Technologies FMOD Studio API

DSPConnection
=============

Functions
---------

[DSPConnection::getInput][]\
 [DSPConnection::getMix][]\
 [DSPConnection::getMixMatrix][]\
 [DSPConnection::getOutput][]\
 [DSPConnection::getType][]\
 [DSPConnection::getUserData][]\
 [DSPConnection::setMix][]\
 [DSPConnection::setMixMatrix][]\
 [DSPConnection::setUserData][]\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FMOD\_CHANNELCONTROL\_CALLBACK\_TYPE][]\
 [FMOD\_CHANNELCONTROL\_DSP\_INDEX][]\
 [FMOD\_CHANNELCONTROL\_TYPE][]\
 [FMOD\_CHANNELORDER][]\
 [FMOD\_DSPCONNECTION\_TYPE][]\
 [FMOD\_DSP\_CHORUS][]\
 [FMOD\_DSP\_COMPRESSOR][]\
 [FMOD\_DSP\_DELAY][]\
 [FMOD\_DSP\_DISTORTION][]\
 [FMOD\_DSP\_ECHO][]\
 [FMOD\_DSP\_ENVELOPEFOLLOWER][]\
 [FMOD\_DSP\_FFT][]\
 [FMOD\_DSP\_FFT\_WINDOW][]\
 [FMOD\_DSP\_FLANGE][]\
 [FMOD\_DSP\_HIGHPASS][]\
 [FMOD\_DSP\_HIGHPASS\_SIMPLE][]\
 [FMOD\_DSP\_ITECHO][]\
 [FMOD\_DSP\_ITLOWPASS][]\
 [FMOD\_DSP\_LIMITER][]\
 [FMOD\_DSP\_LOWPASS][]\
 [FMOD\_DSP\_LOWPASS\_SIMPLE][]\
 [FMOD\_DSP\_NORMALIZE][]\
 [FMOD\_DSP\_OSCILLATOR][]\
 [FMOD\_DSP\_PAN][]\
 [FMOD\_DSP\_PAN\_3D\_EXTENT\_MODE\_TYPE][]\
 [FMOD\_DSP\_PAN\_3D\_ROLLOFF\_TYPE][]\
 [FMOD\_DSP\_PAN\_SURROUND\_FROM\_STEREO\_MODE\_TYPE][]\
 [FMOD\_DSP\_PARAMEQ][]\
 [FMOD\_DSP\_PARAMETER\_DATA\_TYPE][]\
 [FMOD\_DSP\_PARAMETER\_FLOAT\_MAPPING\_TYPE][]\
 [FMOD\_DSP\_PARAMETER\_TYPE][]\
 [FMOD\_DSP\_PITCHSHIFT][]\
 [FMOD\_DSP\_PROCESS\_OPERATION][]\
 [FMOD\_DSP\_RESAMPLER][]\
 [FMOD\_DSP\_RETURN][]\
 [FMOD\_DSP\_SEND][]\
 [FMOD\_DSP\_SFXREVERB][]\
 [FMOD\_DSP\_THREE\_EQ][]\
 [FMOD\_DSP\_THREE\_EQ\_CROSSOVERSLOPE\_TYPE][]\
 [FMOD\_DSP\_TREMOLO][]\
 [FMOD\_DSP\_TYPE][]\
 [FMOD\_ERRORCALLBACK\_INSTANCETYPE][]\
 [FMOD\_OPENSTATE][]\
 [FMOD\_OUTPUTTYPE][]\
 [FMOD\_PLUGINTYPE][]\
 [FMOD\_RESULT][]\
 [FMOD\_SOUNDGROUP\_BEHAVIOR][]\
 [FMOD\_SOUND\_FORMAT][]\
 [FMOD\_SOUND\_TYPE][]\
 [FMOD\_SPEAKER][]\
 [FMOD\_SPEAKERMODE][]\
 [FMOD\_TAGDATATYPE][]\
 [FMOD\_TAGTYPE][]\
 Firelight Technologies FMOD Studio API

Functions
=========

[Debug\_GetLevel][]\
 [Debug\_SetLevel][]\
 [File\_GetDiskBusy][]\
 [File\_SetDiskBusy][]\
 [Memory\_GetStats][]\
 [Memory\_Initialize][]\
 [System\_Create][]\
 Firelight Technologies FMOD Studio API

Geometry
========

Functions
---------

[Geometry::addPolygon][]\
 [Geometry::getActive][]\
 [Geometry::getMaxPolygons][]\
 [Geometry::getNumPolygons][]\
 [Geometry::getPolygonAttributes][]\
 [Geometry::getPolygonNumVertices][]\
 [Geometry::getPolygonVertex][]\
 [Geometry::getPosition][]\
 [Geometry::getRotation][]\
 [Geometry::getScale][]\
 [Geometry::getUserData][]\
 [Geometry::release][]\
 [Geometry::save][]\
 [Geometry::setActive][]\
 [Geometry::setPolygonAttributes][]\
 [Geometry::setPolygonVertex][]\
 [Geometry::setPosition][]\
 [Geometry::setRotation][]\
 [Geometry::setScale][]\
 [Geometry::setUserData][]\
 Firelight Technologies FMOD Studio API

C++ interfaces
==============

[System][]\
 [Sound][]\
 [ChannelControl][]\
 [Channel][]\
 [ChannelGroup][]\
 [SoundGroup][]\
 [DSP][]\
 [DSPConnection][]\
 [Geometry][]\
 [Reverb3D][]\
 Firelight Technologies FMOD Studio API

Reverb3D
========

Functions
---------

[Reverb3D::get3DAttributes][]\
 [Reverb3D::getActive][]\
 [Reverb3D::getProperties][]\
 [Reverb3D::getUserData][]\
 [Reverb3D::release][]\
 [Reverb3D::set3DAttributes][]\
 [Reverb3D::setActive][]\
 [Reverb3D::setProperties][]\
 [Reverb3D::setUserData][]\
 Firelight Technologies FMOD Studio API

Sound
=====

Functions
---------

[Sound::addSyncPoint][]\
 [Sound::deleteSyncPoint][]\
 [Sound::get3DConeSettings][]\
 [Sound::get3DCustomRolloff][]\
 [Sound::get3DMinMaxDistance][]\
 [Sound::getDefaults][]\
 [Sound::getFormat][]\
 [Sound::getLength][]\
 [Sound::getLoopCount][]\
 [Sound::getLoopPoints][]\
 [Sound::getMode][]\
 [Sound::getMusicChannelVolume][]\
 [Sound::getMusicNumChannels][]\
 [Sound::getMusicSpeed][]\
 [Sound::getName][]\
 [Sound::getNumSubSounds][]\
 [Sound::getNumSyncPoints][]\
 [Sound::getNumTags][]\
 [Sound::getOpenState][]\
 [Sound::getSoundGroup][]\
 [Sound::getSubSound][]\
 [Sound::getSubSoundParent][]\
 [Sound::getSyncPoint][]\
 [Sound::getSyncPointInfo][]\
 [Sound::getSystemObject][]\
 [Sound::getTag][]\
 [Sound::getUserData][]\
 [Sound::lock][]\
 [Sound::readData][]\
 [Sound::release][]\
 [Sound::seekData][]\
 [Sound::set3DConeSettings][]\
 [Sound::set3DCustomRolloff][]\
 [Sound::set3DMinMaxDistance][]\
 [Sound::setDefaults][]\
 [Sound::setLoopCount][]\
 [Sound::setLoopPoints][]\
 [Sound::setMode][]\
 [Sound::setMusicChannelVolume][]\
 [Sound::setMusicSpeed][]\
 [Sound::setSoundGroup][]\
 [Sound::setSubSound][]\
 [Sound::setUserData][]\
 [Sound::unlock][]\
 Firelight Technologies FMOD Studio API

SoundGroup
==========

Functions
---------

[SoundGroup::getMaxAudible][]\
 [SoundGroup::getMaxAudibleBehavior][]\
 [SoundGroup::getMuteFadeSpeed][]\
 [SoundGroup::getName][]\
 [SoundGroup::getNumPlaying][]\
 [SoundGroup::getNumSounds][]\
 [SoundGroup::getSound][]\
 [SoundGroup::getSystemObject][]\
 [SoundGroup::getUserData][]\
 [SoundGroup::getVolume][]\
 [SoundGroup::release][]\
 [SoundGroup::setMaxAudible][]\
 [SoundGroup::setMaxAudibleBehavior][]\
 [SoundGroup::setMuteFadeSpeed][]\
 [SoundGroup::setUserData][]\
 [SoundGroup::setVolume][]\
 [SoundGroup::stop][]\
 Firelight Technologies FMOD Studio API

Structures
==========

[FMOD\_3D\_ATTRIBUTES][]\
 [FMOD\_ADVANCEDSETTINGS][]\
 [FMOD\_ASYNCREADINFO][]\
 [FMOD\_CODEC\_DESCRIPTION][]\
 [FMOD\_CODEC\_STATE][]\
 [FMOD\_CODEC\_WAVEFORMAT][]\
 [FMOD\_CREATESOUNDEXINFO][]\
 [FMOD\_DSP\_BUFFER\_ARRAY][]\
 [FMOD\_DSP\_DESCRIPTION][]\
 [FMOD\_DSP\_METERING\_INFO][]\
 [FMOD\_DSP\_PARAMETER\_3DATTRIBUTES][]\
 [FMOD\_DSP\_PARAMETER\_DESC][]\
 [FMOD\_DSP\_PARAMETER\_DESC\_BOOL][]\
 [FMOD\_DSP\_PARAMETER\_DESC\_DATA][]\
 [FMOD\_DSP\_PARAMETER\_DESC\_FLOAT][]\
 [FMOD\_DSP\_PARAMETER\_DESC\_INT][]\
 [FMOD\_DSP\_PARAMETER\_OVERALLGAIN][]\
 [FMOD\_DSP\_PARAMETER\_SIDECHAIN][]\
 [FMOD\_DSP\_STATE][]\
 [FMOD\_DSP\_STATE\_SYSTEMCALLBACKS][]\
 [FMOD\_ERRORCALLBACK\_INFO][]\
 [FMOD\_GUID][]\
 [FMOD\_OUTPUT\_DESCRIPTION][]\
 [FMOD\_OUTPUT\_STATE][]\
 [FMOD\_REVERB\_PROPERTIES][]\
 [FMOD\_TAG][]\
 [FMOD\_VECTOR][]\
 [piecewiselinearmapping][]\
 Firelight Technologies FMOD Studio API

System
======

The main object for the FMOD Low Level System.

Functions
---------

[System::attachChannelGroupToPort][]\
 [System::attachFileSystem][]\
 [System::close][]\
 [System::createChannelGroup][]\
 [System::createDSP][]\
 [System::createDSPByPlugin][]\
 [System::createDSPByType][]\
 [System::createGeometry][]\
 [System::createReverb3D][]\
 [System::createSound][]\
 [System::createSoundGroup][]\
 [System::createStream][]\
 [System::detachChannelGroupFromPort][]\
 [System::get3DListenerAttributes][]\
 [System::get3DNumListeners][]\
 [System::get3DSettings][]\
 [System::getAdvancedSettings][]\
 [System::getCPUUsage][]\
 [System::getChannel][]\
 [System::getChannelsPlaying][]\
 [System::getDSPBufferSize][]\
 [System::getDSPInfoByPlugin][]\
 [System::getDriver][]\
 [System::getDriverInfo][]\
 [System::getGeometryOcclusion][]\
 [System::getGeometrySettings][]\
 [System::getMasterChannelGroup][]\
 [System::getMasterSoundGroup][]\
 [System::getNetworkProxy][]\
 [System::getNetworkTimeout][]\
 [System::getNumDrivers][]\
 [System::getNumPlugins][]\
 [System::getOutput][]\
 [System::getOutputByPlugin][]\
 [System::getOutputHandle][]\
 [System::getPluginHandle][]\
 [System::getPluginInfo][]\
 [System::getRecordDriverInfo][]\
 [System::getRecordNumDrivers][]\
 [System::getRecordPosition][]\
 [System::getReverbProperties][]\
 [System::getSoftwareChannels][]\
 [System::getSoftwareFormat][]\
 [System::getSoundRAM][]\
 [System::getSpeakerPosition][]\
 [System::getStreamBufferSize][]\
 [System::getUserData][]\
 [System::getVersion][]\
 [System::init][]\
 [System::isRecording][]\
 [System::loadGeometry][]\
 [System::loadPlugin][]\
 [System::lockDSP][]\
 [System::mixerResume][]\
 [System::mixerSuspend][]\
 [System::playDSP][]\
 [System::playSound][]\
 [System::recordStart][]\
 [System::recordStop][]\
 [System::registerCodec][]\
 [System::registerDSP][]\
 [System::release][]\
 [System::set3DListenerAttributes][]\
 [System::set3DNumListeners][]\
 [System::set3DRolloffCallback][]\
 [System::set3DSettings][]\
 [System::setAdvancedSettings][]\
 [System::setCallback][]\
 [System::setDSPBufferSize][]\
 [System::setDriver][]\
 [System::setFileSystem][]\
 [System::setGeometrySettings][]\
 [System::setNetworkProxy][]\
 [System::setNetworkTimeout][]\
 [System::setOutput][]\
 [System::setOutputByPlugin][]\
 [System::setPluginPath][]\
 [System::setReverbProperties][]\
 [System::setSoftwareChannels][]\
 [System::setSoftwareFormat][]\
 [System::setSpeakerPosition][]\
 [System::setStreamBufferSize][]\
 [System::setUserData][]\
 [System::unloadPlugin][]\
 [System::unlockDSP][]\
 [System::update][]\
 Remarks -------

When using FMOD Studio, this system object will be automatically
instantiated as part of [Studio::System::initialize][].

See Also
--------

-   [Studio::System::getLowLevelSystem][]

Firelight Technologies FMOD Studio API

Studio API
==========

[C++ interfaces][6]\
 [Functions][7]\
 [Structures][8]\
 [Defines][9]\
 [Enumerations][10]\
 Firelight Technologies FMOD Studio API

Studio::Bank
============

A bank contains FMOD Studio Event data as well as the actual sound data
for all events in that bank.

Functions
---------

[Studio::Bank::getEventCount][]\
 [Studio::Bank::getEventList][]\
 [Studio::Bank::getID][]\
 [Studio::Bank::getLoadingState][]\
 [Studio::Bank::getMixerStripCount][]\
 [Studio::Bank::getMixerStripList][]\
 [Studio::Bank::getPath][]\
 [Studio::Bank::getSampleLoadingState][]\
 [Studio::Bank::loadSampleData][]\
 [Studio::Bank::unload][]\
 [Studio::Bank::unloadSampleData][]\
 See Also --------

-   [Studio::System::loadBankFile][]
-   [Studio::System::loadBankMemory][]
-   [Studio::System::loadBankCustom][]

Firelight Technologies FMOD Studio API

Callbacks
=========

[FMOD\_STUDIO\_EVENT\_CALLBACK][]\
 Firelight Technologies FMOD Studio API

Studio::CueInstance
===================

A trigger for an FMOD Studio Event.

Functions
---------

[Studio::CueInstance::trigger][]\
 Remarks -------

Cues can be set into events to pause the timeline at a certain point
until the game activates the cue. Currently there is only a single cue
type supported, with a name "keyOff".

See Also
--------

-   [Studio::EventInstance::getCue][]
-   [Studio::EventInstance::getCueByIndex][]
-   [Studio::EventInstance::getCueCount][]

Firelight Technologies FMOD Studio API

Defines
=======

[FMOD\_STUDIO\_INITFLAGS][]\
 [FMOD\_STUDIO\_LOAD\_BANK\_FLAGS][]\
 [FMOD\_STUDIO\_RECORD\_COMMANDS\_FLAGS][]\
 Firelight Technologies FMOD Studio API

Enumerations
============

[FMOD\_STUDIO\_EVENT\_CALLBACK\_TYPE][]\
 [FMOD\_STUDIO\_LOADING\_MODE][]\
 [FMOD\_STUDIO\_LOADING\_STATE][]\
 [FMOD\_STUDIO\_LOAD\_MEMORY\_MODE][]\
 [FMOD\_STUDIO\_PARAMETER\_TYPE][]\
 [FMOD\_STUDIO\_PLAYBACK\_STATE][]\
 [FMOD\_STUDIO\_STOP\_MODE][]\
 [FMOD\_STUDIO\_USER\_PROPERTY\_TYPE][]\
 Firelight Technologies FMOD Studio API

Studio::EventDescription
========================

The description for a FMOD Studio Event.

Functions
---------

[Studio::EventDescription::createInstance][]\
 [Studio::EventDescription::getID][]\
 [Studio::EventDescription::getInstanceCount][]\
 [Studio::EventDescription::getInstanceList][]\
 [Studio::EventDescription::getLength][]\
 [Studio::EventDescription::getMaximumDistance][]\
 [Studio::EventDescription::getMinimumDistance][]\
 [Studio::EventDescription::getParameter][]\
 [Studio::EventDescription::getParameterByIndex][]\
 [Studio::EventDescription::getParameterCount][]\
 [Studio::EventDescription::getPath][]\
 [Studio::EventDescription::getSampleLoadingState][]\
 [Studio::EventDescription::getUserData][]\
 [Studio::EventDescription::getUserProperty][]\
 [Studio::EventDescription::getUserPropertyByIndex][]\
 [Studio::EventDescription::getUserPropertyCount][]\
 [Studio::EventDescription::is3D][]\
 [Studio::EventDescription::isOneshot][]\
 [Studio::EventDescription::isStream][]\
 [Studio::EventDescription::loadSampleData][]\
 [Studio::EventDescription::releaseAllInstances][]\
 [Studio::EventDescription::setCallback][]\
 [Studio::EventDescription::setUserData][]\
 [Studio::EventDescription::unloadSampleData][]\
 Remarks -------

Event Descriptions belong to banks and can be queried after the relevant
bank has been loaded. Event Descriptions can be found either by looking
up by GUID or by querying all descriptions as part of a bank.

See Also
--------

-   [Studio::System::loadBankFile][]
-   [Studio::System::loadBankMemory][]
-   [Studio::System::loadBankCustom][]
-   [Studio::System::getEvent][]
-   [Studio::Bank::getEventCount][]
-   [Studio::Bank::getEventList][]

Firelight Technologies FMOD Studio API

Studio::EventInstance
=====================

An instance of an FMOD Studio Event.

Functions
---------

[Studio::EventInstance::createSubEvent][]\
 [Studio::EventInstance::get3DAttributes][]\
 [Studio::EventInstance::getChannelGroup][]\
 [Studio::EventInstance::getCue][]\
 [Studio::EventInstance::getCueByIndex][]\
 [Studio::EventInstance::getCueCount][]\
 [Studio::EventInstance::getDescription][]\
 [Studio::EventInstance::getLoadingState][]\
 [Studio::EventInstance::getParameter][]\
 [Studio::EventInstance::getParameterByIndex][]\
 [Studio::EventInstance::getParameterCount][]\
 [Studio::EventInstance::getPaused][]\
 [Studio::EventInstance::getPitch][]\
 [Studio::EventInstance::getPlaybackState][]\
 [Studio::EventInstance::getTimelinePosition][]\
 [Studio::EventInstance::getUserData][]\
 [Studio::EventInstance::getVolume][]\
 [Studio::EventInstance::isVirtual][]\
 [Studio::EventInstance::release][]\
 [Studio::EventInstance::set3DAttributes][]\
 [Studio::EventInstance::setCallback][]\
 [Studio::EventInstance::setParameterValue][]\
 [Studio::EventInstance::setParameterValueByIndex][]\
 [Studio::EventInstance::setPaused][]\
 [Studio::EventInstance::setPitch][]\
 [Studio::EventInstance::setTimelinePosition][]\
 [Studio::EventInstance::setUserData][]\
 [Studio::EventInstance::setVolume][]\
 [Studio::EventInstance::start][]\
 [Studio::EventInstance::stop][]\
 See Also --------

-   [Studio::EventDescription::createInstance][]

Firelight Technologies FMOD Studio API

Functions
=========

[ParseID][]\
 Firelight Technologies FMOD Studio API

C++ interfaces
==============

[System][11]\
 [EventDescription][]\
 [EventInstance][]\
 [CueInstance][]\
 [ParameterInstance][]\
 [MixerStrip][]\
 [Bank][]\
 Firelight Technologies FMOD Studio API

Studio::MixerStrip
==================

Represents either a VCA or a bus.

Functions
---------

[Studio::MixerStrip::getChannelGroup][]\
 [Studio::MixerStrip::getFaderLevel][]\
 [Studio::MixerStrip::getID][]\
 [Studio::MixerStrip::getLoadingState][]\
 [Studio::MixerStrip::getMute][]\
 [Studio::MixerStrip::getPath][]\
 [Studio::MixerStrip::getPaused][]\
 [Studio::MixerStrip::release][]\
 [Studio::MixerStrip::setFaderLevel][]\
 [Studio::MixerStrip::setMute][]\
 [Studio::MixerStrip::setPaused][]\
 [Studio::MixerStrip::stopAllEvents][]\
 See Also --------

-   [Studio::System::getMixerStrip][]

Firelight Technologies FMOD Studio API

Studio::ParameterInstance
=========================

A parameter instance for an FMOD Studio Event.

Functions
---------

[Studio::ParameterInstance::getDescription][]\
 [Studio::ParameterInstance::getValue][]\
 [Studio::ParameterInstance::setValue][]\
 See Also --------

-   [Studio::EventInstance::getParameter][]
-   [Studio::EventInstance::getParameterByIndex][]
-   [Studio::EventInstance::getParameterCount][]

Firelight Technologies FMOD Studio API

Structures
==========

[FMOD\_STUDIO\_ADVANCEDSETTINGS][]\
 [FMOD\_STUDIO\_BANK\_INFO][]\
 [FMOD\_STUDIO\_BUFFER\_INFO][]\
 [FMOD\_STUDIO\_BUFFER\_USAGE][]\
 [FMOD\_STUDIO\_CPU\_USAGE][]\
 [FMOD\_STUDIO\_PARAMETER\_DESCRIPTION][]\
 [FMOD\_STUDIO\_PROGRAMMER\_SOUND\_PROPERTIES][]\
 [FMOD\_STUDIO\_USER\_PROPERTY][]\
 Firelight Technologies FMOD Studio API

Studio::System
==============

The main system object for FMOD Studio.

Functions
---------

[Studio::System::create][]\
 [Studio::System::flushCommands][]\
 [Studio::System::getAdvancedSettings][]\
 [Studio::System::getBank][]\
 [Studio::System::getBankCount][]\
 [Studio::System::getBankList][]\
 [Studio::System::getBufferUsage][]\
 [Studio::System::getCPUUsage][]\
 [Studio::System::getEvent][]\
 [Studio::System::getListenerAttributes][]\
 [Studio::System::getLowLevelSystem][]\
 [Studio::System::getMixerStrip][]\
 [Studio::System::initialize][]\
 [Studio::System::loadBankCustom][]\
 [Studio::System::loadBankFile][]\
 [Studio::System::loadBankMemory][]\
 [Studio::System::lookupID][]\
 [Studio::System::lookupPath][]\
 [Studio::System::playbackCommands][]\
 [Studio::System::registerPlugin][]\
 [Studio::System::release][]\
 [Studio::System::resetBufferUsage][]\
 [Studio::System::setAdvancedSettings][]\
 [Studio::System::setListenerAttributes][]\
 [Studio::System::startRecordCommands][]\
 [Studio::System::stopRecordCommands][]\
 [Studio::System::unloadAll][]\
 [Studio::System::unregisterPlugin][]\
 [Studio::System::update][]\
 Remarks -------

Initializing the FMOD Studio System object will also initialise the low
level System object.

See Also
--------

-   [Studio::System::create][]
-   [Studio::System::initialize][]

  [Functions]: generated/fsbank_api_functions.html
  [Callbacks]: generated/fsbank_api_callbacks.html
  [Structures]: generated/fsbank_api_structures.html
  [Defines]: generated/fsbank_api_defines.html
  [Enumerations]: generated/fsbank_api_enumerations.html
  [FSBANK\_MEMORY\_ALLOC\_CALLBACK]: generated/FSBANK_MEMORY_ALLOC_CALLBACK.html
  [FSBANK\_MEMORY\_FREE\_CALLBACK]: generated/FSBANK_MEMORY_FREE_CALLBACK.html
  [FSBANK\_MEMORY\_REALLOC\_CALLBACK]: generated/FSBANK_MEMORY_REALLOC_CALLBACK.html
  [FSBANK\_BUILDFLAGS]: generated/FSBANK_BUILDFLAGS.html
  [FSBANK\_INITFLAGS]: generated/FSBANK_INITFLAGS.html
  [FSBANK\_FORMAT]: generated/FSBANK_FORMAT.html
  [FSBANK\_FSBVERSION]: generated/FSBANK_FSBVERSION.html
  [FSBANK\_RESULT]: generated/FSBANK_RESULT.html
  [FSBANK\_SPEAKERMAP]: generated/FSBANK_SPEAKERMAP.html
  [FSBANK\_STATE]: generated/FSBANK_STATE.html
  [FSBank\_Build]: generated/FSBank_Build.html
  [FSBank\_BuildCancel]: generated/FSBank_BuildCancel.html
  [FSBank\_FetchNextProgressItem]: generated/FSBank_FetchNextProgressItem.html
  [FSBank\_Init]: generated/FSBank_Init.html
  [FSBank\_MemoryGetStats]: generated/FSBank_MemoryGetStats.html
  [FSBank\_MemoryInit]: generated/FSBank_MemoryInit.html
  [FSBank\_Release]: generated/FSBank_Release.html
  [FSBank\_ReleaseProgressItem]: generated/FSBank_ReleaseProgressItem.html
  [FSBANK\_PROGRESSITEM]: generated/FSBANK_PROGRESSITEM.html
  [FSBANK\_STATEDATA\_FAILED]: generated/FSBANK_STATEDATA_FAILED.html
  [FSBANK\_STATEDATA\_WARNING]: generated/FSBANK_STATEDATA_WARNING.html
  [FSBANK\_SUBSOUND]: generated/FSBANK_SUBSOUND.html
  [FSBANK\_OK]: generated/fsbank_result.html
  [FMOD\_OPENMEMORY\_POINT]: generated/FMOD_MODE.html
  [C++ interfaces]: generated/lowlevel_api_interfaces.html
  [1]: generated/lowlevel_api_functions.html
  [2]: generated/lowlevel_api_callbacks.html
  [3]: generated/lowlevel_api_structures.html
  [4]: generated/lowlevel_api_defines.html
  [5]: generated/lowlevel_api_enumerations.html
  [FMOD\_3D\_ROLLOFF\_CALLBACK]: FMOD_3D_ROLLOFF_CALLBACK.html
  [FMOD\_CHANNELCONTROL\_CALLBACK]: generated/FMOD_CHANNELCONTROL_CALLBACK.html
  [FMOD\_CODEC\_CLOSE\_CALLBACK]: generated/FMOD_CODEC_CLOSE_CALLBACK.html
  [FMOD\_CODEC\_GETLENGTH\_CALLBACK]: generated/FMOD_CODEC_GETLENGTH_CALLBACK.html
  [FMOD\_CODEC\_GETPOSITION\_CALLBACK]: generated/FMOD_CODEC_GETPOSITION_CALLBACK.html
  [FMOD\_CODEC\_METADATA\_CALLBACK]: generated/FMOD_CODEC_METADATA_CALLBACK.html
  [FMOD\_CODEC\_OPEN\_CALLBACK]: generated/FMOD_CODEC_OPEN_CALLBACK.html
  [FMOD\_CODEC\_READ\_CALLBACK]: generated/FMOD_CODEC_READ_CALLBACK.html
  [FMOD\_CODEC\_SETPOSITION\_CALLBACK]: generated/FMOD_CODEC_SETPOSITION_CALLBACK.html
  [FMOD\_CODEC\_SOUNDCREATE\_CALLBACK]: generated/FMOD_CODEC_SOUNDCREATE_CALLBACK.html
  [FMOD\_DSP\_CREATE\_CALLBACK]: generated/FMOD_DSP_CREATE_CALLBACK.html
  [FMOD\_DSP\_DIALOG\_CALLBACK]: generated/FMOD_DSP_DIALOG_CALLBACK.html
  [FMOD\_DSP\_GETPARAM\_BOOL\_CALLBACK]: generated/FMOD_DSP_GETPARAM_BOOL_CALLBACK.html
  [FMOD\_DSP\_GETPARAM\_DATA\_CALLBACK]: generated/FMOD_DSP_GETPARAM_DATA_CALLBACK.html
  [FMOD\_DSP\_GETPARAM\_FLOAT\_CALLBACK]: generated/FMOD_DSP_GETPARAM_FLOAT_CALLBACK.html
  [FMOD\_DSP\_GETPARAM\_INT\_CALLBACK]: generated/FMOD_DSP_GETPARAM_INT_CALLBACK.html
  [FMOD\_DSP\_PROCESS\_CALLBACK]: generated/FMOD_DSP_PROCESS_CALLBACK.html
  [FMOD\_DSP\_READ\_CALLBACK]: generated/FMOD_DSP_READ_CALLBACK.html
  [FMOD\_DSP\_RELEASE\_CALLBACK]: generated/FMOD_DSP_RELEASE_CALLBACK.html
  [FMOD\_DSP\_RESET\_CALLBACK]: generated/FMOD_DSP_RESET_CALLBACK.html
  [FMOD\_DSP\_SETPARAM\_BOOL\_CALLBACK]: generated/FMOD_DSP_SETPARAM_BOOL_CALLBACK.html
  [FMOD\_DSP\_SETPARAM\_DATA\_CALLBACK]: generated/FMOD_DSP_SETPARAM_DATA_CALLBACK.html
  [FMOD\_DSP\_SETPARAM\_FLOAT\_CALLBACK]: generated/FMOD_DSP_SETPARAM_FLOAT_CALLBACK.html
  [FMOD\_DSP\_SETPARAM\_INT\_CALLBACK]: generated/FMOD_DSP_SETPARAM_INT_CALLBACK.html
  [FMOD\_DSP\_SETPOSITION\_CALLBACK]: generated/FMOD_DSP_SETPOSITION_CALLBACK.html
  [FMOD\_DSP\_SHOULDIPROCESS\_CALLBACK]: generated/FMOD_DSP_SHOULDIPROCESS_CALLBACK.html
  [FMOD\_FILE\_ASYNCCANCEL\_CALLBACK]: generated/FMOD_FILE_ASYNCCANCEL_CALLBACK.html
  [FMOD\_FILE\_ASYNCREAD\_CALLBACK]: generated/FMOD_FILE_ASYNCREAD_CALLBACK.html
  [FMOD\_FILE\_CLOSE\_CALLBACK]: generated/FMOD_FILE_CLOSE_CALLBACK.html
  [FMOD\_FILE\_OPEN\_CALLBACK]: generated/FMOD_FILE_OPEN_CALLBACK.html
  [FMOD\_FILE\_READ\_CALLBACK]: generated/FMOD_FILE_READ_CALLBACK.html
  [FMOD\_FILE\_SEEK\_CALLBACK]: generated/FMOD_FILE_SEEK_CALLBACK.html
  [FMOD\_MEMORY\_ALLOC\_CALLBACK]: generated/FMOD_MEMORY_ALLOC_CALLBACK.html
  [FMOD\_MEMORY\_FREE\_CALLBACK]: generated/FMOD_MEMORY_FREE_CALLBACK.html
  [FMOD\_MEMORY\_REALLOC\_CALLBACK]: generated/FMOD_MEMORY_REALLOC_CALLBACK.html
  [FMOD\_OUTPUT\_CLOSE\_CALLBACK]: generated/FMOD_OUTPUT_CLOSE_CALLBACK.html
  [FMOD\_OUTPUT\_GETDRIVERINFO\_CALLBACK]: generated/FMOD_OUTPUT_GETDRIVERINFO_CALLBACK.html
  [FMOD\_OUTPUT\_GETHANDLE\_CALLBACK]: generated/FMOD_OUTPUT_GETHANDLE_CALLBACK.html
  [FMOD\_OUTPUT\_GETNUMDRIVERS\_CALLBACK]: generated/FMOD_OUTPUT_GETNUMDRIVERS_CALLBACK.html
  [FMOD\_OUTPUT\_GETPOSITION\_CALLBACK]: generated/FMOD_OUTPUT_GETPOSITION_CALLBACK.html
  [FMOD\_OUTPUT\_INIT\_CALLBACK]: generated/FMOD_OUTPUT_INIT_CALLBACK.html
  [FMOD\_OUTPUT\_LOCK\_CALLBACK]: generated/FMOD_OUTPUT_LOCK_CALLBACK.html
  [FMOD\_OUTPUT\_READFROMMIXER]: generated/FMOD_OUTPUT_READFROMMIXER.html
  [FMOD\_OUTPUT\_UNLOCK\_CALLBACK]: generated/FMOD_OUTPUT_UNLOCK_CALLBACK.html
  [FMOD\_OUTPUT\_UPDATE\_CALLBACK]: generated/FMOD_OUTPUT_UPDATE_CALLBACK.html
  [FMOD\_SOUND\_NONBLOCK\_CALLBACK]: generated/FMOD_SOUND_NONBLOCK_CALLBACK.html
  [FMOD\_SOUND\_PCMREAD\_CALLBACK]: generated/FMOD_SOUND_PCMREAD_CALLBACK.html
  [FMOD\_SOUND\_PCMSETPOS\_CALLBACK]: generated/FMOD_SOUND_PCMSETPOS_CALLBACK.html
  [FMOD\_SYSTEM\_CALLBACK]: generated/FMOD_SYSTEM_CALLBACK.html
  [Channel::addDSP]: generated/FMOD_Channel_AddDSP.html
  [Channel::addFadePoint]: generated/FMOD_Channel_AddFadePoint.html
  [Channel::get3DAttributes]: FMOD_Channel_Get3DAttributes.html
  [Channel::get3DConeOrientation]: FMOD_Channel_Get3DConeOrientation.html
  [Channel::get3DConeSettings]: FMOD_Channel_Get3DConeSettings.html
  [Channel::get3DCustomRolloff]: FMOD_Channel_Get3DCustomRolloff.html
  [Channel::get3DDistanceFilter]: FMOD_Channel_Get3DDistanceFilter.html
  [Channel::get3DDopplerLevel]: FMOD_Channel_Get3DDopplerLevel.html
  [Channel::get3DLevel]: FMOD_Channel_Get3DLevel.html
  [Channel::get3DMinMaxDistance]: FMOD_Channel_Get3DMinMaxDistance.html
  [Channel::get3DOcclusion]: FMOD_Channel_Get3DOcclusion.html
  [Channel::get3DSpread]: FMOD_Channel_Get3DSpread.html
  [Channel::getAudibility]: generated/FMOD_Channel_GetAudibility.html
  [Channel::getChannelGroup]: generated/FMOD_Channel_GetChannelGroup.html
  [Channel::getCurrentSound]: generated/FMOD_Channel_GetCurrentSound.html
  [Channel::getDSP]: generated/FMOD_Channel_GetDSP.html
  [Channel::getDSPClock]: generated/FMOD_Channel_GetDSPClock.html
  [Channel::getDelay]: generated/FMOD_Channel_GetDelay.html
  [Channel::getFadePoints]: generated/FMOD_Channel_GetFadePoints.html
  [Channel::getFrequency]: generated/FMOD_Channel_GetFrequency.html
  [Channel::getIndex]: generated/FMOD_Channel_GetIndex.html
  [Channel::getLoopCount]: generated/FMOD_Channel_GetLoopCount.html
  [Channel::getLoopPoints]: generated/FMOD_Channel_GetLoopPoints.html
  [Channel::getLowPassGain]: generated/FMOD_Channel_GetLowPassGain.html
  [Channel::getMixMatrix]: generated/FMOD_Channel_GetMixMatrix.html
  [Channel::getMode]: generated/FMOD_Channel_GetMode.html
  [Channel::getMute]: generated/FMOD_Channel_GetMute.html
  [Channel::getNumDSPs]: generated/FMOD_Channel_GetNumDSPs.html
  [Channel::getPaused]: generated/FMOD_Channel_GetPaused.html
  [Channel::getPitch]: generated/FMOD_Channel_GetPitch.html
  [Channel::getPosition]: generated/FMOD_Channel_GetPosition.html
  [Channel::getPriority]: generated/FMOD_Channel_GetPriority.html
  [Channel::getReverbProperties]: generated/FMOD_Channel_GetReverbProperties.html
  [Channel::getSystemObject]: generated/FMOD_Channel_GetSystemObject.html
  [Channel::getUserData]: generated/FMOD_Channel_GetUserData.html
  [Channel::getVolume]: generated/FMOD_Channel_GetVolume.html
  [Channel::getVolumeRamp]: generated/FMOD_Channel_GetVolumeRamp.html
  [Channel::isPlaying]: generated/FMOD_Channel_IsPlaying.html
  [Channel::isVirtual]: generated/FMOD_Channel_IsVirtual.html
  [Channel::removeDSP]: generated/FMOD_Channel_RemoveDSP.html
  [Channel::removeFadePoints]: generated/FMOD_Channel_RemoveFadePoints.html
  [Channel::set3DAttributes]: FMOD_Channel_Set3DAttributes.html
  [Channel::set3DConeOrientation]: FMOD_Channel_Set3DConeOrientation.html
  [Channel::set3DConeSettings]: FMOD_Channel_Set3DConeSettings.html
  [Channel::set3DCustomRolloff]: FMOD_Channel_Set3DCustomRolloff.html
  [Channel::set3DDistanceFilter]: FMOD_Channel_Set3DDistanceFilter.html
  [Channel::set3DDopplerLevel]: FMOD_Channel_Set3DDopplerLevel.html
  [Channel::set3DLevel]: FMOD_Channel_Set3DLevel.html
  [Channel::set3DMinMaxDistance]: FMOD_Channel_Set3DMinMaxDistance.html
  [Channel::set3DOcclusion]: FMOD_Channel_Set3DOcclusion.html
  [Channel::set3DSpread]: FMOD_Channel_Set3DSpread.html
  [Channel::setCallback]: generated/FMOD_Channel_SetCallback.html
  [Channel::setChannelGroup]: generated/FMOD_Channel_SetChannelGroup.html
  [Channel::setDelay]: generated/FMOD_Channel_SetDelay.html
  [Channel::setFrequency]: generated/FMOD_Channel_SetFrequency.html
  [Channel::setLoopCount]: generated/FMOD_Channel_SetLoopCount.html
  [Channel::setLoopPoints]: generated/FMOD_Channel_SetLoopPoints.html
  [Channel::setLowPassGain]: generated/FMOD_Channel_SetLowPassGain.html
  [Channel::setMixLevelsInput]: generated/FMOD_Channel_SetMixLevelsInput.html
  [Channel::setMixLevelsOutput]: generated/FMOD_Channel_SetMixLevelsOutput.html
  [Channel::setMixMatrix]: generated/FMOD_Channel_SetMixMatrix.html
  [Channel::setMode]: generated/FMOD_Channel_SetMode.html
  [Channel::setMute]: generated/FMOD_Channel_SetMute.html
  [Channel::setPan]: generated/FMOD_Channel_SetPan.html
  [Channel::setPaused]: generated/FMOD_Channel_SetPaused.html
  [Channel::setPitch]: generated/FMOD_Channel_SetPitch.html
  [Channel::setPosition]: generated/FMOD_Channel_SetPosition.html
  [Channel::setPriority]: generated/FMOD_Channel_SetPriority.html
  [Channel::setReverbProperties]: generated/FMOD_Channel_SetReverbProperties.html
  [Channel::setUserData]: generated/FMOD_Channel_SetUserData.html
  [Channel::setVolume]: generated/FMOD_Channel_SetVolume.html
  [Channel::setVolumeRamp]: generated/FMOD_Channel_SetVolumeRamp.html
  [Channel::stop]: generated/FMOD_Channel_Stop.html
  [ChannelControl::addDSP]: generated/FMOD_ChannelControl_AddDSP.html
  [ChannelControl::addFadePoint]: generated/FMOD_ChannelControl_AddFadePoint.html
  [ChannelControl::get3DAttributes]: FMOD_ChannelControl_Get3DAttributes.html
  [ChannelControl::get3DConeOrientation]: FMOD_ChannelControl_Get3DConeOrientation.html
  [ChannelControl::get3DConeSettings]: FMOD_ChannelControl_Get3DConeSettings.html
  [ChannelControl::get3DCustomRolloff]: FMOD_ChannelControl_Get3DCustomRolloff.html
  [ChannelControl::get3DDistanceFilter]: FMOD_ChannelControl_Get3DDistanceFilter.html
  [ChannelControl::get3DDopplerLevel]: FMOD_ChannelControl_Get3DDopplerLevel.html
  [ChannelControl::get3DLevel]: FMOD_ChannelControl_Get3DLevel.html
  [ChannelControl::get3DMinMaxDistance]: FMOD_ChannelControl_Get3DMinMaxDistance.html
  [ChannelControl::get3DOcclusion]: FMOD_ChannelControl_Get3DOcclusion.html
  [ChannelControl::get3DSpread]: FMOD_ChannelControl_Get3DSpread.html
  [ChannelControl::getAudibility]: generated/FMOD_ChannelControl_GetAudibility.html
  [ChannelControl::getDSP]: generated/FMOD_ChannelControl_GetDSP.html
  [ChannelControl::getDSPClock]: generated/FMOD_ChannelControl_GetDSPClock.html
  [ChannelControl::getDelay]: generated/FMOD_ChannelControl_GetDelay.html
  [ChannelControl::getFadePoints]: generated/FMOD_ChannelControl_GetFadePoints.html
  [ChannelControl::getLowPassGain]: generated/FMOD_ChannelControl_GetLowPassGain.html
  [ChannelControl::getMixMatrix]: generated/FMOD_ChannelControl_GetMixMatrix.html
  [ChannelControl::getMute]: generated/FMOD_ChannelControl_GetMute.html
  [ChannelControl::getNumDSPs]: generated/FMOD_ChannelControl_GetNumDSPs.html
  [ChannelControl::getPaused]: generated/FMOD_ChannelControl_GetPaused.html
  [ChannelControl::getPitch]: generated/FMOD_ChannelControl_GetPitch.html
  [ChannelControl::getReverbProperties]: generated/FMOD_ChannelControl_GetReverbProperties.html
  [ChannelControl::getSystemObject]: generated/FMOD_ChannelControl_GetSystemObject.html
  [ChannelControl::getUserData]: generated/FMOD_ChannelControl_GetUserData.html
  [ChannelControl::getVolume]: generated/FMOD_ChannelControl_GetVolume.html
  [ChannelControl::getVolumeRamp]: generated/FMOD_ChannelControl_GetVolumeRamp.html
  [ChannelControl::isPlaying]: generated/FMOD_ChannelControl_IsPlaying.html
  [ChannelControl::removeDSP]: generated/FMOD_ChannelControl_RemoveDSP.html
  [ChannelControl::removeFadePoints]: generated/FMOD_ChannelControl_RemoveFadePoints.html
  [ChannelControl::set3DAttributes]: FMOD_ChannelControl_Set3DAttributes.html
  [ChannelControl::set3DConeOrientation]: FMOD_ChannelControl_Set3DConeOrientation.html
  [ChannelControl::set3DConeSettings]: FMOD_ChannelControl_Set3DConeSettings.html
  [ChannelControl::set3DCustomRolloff]: FMOD_ChannelControl_Set3DCustomRolloff.html
  [ChannelControl::set3DDistanceFilter]: FMOD_ChannelControl_Set3DDistanceFilter.html
  [ChannelControl::set3DDopplerLevel]: FMOD_ChannelControl_Set3DDopplerLevel.html
  [ChannelControl::set3DLevel]: FMOD_ChannelControl_Set3DLevel.html
  [ChannelControl::set3DMinMaxDistance]: FMOD_ChannelControl_Set3DMinMaxDistance.html
  [ChannelControl::set3DOcclusion]: FMOD_ChannelControl_Set3DOcclusion.html
  [ChannelControl::set3DSpread]: FMOD_ChannelControl_Set3DSpread.html
  [ChannelControl::setCallback]: generated/FMOD_ChannelControl_SetCallback.html
  [ChannelControl::setDelay]: generated/FMOD_ChannelControl_SetDelay.html
  [ChannelControl::setLowPassGain]: generated/FMOD_ChannelControl_SetLowPassGain.html
  [ChannelControl::setMixLevelsInput]: generated/FMOD_ChannelControl_SetMixLevelsInput.html
  [ChannelControl::setMixLevelsOutput]: generated/FMOD_ChannelControl_SetMixLevelsOutput.html
  [ChannelControl::setMixMatrix]: generated/FMOD_ChannelControl_SetMixMatrix.html
  [ChannelControl::setMute]: generated/FMOD_ChannelControl_SetMute.html
  [ChannelControl::setPan]: generated/FMOD_ChannelControl_SetPan.html
  [ChannelControl::setPaused]: generated/FMOD_ChannelControl_SetPaused.html
  [ChannelControl::setPitch]: generated/FMOD_ChannelControl_SetPitch.html
  [ChannelControl::setReverbProperties]: generated/FMOD_ChannelControl_SetReverbProperties.html
  [ChannelControl::setUserData]: generated/FMOD_ChannelControl_SetUserData.html
  [ChannelControl::setVolume]: generated/FMOD_ChannelControl_SetVolume.html
  [ChannelControl::setVolumeRamp]: generated/FMOD_ChannelControl_SetVolumeRamp.html
  [ChannelControl::stop]: generated/FMOD_ChannelControl_Stop.html
  [ChannelGroup::addDSP]: generated/FMOD_ChannelGroup_AddDSP.html
  [ChannelGroup::addFadePoint]: generated/FMOD_ChannelGroup_AddFadePoint.html
  [ChannelGroup::addGroup]: generated/FMOD_ChannelGroup_AddGroup.html
  [ChannelGroup::get3DAttributes]: FMOD_ChannelGroup_Get3DAttributes.html
  [ChannelGroup::get3DConeOrientation]: FMOD_ChannelGroup_Get3DConeOrientation.html
  [ChannelGroup::get3DConeSettings]: FMOD_ChannelGroup_Get3DConeSettings.html
  [ChannelGroup::get3DCustomRolloff]: FMOD_ChannelGroup_Get3DCustomRolloff.html
  [ChannelGroup::get3DDistanceFilter]: FMOD_ChannelGroup_Get3DDistanceFilter.html
  [ChannelGroup::get3DDopplerLevel]: FMOD_ChannelGroup_Get3DDopplerLevel.html
  [ChannelGroup::get3DLevel]: FMOD_ChannelGroup_Get3DLevel.html
  [ChannelGroup::get3DMinMaxDistance]: FMOD_ChannelGroup_Get3DMinMaxDistance.html
  [ChannelGroup::get3DOcclusion]: FMOD_ChannelGroup_Get3DOcclusion.html
  [ChannelGroup::get3DSpread]: FMOD_ChannelGroup_Get3DSpread.html
  [ChannelGroup::getAudibility]: generated/FMOD_ChannelGroup_GetAudibility.html
  [ChannelGroup::getChannel]: generated/FMOD_ChannelGroup_GetChannel.html
  [ChannelGroup::getDSP]: generated/FMOD_ChannelGroup_GetDSP.html
  [ChannelGroup::getDSPClock]: generated/FMOD_ChannelGroup_GetDSPClock.html
  [ChannelGroup::getDSPIndex]: generated/FMOD_ChannelGroup_GetDSPIndex.html
  [ChannelGroup::getDelay]: generated/FMOD_ChannelGroup_GetDelay.html
  [ChannelGroup::getFadePoints]: generated/FMOD_ChannelGroup_GetFadePoints.html
  [ChannelGroup::getGroup]: generated/FMOD_ChannelGroup_GetGroup.html
  [ChannelGroup::getLowPassGain]: generated/FMOD_ChannelGroup_GetLowPassGain.html
  [ChannelGroup::getMixMatrix]: generated/FMOD_ChannelGroup_GetMixMatrix.html
  [ChannelGroup::getMute]: generated/FMOD_ChannelGroup_GetMute.html
  [ChannelGroup::getName]: generated/FMOD_ChannelGroup_GetName.html
  [ChannelGroup::getNumChannels]: generated/FMOD_ChannelGroup_GetNumChannels.html
  [ChannelGroup::getNumDSPs]: generated/FMOD_ChannelGroup_GetNumDSPs.html
  [ChannelGroup::getNumGroups]: generated/FMOD_ChannelGroup_GetNumGroups.html
  [ChannelGroup::getParentGroup]: generated/FMOD_ChannelGroup_GetParentGroup.html
  [ChannelGroup::getPaused]: generated/FMOD_ChannelGroup_GetPaused.html
  [ChannelGroup::getPitch]: generated/FMOD_ChannelGroup_GetPitch.html
  [ChannelGroup::getReverbProperties]: generated/FMOD_ChannelGroup_GetReverbProperties.html
  [ChannelGroup::getSystemObject]: generated/FMOD_ChannelGroup_GetSystemObject.html
  [ChannelGroup::getUserData]: generated/FMOD_ChannelGroup_GetUserData.html
  [ChannelGroup::getVolume]: generated/FMOD_ChannelGroup_GetVolume.html
  [ChannelGroup::getVolumeRamp]: generated/FMOD_ChannelGroup_GetVolumeRamp.html
  [ChannelGroup::isPlaying]: generated/FMOD_ChannelGroup_IsPlaying.html
  [ChannelGroup::release]: generated/FMOD_ChannelGroup_Release.html
  [ChannelGroup::removeDSP]: generated/FMOD_ChannelGroup_RemoveDSP.html
  [ChannelGroup::removeFadePoints]: generated/FMOD_ChannelGroup_RemoveFadePoints.html
  [ChannelGroup::set3DAttributes]: FMOD_ChannelGroup_Set3DAttributes.html
  [ChannelGroup::set3DConeOrientation]: FMOD_ChannelGroup_Set3DConeOrientation.html
  [ChannelGroup::set3DConeSettings]: FMOD_ChannelGroup_Set3DConeSettings.html
  [ChannelGroup::set3DCustomRolloff]: FMOD_ChannelGroup_Set3DCustomRolloff.html
  [ChannelGroup::set3DDistanceFilter]: FMOD_ChannelGroup_Set3DDistanceFilter.html
  [ChannelGroup::set3DDopplerLevel]: FMOD_ChannelGroup_Set3DDopplerLevel.html
  [ChannelGroup::set3DLevel]: FMOD_ChannelGroup_Set3DLevel.html
  [ChannelGroup::set3DMinMaxDistance]: FMOD_ChannelGroup_Set3DMinMaxDistance.html
  [ChannelGroup::set3DOcclusion]: FMOD_ChannelGroup_Set3DOcclusion.html
  [ChannelGroup::set3DSpread]: FMOD_ChannelGroup_Set3DSpread.html
  [ChannelGroup::setCallback]: generated/FMOD_ChannelGroup_SetCallback.html
  [ChannelGroup::setDSPIndex]: generated/FMOD_ChannelGroup_SetDSPIndex.html
  [ChannelGroup::setDelay]: generated/FMOD_ChannelGroup_SetDelay.html
  [ChannelGroup::setLowPassGain]: generated/FMOD_ChannelGroup_SetLowPassGain.html
  [ChannelGroup::setMixLevelsInput]: generated/FMOD_ChannelGroup_SetMixLevelsInput.html
  [ChannelGroup::setMixLevelsOutput]: generated/FMOD_ChannelGroup_SetMixLevelsOutput.html
  [ChannelGroup::setMixMatrix]: generated/FMOD_ChannelGroup_SetMixMatrix.html
  [ChannelGroup::setMute]: generated/FMOD_ChannelGroup_SetMute.html
  [ChannelGroup::setPan]: generated/FMOD_ChannelGroup_SetPan.html
  [ChannelGroup::setPaused]: generated/FMOD_ChannelGroup_SetPaused.html
  [ChannelGroup::setPitch]: generated/FMOD_ChannelGroup_SetPitch.html
  [ChannelGroup::setReverbProperties]: generated/FMOD_ChannelGroup_SetReverbProperties.html
  [ChannelGroup::setUserData]: generated/FMOD_ChannelGroup_SetUserData.html
  [ChannelGroup::setVolume]: generated/FMOD_ChannelGroup_SetVolume.html
  [ChannelGroup::setVolumeRamp]: generated/FMOD_ChannelGroup_SetVolumeRamp.html
  [ChannelGroup::stop]: generated/FMOD_ChannelGroup_Stop.html
  [FMOD\_CHANNELMASK]: generated/FMOD_CHANNELMASK.html
  [FMOD\_CODEC\_WAVEFORMAT\_VERSION]: generated/FMOD_CODEC_WAVEFORMAT_VERSION.html
  [FMOD\_DEBUGLEVEL]: generated/FMOD_DEBUGLEVEL.html
  [FMOD\_INITFLAGS]: generated/FMOD_INITFLAGS.html
  [FMOD\_MEMORY\_TYPE]: generated/FMOD_MEMORY_TYPE.html
  [FMOD\_PORT\_INDEX]: generated/FMOD_PORT_INDEX.html
  [FMOD\_REVERB\_PRESETS]: generated/FMOD_REVERB_PRESETS.html
  [FMOD\_SYSTEM\_CALLBACK\_TYPE]: generated/FMOD_SYSTEM_CALLBACK_TYPE.html
  [FMOD\_TIMEUNIT]: generated/FMOD_TIMEUNIT.html
  [DSP::addInput]: generated/FMOD_DSP_AddInput.html
  [DSP::disconnectAll]: generated/FMOD_DSP_DisconnectAll.html
  [DSP::disconnectFrom]: generated/FMOD_DSP_DisconnectFrom.html
  [DSP::getActive]: generated/FMOD_DSP_GetActive.html
  [DSP::getBypass]: generated/FMOD_DSP_GetBypass.html
  [DSP::getChannelFormat]: generated/FMOD_DSP_GetChannelFormat.html
  [DSP::getDataParameterIndex]: generated/FMOD_DSP_GetDataParameterIndex.html
  [DSP::getIdle]: generated/FMOD_DSP_GetIdle.html
  [DSP::getInfo]: generated/FMOD_DSP_GetInfo.html
  [DSP::getInput]: generated/FMOD_DSP_GetInput.html
  [DSP::getMeteringEnabled]: generated/FMOD_DSP_GetMeteringEnabled.html
  [DSP::getMeteringInfo]: generated/FMOD_DSP_GetMeteringInfo.html
  [DSP::getNumInputs]: generated/FMOD_DSP_GetNumInputs.html
  [DSP::getNumOutputs]: generated/FMOD_DSP_GetNumOutputs.html
  [DSP::getNumParameters]: generated/FMOD_DSP_GetNumParameters.html
  [DSP::getOutput]: generated/FMOD_DSP_GetOutput.html
  [DSP::getOutputChannelFormat]: generated/FMOD_DSP_GetOutputChannelFormat.html
  [DSP::getParameterBool]: generated/FMOD_DSP_GetParameterBool.html
  [DSP::getParameterData]: generated/FMOD_DSP_GetParameterData.html
  [DSP::getParameterFloat]: generated/FMOD_DSP_GetParameterFloat.html
  [DSP::getParameterInfo]: generated/FMOD_DSP_GetParameterInfo.html
  [DSP::getParameterInt]: generated/FMOD_DSP_GetParameterInt.html
  [DSP::getSystemObject]: generated/FMOD_DSP_GetSystemObject.html
  [DSP::getType]: generated/FMOD_DSP_GetType.html
  [DSP::getUserData]: generated/FMOD_DSP_GetUserData.html
  [DSP::release]: generated/FMOD_DSP_Release.html
  [DSP::reset]: generated/FMOD_DSP_Reset.html
  [DSP::setActive]: generated/FMOD_DSP_SetActive.html
  [DSP::setBypass]: generated/FMOD_DSP_SetBypass.html
  [DSP::setChannelFormat]: generated/FMOD_DSP_SetChannelFormat.html
  [DSP::setMeteringEnabled]: generated/FMOD_DSP_SetMeteringEnabled.html
  [DSP::setParameterBool]: generated/FMOD_DSP_SetParameterBool.html
  [DSP::setParameterData]: generated/FMOD_DSP_SetParameterData.html
  [DSP::setParameterFloat]: generated/FMOD_DSP_SetParameterFloat.html
  [DSP::setParameterInt]: generated/FMOD_DSP_SetParameterInt.html
  [DSP::setUserData]: generated/FMOD_DSP_SetUserData.html
  [DSP::showConfigDialog]: generated/FMOD_DSP_ShowConfigDialog.html
  [DSPConnection::getInput]: generated/FMOD_DSPConnection_GetInput.html
  [DSPConnection::getMix]: generated/FMOD_DSPConnection_GetMix.html
  [DSPConnection::getMixMatrix]: generated/FMOD_DSPConnection_GetMixMatrix.html
  [DSPConnection::getOutput]: generated/FMOD_DSPConnection_GetOutput.html
  [DSPConnection::getType]: generated/FMOD_DSPConnection_GetType.html
  [DSPConnection::getUserData]: generated/FMOD_DSPConnection_GetUserData.html
  [DSPConnection::setMix]: generated/FMOD_DSPConnection_SetMix.html
  [DSPConnection::setMixMatrix]: generated/FMOD_DSPConnection_SetMixMatrix.html
  [DSPConnection::setUserData]: generated/FMOD_DSPConnection_SetUserData.html
  [FMOD\_CHANNELCONTROL\_CALLBACK\_TYPE]: generated/FMOD_CHANNELCONTROL_CALLBACK_TYPE.html
  [FMOD\_CHANNELCONTROL\_DSP\_INDEX]: generated/FMOD_CHANNELCONTROL_DSP_INDEX.html
  [FMOD\_CHANNELCONTROL\_TYPE]: generated/FMOD_CHANNELCONTROL_TYPE.html
  [FMOD\_CHANNELORDER]: generated/FMOD_CHANNELORDER.html
  [FMOD\_DSPCONNECTION\_TYPE]: generated/FMOD_DSPCONNECTION_TYPE.html
  [FMOD\_DSP\_CHORUS]: generated/FMOD_DSP_CHORUS.html
  [FMOD\_DSP\_COMPRESSOR]: generated/FMOD_DSP_COMPRESSOR.html
  [FMOD\_DSP\_DELAY]: generated/FMOD_DSP_DELAY.html
  [FMOD\_DSP\_DISTORTION]: generated/FMOD_DSP_DISTORTION.html
  [FMOD\_DSP\_ECHO]: generated/FMOD_DSP_ECHO.html
  [FMOD\_DSP\_ENVELOPEFOLLOWER]: generated/FMOD_DSP_ENVELOPEFOLLOWER.html
  [FMOD\_DSP\_FFT]: generated/FMOD_DSP_FFT.html
  [FMOD\_DSP\_FFT\_WINDOW]: generated/FMOD_DSP_FFT_WINDOW.html
  [FMOD\_DSP\_FLANGE]: generated/FMOD_DSP_FLANGE.html
  [FMOD\_DSP\_HIGHPASS]: generated/FMOD_DSP_HIGHPASS.html
  [FMOD\_DSP\_HIGHPASS\_SIMPLE]: generated/FMOD_DSP_HIGHPASS_SIMPLE.html
  [FMOD\_DSP\_ITECHO]: generated/FMOD_DSP_ITECHO.html
  [FMOD\_DSP\_ITLOWPASS]: generated/FMOD_DSP_ITLOWPASS.html
  [FMOD\_DSP\_LIMITER]: generated/FMOD_DSP_LIMITER.html
  [FMOD\_DSP\_LOWPASS]: generated/FMOD_DSP_LOWPASS.html
  [FMOD\_DSP\_LOWPASS\_SIMPLE]: generated/FMOD_DSP_LOWPASS_SIMPLE.html
  [FMOD\_DSP\_NORMALIZE]: generated/FMOD_DSP_NORMALIZE.html
  [FMOD\_DSP\_OSCILLATOR]: generated/FMOD_DSP_OSCILLATOR.html
  [FMOD\_DSP\_PAN]: generated/FMOD_DSP_PAN.html
  [FMOD\_DSP\_PAN\_3D\_EXTENT\_MODE\_TYPE]: FMOD_DSP_PAN_3D_EXTENT_MODE_TYPE.html
  [FMOD\_DSP\_PAN\_3D\_ROLLOFF\_TYPE]: FMOD_DSP_PAN_3D_ROLLOFF_TYPE.html
  [FMOD\_DSP\_PAN\_SURROUND\_FROM\_STEREO\_MODE\_TYPE]: generated/FMOD_DSP_PAN_SURROUND_FROM_STEREO_MODE_TYPE.html
  [FMOD\_DSP\_PARAMEQ]: generated/FMOD_DSP_PARAMEQ.html
  [FMOD\_DSP\_PARAMETER\_DATA\_TYPE]: generated/FMOD_DSP_PARAMETER_DATA_TYPE.html
  [FMOD\_DSP\_PARAMETER\_FLOAT\_MAPPING\_TYPE]: generated/FMOD_DSP_PARAMETER_FLOAT_MAPPING_TYPE.html
  [FMOD\_DSP\_PARAMETER\_TYPE]: generated/FMOD_DSP_PARAMETER_TYPE.html
  [FMOD\_DSP\_PITCHSHIFT]: generated/FMOD_DSP_PITCHSHIFT.html
  [FMOD\_DSP\_PROCESS\_OPERATION]: generated/FMOD_DSP_PROCESS_OPERATION.html
  [FMOD\_DSP\_RESAMPLER]: generated/FMOD_DSP_RESAMPLER.html
  [FMOD\_DSP\_RETURN]: generated/FMOD_DSP_RETURN.html
  [FMOD\_DSP\_SEND]: generated/FMOD_DSP_SEND.html
  [FMOD\_DSP\_SFXREVERB]: generated/FMOD_DSP_SFXREVERB.html
  [FMOD\_DSP\_THREE\_EQ]: generated/FMOD_DSP_THREE_EQ.html
  [FMOD\_DSP\_THREE\_EQ\_CROSSOVERSLOPE\_TYPE]: generated/FMOD_DSP_THREE_EQ_CROSSOVERSLOPE_TYPE.html
  [FMOD\_DSP\_TREMOLO]: generated/FMOD_DSP_TREMOLO.html
  [FMOD\_DSP\_TYPE]: generated/FMOD_DSP_TYPE.html
  [FMOD\_ERRORCALLBACK\_INSTANCETYPE]: generated/FMOD_ERRORCALLBACK_INSTANCETYPE.html
  [FMOD\_OPENSTATE]: generated/FMOD_OPENSTATE.html
  [FMOD\_OUTPUTTYPE]: generated/FMOD_OUTPUTTYPE.html
  [FMOD\_PLUGINTYPE]: generated/FMOD_PLUGINTYPE.html
  [FMOD\_RESULT]: generated/FMOD_RESULT.html
  [FMOD\_SOUNDGROUP\_BEHAVIOR]: generated/FMOD_SOUNDGROUP_BEHAVIOR.html
  [FMOD\_SOUND\_FORMAT]: generated/FMOD_SOUND_FORMAT.html
  [FMOD\_SOUND\_TYPE]: generated/FMOD_SOUND_TYPE.html
  [FMOD\_SPEAKER]: generated/FMOD_SPEAKER.html
  [FMOD\_SPEAKERMODE]: generated/FMOD_SPEAKERMODE.html
  [FMOD\_TAGDATATYPE]: generated/FMOD_TAGDATATYPE.html
  [FMOD\_TAGTYPE]: generated/FMOD_TAGTYPE.html
  [Debug\_GetLevel]: generated/FMOD_Debug_GetLevel.html
  [Debug\_SetLevel]: generated/FMOD_Debug_SetLevel.html
  [File\_GetDiskBusy]: generated/FMOD_File_GetDiskBusy.html
  [File\_SetDiskBusy]: generated/FMOD_File_SetDiskBusy.html
  [Memory\_GetStats]: generated/FMOD_Memory_GetStats.html
  [Memory\_Initialize]: generated/FMOD_Memory_Initialize.html
  [System\_Create]: generated/FMOD_System_Create.html
  [Geometry::addPolygon]: generated/FMOD_Geometry_AddPolygon.html
  [Geometry::getActive]: generated/FMOD_Geometry_GetActive.html
  [Geometry::getMaxPolygons]: generated/FMOD_Geometry_GetMaxPolygons.html
  [Geometry::getNumPolygons]: generated/FMOD_Geometry_GetNumPolygons.html
  [Geometry::getPolygonAttributes]: generated/FMOD_Geometry_GetPolygonAttributes.html
  [Geometry::getPolygonNumVertices]: generated/FMOD_Geometry_GetPolygonNumVertices.html
  [Geometry::getPolygonVertex]: generated/FMOD_Geometry_GetPolygonVertex.html
  [Geometry::getPosition]: generated/FMOD_Geometry_GetPosition.html
  [Geometry::getRotation]: generated/FMOD_Geometry_GetRotation.html
  [Geometry::getScale]: generated/FMOD_Geometry_GetScale.html
  [Geometry::getUserData]: generated/FMOD_Geometry_GetUserData.html
  [Geometry::release]: generated/FMOD_Geometry_Release.html
  [Geometry::save]: generated/FMOD_Geometry_Save.html
  [Geometry::setActive]: generated/FMOD_Geometry_SetActive.html
  [Geometry::setPolygonAttributes]: generated/FMOD_Geometry_SetPolygonAttributes.html
  [Geometry::setPolygonVertex]: generated/FMOD_Geometry_SetPolygonVertex.html
  [Geometry::setPosition]: generated/FMOD_Geometry_SetPosition.html
  [Geometry::setRotation]: generated/FMOD_Geometry_SetRotation.html
  [Geometry::setScale]: generated/FMOD_Geometry_SetScale.html
  [Geometry::setUserData]: generated/FMOD_Geometry_SetUserData.html
  [System]: generated/lowlevel_api_System.html
  [Sound]: generated/lowlevel_api_Sound.html
  [ChannelControl]: generated/lowlevel_api_ChannelControl.html
  [Channel]: generated/lowlevel_api_Channel.html
  [ChannelGroup]: generated/lowlevel_api_ChannelGroup.html
  [SoundGroup]: generated/lowlevel_api_SoundGroup.html
  [DSP]: generated/lowlevel_api_DSP.html
  [DSPConnection]: generated/lowlevel_api_DSPConnection.html
  [Geometry]: generated/lowlevel_api_Geometry.html
  [Reverb3D]: lowlevel_api_Reverb3D.html
  [Reverb3D::get3DAttributes]: FMOD_Reverb3D_Get3DAttributes.html
  [Reverb3D::getActive]: FMOD_Reverb3D_GetActive.html
  [Reverb3D::getProperties]: FMOD_Reverb3D_GetProperties.html
  [Reverb3D::getUserData]: FMOD_Reverb3D_GetUserData.html
  [Reverb3D::release]: FMOD_Reverb3D_Release.html
  [Reverb3D::set3DAttributes]: FMOD_Reverb3D_Set3DAttributes.html
  [Reverb3D::setActive]: FMOD_Reverb3D_SetActive.html
  [Reverb3D::setProperties]: FMOD_Reverb3D_SetProperties.html
  [Reverb3D::setUserData]: FMOD_Reverb3D_SetUserData.html
  [Sound::addSyncPoint]: generated/FMOD_Sound_AddSyncPoint.html
  [Sound::deleteSyncPoint]: generated/FMOD_Sound_DeleteSyncPoint.html
  [Sound::get3DConeSettings]: FMOD_Sound_Get3DConeSettings.html
  [Sound::get3DCustomRolloff]: FMOD_Sound_Get3DCustomRolloff.html
  [Sound::get3DMinMaxDistance]: FMOD_Sound_Get3DMinMaxDistance.html
  [Sound::getDefaults]: generated/FMOD_Sound_GetDefaults.html
  [Sound::getFormat]: generated/FMOD_Sound_GetFormat.html
  [Sound::getLength]: generated/FMOD_Sound_GetLength.html
  [Sound::getLoopCount]: generated/FMOD_Sound_GetLoopCount.html
  [Sound::getLoopPoints]: generated/FMOD_Sound_GetLoopPoints.html
  [Sound::getMode]: generated/FMOD_Sound_GetMode.html
  [Sound::getMusicChannelVolume]: generated/FMOD_Sound_GetMusicChannelVolume.html
  [Sound::getMusicNumChannels]: generated/FMOD_Sound_GetMusicNumChannels.html
  [Sound::getMusicSpeed]: generated/FMOD_Sound_GetMusicSpeed.html
  [Sound::getName]: generated/FMOD_Sound_GetName.html
  [Sound::getNumSubSounds]: generated/FMOD_Sound_GetNumSubSounds.html
  [Sound::getNumSyncPoints]: generated/FMOD_Sound_GetNumSyncPoints.html
  [Sound::getNumTags]: generated/FMOD_Sound_GetNumTags.html
  [Sound::getOpenState]: generated/FMOD_Sound_GetOpenState.html
  [Sound::getSoundGroup]: generated/FMOD_Sound_GetSoundGroup.html
  [Sound::getSubSound]: generated/FMOD_Sound_GetSubSound.html
  [Sound::getSubSoundParent]: generated/FMOD_Sound_GetSubSoundParent.html
  [Sound::getSyncPoint]: generated/FMOD_Sound_GetSyncPoint.html
  [Sound::getSyncPointInfo]: generated/FMOD_Sound_GetSyncPointInfo.html
  [Sound::getSystemObject]: generated/FMOD_Sound_GetSystemObject.html
  [Sound::getTag]: generated/FMOD_Sound_GetTag.html
  [Sound::getUserData]: generated/FMOD_Sound_GetUserData.html
  [Sound::lock]: generated/FMOD_Sound_Lock.html
  [Sound::readData]: generated/FMOD_Sound_ReadData.html
  [Sound::release]: generated/FMOD_Sound_Release.html
  [Sound::seekData]: generated/FMOD_Sound_SeekData.html
  [Sound::set3DConeSettings]: FMOD_Sound_Set3DConeSettings.html
  [Sound::set3DCustomRolloff]: FMOD_Sound_Set3DCustomRolloff.html
  [Sound::set3DMinMaxDistance]: FMOD_Sound_Set3DMinMaxDistance.html
  [Sound::setDefaults]: generated/FMOD_Sound_SetDefaults.html
  [Sound::setLoopCount]: generated/FMOD_Sound_SetLoopCount.html
  [Sound::setLoopPoints]: generated/FMOD_Sound_SetLoopPoints.html
  [Sound::setMode]: generated/FMOD_Sound_SetMode.html
  [Sound::setMusicChannelVolume]: generated/FMOD_Sound_SetMusicChannelVolume.html
  [Sound::setMusicSpeed]: generated/FMOD_Sound_SetMusicSpeed.html
  [Sound::setSoundGroup]: generated/FMOD_Sound_SetSoundGroup.html
  [Sound::setSubSound]: generated/FMOD_Sound_SetSubSound.html
  [Sound::setUserData]: generated/FMOD_Sound_SetUserData.html
  [Sound::unlock]: generated/FMOD_Sound_Unlock.html
  [SoundGroup::getMaxAudible]: generated/FMOD_SoundGroup_GetMaxAudible.html
  [SoundGroup::getMaxAudibleBehavior]: generated/FMOD_SoundGroup_GetMaxAudibleBehavior.html
  [SoundGroup::getMuteFadeSpeed]: generated/FMOD_SoundGroup_GetMuteFadeSpeed.html
  [SoundGroup::getName]: generated/FMOD_SoundGroup_GetName.html
  [SoundGroup::getNumPlaying]: generated/FMOD_SoundGroup_GetNumPlaying.html
  [SoundGroup::getNumSounds]: generated/FMOD_SoundGroup_GetNumSounds.html
  [SoundGroup::getSound]: generated/FMOD_SoundGroup_GetSound.html
  [SoundGroup::getSystemObject]: generated/FMOD_SoundGroup_GetSystemObject.html
  [SoundGroup::getUserData]: generated/FMOD_SoundGroup_GetUserData.html
  [SoundGroup::getVolume]: generated/FMOD_SoundGroup_GetVolume.html
  [SoundGroup::release]: generated/FMOD_SoundGroup_Release.html
  [SoundGroup::setMaxAudible]: generated/FMOD_SoundGroup_SetMaxAudible.html
  [SoundGroup::setMaxAudibleBehavior]: generated/FMOD_SoundGroup_SetMaxAudibleBehavior.html
  [SoundGroup::setMuteFadeSpeed]: generated/FMOD_SoundGroup_SetMuteFadeSpeed.html
  [SoundGroup::setUserData]: generated/FMOD_SoundGroup_SetUserData.html
  [SoundGroup::setVolume]: generated/FMOD_SoundGroup_SetVolume.html
  [SoundGroup::stop]: generated/FMOD_SoundGroup_Stop.html
  [FMOD\_3D\_ATTRIBUTES]: FMOD_3D_ATTRIBUTES.html
  [FMOD\_ADVANCEDSETTINGS]: generated/FMOD_ADVANCEDSETTINGS.html
  [FMOD\_ASYNCREADINFO]: generated/FMOD_ASYNCREADINFO.html
  [FMOD\_CODEC\_DESCRIPTION]: generated/FMOD_CODEC_DESCRIPTION.html
  [FMOD\_CODEC\_STATE]: generated/FMOD_CODEC_STATE.html
  [FMOD\_CODEC\_WAVEFORMAT]: generated/FMOD_CODEC_WAVEFORMAT.html
  [FMOD\_CREATESOUNDEXINFO]: generated/FMOD_CREATESOUNDEXINFO.html
  [FMOD\_DSP\_BUFFER\_ARRAY]: generated/FMOD_DSP_BUFFER_ARRAY.html
  [FMOD\_DSP\_DESCRIPTION]: generated/FMOD_DSP_DESCRIPTION.html
  [FMOD\_DSP\_METERING\_INFO]: generated/FMOD_DSP_METERING_INFO.html
  [FMOD\_DSP\_PARAMETER\_3DATTRIBUTES]: FMOD_DSP_PARAMETER_3DATTRIBUTES.html
  [FMOD\_DSP\_PARAMETER\_DESC]: generated/FMOD_DSP_PARAMETER_DESC.html
  [FMOD\_DSP\_PARAMETER\_DESC\_BOOL]: generated/FMOD_DSP_PARAMETER_DESC_BOOL.html
  [FMOD\_DSP\_PARAMETER\_DESC\_DATA]: generated/FMOD_DSP_PARAMETER_DESC_DATA.html
  [FMOD\_DSP\_PARAMETER\_DESC\_FLOAT]: generated/FMOD_DSP_PARAMETER_DESC_FLOAT.html
  [FMOD\_DSP\_PARAMETER\_DESC\_INT]: generated/FMOD_DSP_PARAMETER_DESC_INT.html
  [FMOD\_DSP\_PARAMETER\_OVERALLGAIN]: generated/FMOD_DSP_PARAMETER_OVERALLGAIN.html
  [FMOD\_DSP\_PARAMETER\_SIDECHAIN]: generated/FMOD_DSP_PARAMETER_SIDECHAIN.html
  [FMOD\_DSP\_STATE]: generated/FMOD_DSP_STATE.html
  [FMOD\_DSP\_STATE\_SYSTEMCALLBACKS]: generated/FMOD_DSP_STATE_SYSTEMCALLBACKS.html
  [FMOD\_ERRORCALLBACK\_INFO]: generated/FMOD_ERRORCALLBACK_INFO.html
  [FMOD\_GUID]: generated/FMOD_GUID.html
  [FMOD\_OUTPUT\_DESCRIPTION]: generated/FMOD_OUTPUT_DESCRIPTION.html
  [FMOD\_OUTPUT\_STATE]: generated/FMOD_OUTPUT_STATE.html
  [FMOD\_REVERB\_PROPERTIES]: generated/FMOD_REVERB_PROPERTIES.html
  [FMOD\_TAG]: generated/FMOD_TAG.html
  [FMOD\_VECTOR]: generated/FMOD_VECTOR.html
  [piecewiselinearmapping]: generated/piecewiselinearmapping.html
  [System::attachChannelGroupToPort]: generated/FMOD_System_AttachChannelGroupToPort.html
  [System::attachFileSystem]: generated/FMOD_System_AttachFileSystem.html
  [System::close]: generated/FMOD_System_Close.html
  [System::createChannelGroup]: generated/FMOD_System_CreateChannelGroup.html
  [System::createDSP]: generated/FMOD_System_CreateDSP.html
  [System::createDSPByPlugin]: generated/FMOD_System_CreateDSPByPlugin.html
  [System::createDSPByType]: generated/FMOD_System_CreateDSPByType.html
  [System::createGeometry]: generated/FMOD_System_CreateGeometry.html
  [System::createReverb3D]: FMOD_System_CreateReverb3D.html
  [System::createSound]: generated/FMOD_System_CreateSound.html
  [System::createSoundGroup]: generated/FMOD_System_CreateSoundGroup.html
  [System::createStream]: generated/FMOD_System_CreateStream.html
  [System::detachChannelGroupFromPort]: generated/FMOD_System_DetachChannelGroupFromPort.html
  [System::get3DListenerAttributes]: FMOD_System_Get3DListenerAttributes.html
  [System::get3DNumListeners]: FMOD_System_Get3DNumListeners.html
  [System::get3DSettings]: FMOD_System_Get3DSettings.html
  [System::getAdvancedSettings]: generated/FMOD_System_GetAdvancedSettings.html
  [System::getCPUUsage]: generated/FMOD_System_GetCPUUsage.html
  [System::getChannel]: generated/FMOD_System_GetChannel.html
  [System::getChannelsPlaying]: generated/FMOD_System_GetChannelsPlaying.html
  [System::getDSPBufferSize]: generated/FMOD_System_GetDSPBufferSize.html
  [System::getDSPInfoByPlugin]: generated/FMOD_System_GetDSPInfoByPlugin.html
  [System::getDriver]: generated/FMOD_System_GetDriver.html
  [System::getDriverInfo]: generated/FMOD_System_GetDriverInfo.html
  [System::getGeometryOcclusion]: generated/FMOD_System_GetGeometryOcclusion.html
  [System::getGeometrySettings]: generated/FMOD_System_GetGeometrySettings.html
  [System::getMasterChannelGroup]: generated/FMOD_System_GetMasterChannelGroup.html
  [System::getMasterSoundGroup]: generated/FMOD_System_GetMasterSoundGroup.html
  [System::getNetworkProxy]: generated/FMOD_System_GetNetworkProxy.html
  [System::getNetworkTimeout]: generated/FMOD_System_GetNetworkTimeout.html
  [System::getNumDrivers]: generated/FMOD_System_GetNumDrivers.html
  [System::getNumPlugins]: generated/FMOD_System_GetNumPlugins.html
  [System::getOutput]: generated/FMOD_System_GetOutput.html
  [System::getOutputByPlugin]: generated/FMOD_System_GetOutputByPlugin.html
  [System::getOutputHandle]: generated/FMOD_System_GetOutputHandle.html
  [System::getPluginHandle]: generated/FMOD_System_GetPluginHandle.html
  [System::getPluginInfo]: generated/FMOD_System_GetPluginInfo.html
  [System::getRecordDriverInfo]: generated/FMOD_System_GetRecordDriverInfo.html
  [System::getRecordNumDrivers]: generated/FMOD_System_GetRecordNumDrivers.html
  [System::getRecordPosition]: generated/FMOD_System_GetRecordPosition.html
  [System::getReverbProperties]: generated/FMOD_System_GetReverbProperties.html
  [System::getSoftwareChannels]: generated/FMOD_System_GetSoftwareChannels.html
  [System::getSoftwareFormat]: generated/FMOD_System_GetSoftwareFormat.html
  [System::getSoundRAM]: generated/FMOD_System_GetSoundRAM.html
  [System::getSpeakerPosition]: generated/FMOD_System_GetSpeakerPosition.html
  [System::getStreamBufferSize]: generated/FMOD_System_GetStreamBufferSize.html
  [System::getUserData]: generated/FMOD_System_GetUserData.html
  [System::getVersion]: generated/FMOD_System_GetVersion.html
  [System::init]: generated/FMOD_System_Init.html
  [System::isRecording]: generated/FMOD_System_IsRecording.html
  [System::loadGeometry]: generated/FMOD_System_LoadGeometry.html
  [System::loadPlugin]: generated/FMOD_System_LoadPlugin.html
  [System::lockDSP]: generated/FMOD_System_LockDSP.html
  [System::mixerResume]: generated/FMOD_System_MixerResume.html
  [System::mixerSuspend]: generated/FMOD_System_MixerSuspend.html
  [System::playDSP]: generated/FMOD_System_PlayDSP.html
  [System::playSound]: generated/FMOD_System_PlaySound.html
  [System::recordStart]: generated/FMOD_System_RecordStart.html
  [System::recordStop]: generated/FMOD_System_RecordStop.html
  [System::registerCodec]: generated/FMOD_System_RegisterCodec.html
  [System::registerDSP]: generated/FMOD_System_RegisterDSP.html
  [System::release]: generated/FMOD_System_Release.html
  [System::set3DListenerAttributes]: FMOD_System_Set3DListenerAttributes.html
  [System::set3DNumListeners]: FMOD_System_Set3DNumListeners.html
  [System::set3DRolloffCallback]: FMOD_System_Set3DRolloffCallback.html
  [System::set3DSettings]: FMOD_System_Set3DSettings.html
  [System::setAdvancedSettings]: generated/FMOD_System_SetAdvancedSettings.html
  [System::setCallback]: generated/FMOD_System_SetCallback.html
  [System::setDSPBufferSize]: generated/FMOD_System_SetDSPBufferSize.html
  [System::setDriver]: generated/FMOD_System_SetDriver.html
  [System::setFileSystem]: generated/FMOD_System_SetFileSystem.html
  [System::setGeometrySettings]: generated/FMOD_System_SetGeometrySettings.html
  [System::setNetworkProxy]: generated/FMOD_System_SetNetworkProxy.html
  [System::setNetworkTimeout]: generated/FMOD_System_SetNetworkTimeout.html
  [System::setOutput]: generated/FMOD_System_SetOutput.html
  [System::setOutputByPlugin]: generated/FMOD_System_SetOutputByPlugin.html
  [System::setPluginPath]: generated/FMOD_System_SetPluginPath.html
  [System::setReverbProperties]: generated/FMOD_System_SetReverbProperties.html
  [System::setSoftwareChannels]: generated/FMOD_System_SetSoftwareChannels.html
  [System::setSoftwareFormat]: generated/FMOD_System_SetSoftwareFormat.html
  [System::setSpeakerPosition]: generated/FMOD_System_SetSpeakerPosition.html
  [System::setStreamBufferSize]: generated/FMOD_System_SetStreamBufferSize.html
  [System::setUserData]: generated/FMOD_System_SetUserData.html
  [System::unloadPlugin]: generated/FMOD_System_UnloadPlugin.html
  [System::unlockDSP]: generated/FMOD_System_UnlockDSP.html
  [System::update]: generated/FMOD_System_Update.html
  [Studio::System::initialize]: generated/FMOD_Studio_System_Initialize.html
  [Studio::System::getLowLevelSystem]: generated/FMOD_Studio_System_GetLowLevelSystem.html
  [6]: generated/studio_api_interfaces.html
  [7]: generated/studio_api_functions.html
  [8]: generated/studio_api_structures.html
  [9]: generated/studio_api_defines.html
  [10]: generated/studio_api_enumerations.html
  [Studio::Bank::getEventCount]: generated/FMOD_Studio_Bank_GetEventCount.html
  [Studio::Bank::getEventList]: generated/FMOD_Studio_Bank_GetEventList.html
  [Studio::Bank::getID]: generated/FMOD_Studio_Bank_GetID.html
  [Studio::Bank::getLoadingState]: generated/FMOD_Studio_Bank_GetLoadingState.html
  [Studio::Bank::getMixerStripCount]: generated/FMOD_Studio_Bank_GetMixerStripCount.html
  [Studio::Bank::getMixerStripList]: generated/FMOD_Studio_Bank_GetMixerStripList.html
  [Studio::Bank::getPath]: generated/FMOD_Studio_Bank_GetPath.html
  [Studio::Bank::getSampleLoadingState]: generated/FMOD_Studio_Bank_GetSampleLoadingState.html
  [Studio::Bank::loadSampleData]: generated/FMOD_Studio_Bank_LoadSampleData.html
  [Studio::Bank::unload]: generated/FMOD_Studio_Bank_Unload.html
  [Studio::Bank::unloadSampleData]: generated/FMOD_Studio_Bank_UnloadSampleData.html
  [Studio::System::loadBankFile]: generated/FMOD_Studio_System_LoadBankFile.html
  [Studio::System::loadBankMemory]: generated/FMOD_Studio_System_LoadBankMemory.html
  [Studio::System::loadBankCustom]: generated/FMOD_Studio_System_LoadBankCustom.html
  [FMOD\_STUDIO\_EVENT\_CALLBACK]: generated/FMOD_STUDIO_EVENT_CALLBACK.html
  [Studio::CueInstance::trigger]: generated/FMOD_Studio_CueInstance_Trigger.html
  [Studio::EventInstance::getCue]: generated/FMOD_Studio_EventInstance_GetCue.html
  [Studio::EventInstance::getCueByIndex]: generated/FMOD_Studio_EventInstance_GetCueByIndex.html
  [Studio::EventInstance::getCueCount]: generated/FMOD_Studio_EventInstance_GetCueCount.html
  [FMOD\_STUDIO\_INITFLAGS]: generated/FMOD_STUDIO_INITFLAGS.html
  [FMOD\_STUDIO\_LOAD\_BANK\_FLAGS]: generated/FMOD_STUDIO_LOAD_BANK_FLAGS.html
  [FMOD\_STUDIO\_RECORD\_COMMANDS\_FLAGS]: generated/FMOD_STUDIO_RECORD_COMMANDS_FLAGS.html
  [FMOD\_STUDIO\_EVENT\_CALLBACK\_TYPE]: generated/FMOD_STUDIO_EVENT_CALLBACK_TYPE.html
  [FMOD\_STUDIO\_LOADING\_MODE]: generated/FMOD_STUDIO_LOADING_MODE.html
  [FMOD\_STUDIO\_LOADING\_STATE]: generated/FMOD_STUDIO_LOADING_STATE.html
  [FMOD\_STUDIO\_LOAD\_MEMORY\_MODE]: generated/FMOD_STUDIO_LOAD_MEMORY_MODE.html
  [FMOD\_STUDIO\_PARAMETER\_TYPE]: generated/FMOD_STUDIO_PARAMETER_TYPE.html
  [FMOD\_STUDIO\_PLAYBACK\_STATE]: generated/FMOD_STUDIO_PLAYBACK_STATE.html
  [FMOD\_STUDIO\_STOP\_MODE]: generated/FMOD_STUDIO_STOP_MODE.html
  [FMOD\_STUDIO\_USER\_PROPERTY\_TYPE]: generated/FMOD_STUDIO_USER_PROPERTY_TYPE.html
  [Studio::EventDescription::createInstance]: generated/FMOD_Studio_EventDescription_CreateInstance.html
  [Studio::EventDescription::getID]: generated/FMOD_Studio_EventDescription_GetID.html
  [Studio::EventDescription::getInstanceCount]: generated/FMOD_Studio_EventDescription_GetInstanceCount.html
  [Studio::EventDescription::getInstanceList]: generated/FMOD_Studio_EventDescription_GetInstanceList.html
  [Studio::EventDescription::getLength]: generated/FMOD_Studio_EventDescription_GetLength.html
  [Studio::EventDescription::getMaximumDistance]: generated/FMOD_Studio_EventDescription_GetMaximumDistance.html
  [Studio::EventDescription::getMinimumDistance]: generated/FMOD_Studio_EventDescription_GetMinimumDistance.html
  [Studio::EventDescription::getParameter]: generated/FMOD_Studio_EventDescription_GetParameter.html
  [Studio::EventDescription::getParameterByIndex]: generated/FMOD_Studio_EventDescription_GetParameterByIndex.html
  [Studio::EventDescription::getParameterCount]: generated/FMOD_Studio_EventDescription_GetParameterCount.html
  [Studio::EventDescription::getPath]: generated/FMOD_Studio_EventDescription_GetPath.html
  [Studio::EventDescription::getSampleLoadingState]: generated/FMOD_Studio_EventDescription_GetSampleLoadingState.html
  [Studio::EventDescription::getUserData]: generated/FMOD_Studio_EventDescription_GetUserData.html
  [Studio::EventDescription::getUserProperty]: generated/FMOD_Studio_EventDescription_GetUserProperty.html
  [Studio::EventDescription::getUserPropertyByIndex]: generated/FMOD_Studio_EventDescription_GetUserPropertyByIndex.html
  [Studio::EventDescription::getUserPropertyCount]: generated/FMOD_Studio_EventDescription_GetUserPropertyCount.html
  [Studio::EventDescription::is3D]: FMOD_Studio_EventDescription_Is3D.html
  [Studio::EventDescription::isOneshot]: generated/FMOD_Studio_EventDescription_IsOneshot.html
  [Studio::EventDescription::isStream]: generated/FMOD_Studio_EventDescription_IsStream.html
  [Studio::EventDescription::loadSampleData]: generated/FMOD_Studio_EventDescription_LoadSampleData.html
  [Studio::EventDescription::releaseAllInstances]: generated/FMOD_Studio_EventDescription_ReleaseAllInstances.html
  [Studio::EventDescription::setCallback]: generated/FMOD_Studio_EventDescription_SetCallback.html
  [Studio::EventDescription::setUserData]: generated/FMOD_Studio_EventDescription_SetUserData.html
  [Studio::EventDescription::unloadSampleData]: generated/FMOD_Studio_EventDescription_UnloadSampleData.html
  [Studio::System::getEvent]: generated/FMOD_Studio_System_GetEvent.html
  [Studio::EventInstance::createSubEvent]: generated/FMOD_Studio_EventInstance_CreateSubEvent.html
  [Studio::EventInstance::get3DAttributes]: FMOD_Studio_EventInstance_Get3DAttributes.html
  [Studio::EventInstance::getChannelGroup]: generated/FMOD_Studio_EventInstance_GetChannelGroup.html
  [Studio::EventInstance::getDescription]: generated/FMOD_Studio_EventInstance_GetDescription.html
  [Studio::EventInstance::getLoadingState]: generated/FMOD_Studio_EventInstance_GetLoadingState.html
  [Studio::EventInstance::getParameter]: generated/FMOD_Studio_EventInstance_GetParameter.html
  [Studio::EventInstance::getParameterByIndex]: generated/FMOD_Studio_EventInstance_GetParameterByIndex.html
  [Studio::EventInstance::getParameterCount]: generated/FMOD_Studio_EventInstance_GetParameterCount.html
  [Studio::EventInstance::getPaused]: generated/FMOD_Studio_EventInstance_GetPaused.html
  [Studio::EventInstance::getPitch]: generated/FMOD_Studio_EventInstance_GetPitch.html
  [Studio::EventInstance::getPlaybackState]: generated/FMOD_Studio_EventInstance_GetPlaybackState.html
  [Studio::EventInstance::getTimelinePosition]: generated/FMOD_Studio_EventInstance_GetTimelinePosition.html
  [Studio::EventInstance::getUserData]: generated/FMOD_Studio_EventInstance_GetUserData.html
  [Studio::EventInstance::getVolume]: generated/FMOD_Studio_EventInstance_GetVolume.html
  [Studio::EventInstance::isVirtual]: generated/FMOD_Studio_EventInstance_IsVirtual.html
  [Studio::EventInstance::release]: generated/FMOD_Studio_EventInstance_Release.html
  [Studio::EventInstance::set3DAttributes]: FMOD_Studio_EventInstance_Set3DAttributes.html
  [Studio::EventInstance::setCallback]: generated/FMOD_Studio_EventInstance_SetCallback.html
  [Studio::EventInstance::setParameterValue]: generated/FMOD_Studio_EventInstance_SetParameterValue.html
  [Studio::EventInstance::setParameterValueByIndex]: generated/FMOD_Studio_EventInstance_SetParameterValueByIndex.html
  [Studio::EventInstance::setPaused]: generated/FMOD_Studio_EventInstance_SetPaused.html
  [Studio::EventInstance::setPitch]: generated/FMOD_Studio_EventInstance_SetPitch.html
  [Studio::EventInstance::setTimelinePosition]: generated/FMOD_Studio_EventInstance_SetTimelinePosition.html
  [Studio::EventInstance::setUserData]: generated/FMOD_Studio_EventInstance_SetUserData.html
  [Studio::EventInstance::setVolume]: generated/FMOD_Studio_EventInstance_SetVolume.html
  [Studio::EventInstance::start]: generated/FMOD_Studio_EventInstance_Start.html
  [Studio::EventInstance::stop]: generated/FMOD_Studio_EventInstance_Stop.html
  [ParseID]: generated/FMOD_Studio_ParseID.html
  [11]: generated/studio_api_System.html
  [EventDescription]: generated/studio_api_EventDescription.html
  [EventInstance]: generated/studio_api_EventInstance.html
  [CueInstance]: generated/studio_api_CueInstance.html
  [ParameterInstance]: generated/studio_api_ParameterInstance.html
  [MixerStrip]: generated/studio_api_MixerStrip.html
  [Bank]: generated/studio_api_Bank.html
  [Studio::MixerStrip::getChannelGroup]: generated/FMOD_Studio_MixerStrip_GetChannelGroup.html
  [Studio::MixerStrip::getFaderLevel]: generated/FMOD_Studio_MixerStrip_GetFaderLevel.html
  [Studio::MixerStrip::getID]: generated/FMOD_Studio_MixerStrip_GetID.html
  [Studio::MixerStrip::getLoadingState]: generated/FMOD_Studio_MixerStrip_GetLoadingState.html
  [Studio::MixerStrip::getMute]: generated/FMOD_Studio_MixerStrip_GetMute.html
  [Studio::MixerStrip::getPath]: generated/FMOD_Studio_MixerStrip_GetPath.html
  [Studio::MixerStrip::getPaused]: generated/FMOD_Studio_MixerStrip_GetPaused.html
  [Studio::MixerStrip::release]: generated/FMOD_Studio_MixerStrip_Release.html
  [Studio::MixerStrip::setFaderLevel]: generated/FMOD_Studio_MixerStrip_SetFaderLevel.html
  [Studio::MixerStrip::setMute]: generated/FMOD_Studio_MixerStrip_SetMute.html
  [Studio::MixerStrip::setPaused]: generated/FMOD_Studio_MixerStrip_SetPaused.html
  [Studio::MixerStrip::stopAllEvents]: generated/FMOD_Studio_MixerStrip_StopAllEvents.html
  [Studio::System::getMixerStrip]: generated/FMOD_Studio_System_GetMixerStrip.html
  [Studio::ParameterInstance::getDescription]: generated/FMOD_Studio_ParameterInstance_GetDescription.html
  [Studio::ParameterInstance::getValue]: generated/FMOD_Studio_ParameterInstance_GetValue.html
  [Studio::ParameterInstance::setValue]: generated/FMOD_Studio_ParameterInstance_SetValue.html
  [FMOD\_STUDIO\_ADVANCEDSETTINGS]: generated/FMOD_STUDIO_ADVANCEDSETTINGS.html
  [FMOD\_STUDIO\_BANK\_INFO]: generated/FMOD_STUDIO_BANK_INFO.html
  [FMOD\_STUDIO\_BUFFER\_INFO]: generated/FMOD_STUDIO_BUFFER_INFO.html
  [FMOD\_STUDIO\_BUFFER\_USAGE]: generated/FMOD_STUDIO_BUFFER_USAGE.html
  [FMOD\_STUDIO\_CPU\_USAGE]: generated/FMOD_STUDIO_CPU_USAGE.html
  [FMOD\_STUDIO\_PARAMETER\_DESCRIPTION]: generated/FMOD_STUDIO_PARAMETER_DESCRIPTION.html
  [FMOD\_STUDIO\_PROGRAMMER\_SOUND\_PROPERTIES]: generated/FMOD_STUDIO_PROGRAMMER_SOUND_PROPERTIES.html
  [FMOD\_STUDIO\_USER\_PROPERTY]: generated/FMOD_STUDIO_USER_PROPERTY.html
  [Studio::System::create]: generated/FMOD_Studio_System_Create.html
  [Studio::System::flushCommands]: generated/FMOD_Studio_System_FlushCommands.html
  [Studio::System::getAdvancedSettings]: generated/FMOD_Studio_System_GetAdvancedSettings.html
  [Studio::System::getBank]: generated/FMOD_Studio_System_GetBank.html
  [Studio::System::getBankCount]: generated/FMOD_Studio_System_GetBankCount.html
  [Studio::System::getBankList]: generated/FMOD_Studio_System_GetBankList.html
  [Studio::System::getBufferUsage]: generated/FMOD_Studio_System_GetBufferUsage.html
  [Studio::System::getCPUUsage]: generated/FMOD_Studio_System_GetCPUUsage.html
  [Studio::System::getListenerAttributes]: generated/FMOD_Studio_System_GetListenerAttributes.html
  [Studio::System::lookupID]: generated/FMOD_Studio_System_LookupID.html
  [Studio::System::lookupPath]: generated/FMOD_Studio_System_LookupPath.html
  [Studio::System::playbackCommands]: generated/FMOD_Studio_System_PlaybackCommands.html
  [Studio::System::registerPlugin]: generated/FMOD_Studio_System_RegisterPlugin.html
  [Studio::System::release]: generated/FMOD_Studio_System_Release.html
  [Studio::System::resetBufferUsage]: generated/FMOD_Studio_System_ResetBufferUsage.html
  [Studio::System::setAdvancedSettings]: generated/FMOD_Studio_System_SetAdvancedSettings.html
  [Studio::System::setListenerAttributes]: generated/FMOD_Studio_System_SetListenerAttributes.html
  [Studio::System::startRecordCommands]: generated/FMOD_Studio_System_StartRecordCommands.html
  [Studio::System::stopRecordCommands]: generated/FMOD_Studio_System_StopRecordCommands.html
  [Studio::System::unloadAll]: generated/FMOD_Studio_System_UnloadAll.html
  [Studio::System::unregisterPlugin]: generated/FMOD_Studio_System_UnregisterPlugin.html
  [Studio::System::update]: generated/FMOD_Studio_System_Update.html
