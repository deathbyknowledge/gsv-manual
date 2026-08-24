# Use Voice And Gestures

[Web And Desktop](index.md)

Desktop can turn speech into a message draft and, on supported computers, use
camera gestures to control that draft. Microphone and camera processing stay on
the computer.

## Start Voice Input

Use the microphone control in Desktop or choose **Start Voice** from the system
status menu. Desktop shows partial transcription in the composer while you
speak. You can edit the draft before sending it.

The first use may require operating-system permission for the microphone and a
short model download. Choose the intended microphone if more than one is
available.

Finishing voice input stops listening; sending is a separate action unless you
explicitly use the Send gesture.

## Gesture Guide

Open **Gesture Guide** from Desktop or its status menu. On macOS, `Command +
Shift + G` also toggles it.

Gesture control starts disarmed. Hold both hands as closed fists for about 700
milliseconds to arm it. Repeat the same gesture to disarm it. After a command,
return the action hand to a fist before giving another command.

| Action-hand pose | While idle | While listening |
| --- | --- | --- |
| One finger: index only | Start transcription | Finish transcription |
| Two fingers: index and middle | — | Send the current utterance and keep listening |
| Three fingers | — | Delete one visible character from unsent dictation |
| Four fingers, thumb closed | — | Clear dictated text while keeping typed text and files |
| Five fingers | — | Mute or unmute the microphone |

Hold ordinary commands for about 350 milliseconds. Clearing dictation requires
about one second so it is difficult to trigger accidentally.

To scroll, hold the action hand as a fist and the other hand as an open palm.
After the pose settles, tilt the line between the hands to control direction
and speed. Return to the neutral angle to pause or release either hand to stop.

## Safety And Privacy

- Camera frames, landmarks, and microphone audio remain local to the computer.
- Every camera action is bound to the current voice request.
- Losing hand tracking clears the active gesture state.
- Mute changes after the microphone confirms it.
- Gestures act on the visible voice draft.

## If Voice Or Gestures Do Not Work

1. Check the voice and gesture labels in the status menu.
2. Confirm microphone and camera permission in the operating system.
3. Close other applications that may have exclusive access to the device.
4. Open the Gesture Guide and verify that the intended hands and poses are
   recognized before relying on them.
5. Use **Machine diagnostics** for machine-connection problems; voice and
   gesture problems are local to Desktop and can occur even when the machine is
   connected.

Typing, clicking, and ordinary message sending remain available when these
optional controls are unavailable.
