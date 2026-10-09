# Use Voice And Gestures

[Web And Desktop](index.md)

Web and Desktop can turn speech into a message draft. Web records audio for
transcription through your space. Desktop uses local transcription and, on
supported computers, camera gestures to control the draft. Desktop microphone
and camera processing stay on the computer.

## Dictate

### Web

In web Zen, choose **record** and allow browser microphone access. The prompt
becomes a live waveform that responds to your voice; your typed draft is kept
underneath. Choose **stop** when finished. After **transcribing…**, the
draft returns with the words added at its cursor. Review or edit them and press
Enter to send. Enter during recording only stops it for review; Escape cancels
and restores the draft. Recordings stop automatically after five minutes and
are limited to 25 MiB, or the space's smaller limit.

The browser sends the finished audio through your space to its configured
transcription provider. The recording is not attached to the message. **cancel**
discards recording or transcription while keeping typed text. Leaving Zen,
hiding the tab, switching conversations or places, disconnecting, or clearing
the draft also cancels it. If transcription fails, **retry transcription** uses
the audio still held in the tab.

Use HTTPS and a browser that supports microphone recording. If permission is
denied, enable the microphone in the browser's site settings. Provider or
permission errors come from the space's transcription configuration; web voice
does not need a connected computer or the Desktop helper.

### Desktop

In Zen, the composer's **Voice and hands-free** control has a **listen** button
that dictates with the microphone. Partial transcription appears in the draft
while you speak, and you can edit it before sending. Listening stops when you
pause it; sending is a separate action unless you use the send gesture.

The first use may require operating-system permission for the microphone and
downloads a local voice model; Desktop shows the download progress. Choose the
intended microphone if more than one is available. On Windows, enable microphone
and camera access for desktop apps in Windows Privacy settings. These controls
run in the signed-in Desktop session; the background machine service does not
capture audio or video before login.

Windows local voice requires a CPU with AVX2, FMA and F16C support. Desktop
explains when the CPU does not support voice; the rest of Desktop and the
background machine service remain available.

## Hands-Free

**Enable hands-free** turns on the camera. Hands-free has three states: **Off**,
**Ready** (armed, waiting for a command), and **Listening** (dictating). The
same control opens the **Quick guide** and an interactive tutorial that walks
through every gesture with animated hands.

Your right hand gives commands. Your left hand joins in only to scroll and to
switch hands-free off. Make a fist between commands, and hold each pose until
Desktop acknowledges it: about 350 milliseconds for ordinary commands, about a
second for clearing text, and about 700 milliseconds for both fists.

| Right hand | Effect |
| --- | --- |
| Any one finger (thumb counts) | Start listening, or pause it. Pausing keeps your draft. |
| Any two fingers | Send the current draft; listening continues. |
| Three fingers | Delete the last dictated character. |
| Four fingers | Clear dictated text, keeping typed text and files. |
| Both hands as fists | Switch hands-free off. |

Any combination of fingers counts; only the number matters. There is no
five-finger command.

To scroll, open the left palm and hold the right hand as a fist. Once the pose
settles, tilt the line between the two hands to set direction and speed;
return to level to stop, or release either hand.

## Desktop Safety And Privacy

- Camera frames, hand landmarks, and microphone audio remain local to the computer.
- Gestures act only on the visible voice draft, and each action is bound to the current request.
- Losing hand tracking clears the active gesture state.
- Hands-free and the camera stop when you leave Zen or the computer sleeps.

## If Desktop Voice Or Gestures Do Not Work

1. Check the state shown by the **Voice and hands-free** control; **input needs
   attention** offers **reconnect input**.
2. Confirm microphone and camera permission in the operating system.
3. Close other applications that may have exclusive access to the device.
4. Open the **Quick guide** or the tutorial and confirm the intended poses are
   recognized before relying on them.
5. Voice and gesture problems are local to Desktop and can occur even when the
   computer is connected as a place; check **this computer** in the space menu
   separately for the machine connection.

Typing, clicking, and ordinary message sending remain available when these
optional controls are unavailable.
