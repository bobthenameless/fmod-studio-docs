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

See Also
--------

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

Remarks
-------

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

Remarks
-------

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

See Also
--------

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

See Also
--------

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

See Also
--------

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

Remarks
-------

Initializing the FMOD Studio System object will also initialise the low
level System object.

See Also
--------

-   [Studio::System::create](FMOD_Studio_System_Create.html)
-   [Studio::System::initialize](FMOD_Studio_System_Initialize.html)

