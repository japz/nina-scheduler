---
layout: default
title: Profiles
parent: Project / Target Management
nav_order: 1
---

# Profiles
Each NINA profile is represented with a (possibly empty) folder in the navigation trees.  Your projects, targets, etc are explicitly associated with a single NINA profile since the associated settings will likely depend on the equipment defined for that profile.

If you delete a profile that had Target Scheduler entities assigned to it, they are not lost, but they are [orphaned](index.html#orphaned-items).

## Profile Preferences
A set of preferences can be managed for each profile and will impact execution of all projects and targets associated with that profile.

### General Preferences

|Property|Type|Default|Description|
|:--|:--|:--|:--|
|Park On Wait|bool|false|Normally, when the planner returns a directive to wait a period of time for the next target, the plugin will simply stop tracking and guiding.  If this setting is true (and the wait is more than one minute), the mount will also be parked and then unparked when the wait is over.  If you instead use the [Before Wait/After Wait](../sequencer/index.html#custom-event-instructions) custom containers to park and unpark, you should leave this set to false.|
|Exposure Throttle|int|125%|When Image Grading is disabled (at the Project level) and the Accepted count on Exposure Plans isn't incremented manually, the planner will keep scheduling exposures - perhaps way beyond what is reasonable.  The Exposure Throttle will instead use the total number Acquired (displayed with Desired and Accepted) to stop exposures when the number Acquired is greater than Exposure Throttle times the number Desired.  For example, if Exposure Throttle is 150%, Desired=10, and Acquired=5 then an additional 10 exposures will be scheduled.  This has no effect if Image Grading is enabled.|

### Image Grader
The following preferences drive the behavior of the [Image Grader](../post-acquisition/image-grader.html).  Since projects have grading enabled by default and all types of grading (below) are also enabled by default, your images will be graded unless you take steps to disable it.  The defaults were selected to be relatively permissive.

|Property|Type|Default|Description|
|:--|:--|:--|:--|
|Max Samples|int|10|The maximum number of recent images to use for sample determination|
|Grade RMS|bool|true|Enable grading based on the total RMS guiding error during the exposure|
|RMS Pixel Threshold|double|8|The threshold to accept/reject based on guiding RMS error|
|Grade Detected Stars|bool|true|Enable grading for the number of detected stars|
|Detected Stars Sigma Factor|double|4|The number of standard deviations surrounding the mean for acceptable star count values|
|Grade HFR|bool|true|Enable grading based on calculated image HFR|
|HFR Sigma Factor|double|4|The number of standard deviations surrounding the mean for acceptable values of HFR|
|Accept All Improvements|bool|true|Grading on star count and HFR will be biased based on the samples used for comparison.  If they are sub-optimal in some way (bad seeing, passing cloud) then subsequent images with significant improvements may be rejected for falling outside the standard deviation range - and the set of comparison samples will not improve.  If this setting is true, then a new image with a sample value greater than (for star count) or less than (for HFR) the mean of the comparison samples will be automatically accepted.|
