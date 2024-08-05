---
title: Audio Split Combine
class: heading_no_counter
keywords: Audio Split, Audio Combine
desc: Audio Split Merge tool to split an audio into multiple or merge multiple audios into one
---

## Introduce
This tool allows you to split an audio into multiple or combine multiple audios into one, and the audio split supports spectrum visualization operations.

![](../../assets/images/ToolsSet/TSMAudioSplit.png)

## How to use
The top is the audio split area, and the bottom is the audio combine area

* Audio split
  * Open audio file: Click the Open File button in the top toolbar to select the audio file in MP3 or WAV format
  * Audio playback: You can click the play, pause, and stop buttons in the toolbar to control it
  * Split audio: Click the mouse on the spectrogram to set the split position, and then click the orange [Split] button in the toolbar to add a split marker, and the split audio start and end time and duration will be displayed in the list below
  * Adjust the segment: When you need to adjust, you can click the red [Clear] button on the toolbar to clear all and add them again, or you can click the delete button in the top right corner of the segmentation list item to delete a segment
  * Save result: Click the [Save] button on the right side of the toolbar to save the split result as an MP3 file
  > The position adjustment on the spectrogram can only be clicked, not support dragged
  >
  > If the click position is too close to the split position (less than 1 second), splitting will change the previous position 
  >
  > When saving audio, the audio with a duration of 0 is not saved
   
* Audio combine
  * Add audio: Click the Add File button on the left to open the Select File dialog box, from which you can select audio files in MP3 or WAV format, and multiple selections are supported
  * Adjust audio: You can click the delete button on the left to clear the list on the right, or click the delete button in the top right corner of the list item to delete an audio; The start and end times in a list item can be modified
  * Save result: Click the [Save] button on the left to save the combined result as a WAV file
  > If the save fails, the reason for the failure is displayed, which may be the wrong audio file format, inconsistent bitrate, or wrong duration 