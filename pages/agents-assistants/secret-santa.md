# Run a Secret Santa With Ship

[Talk With Ship And Manage Work](index.md)

Ship can run a Secret Santa with other people's Ships: gathering everyone, drawing names, passing wishes and questions along in secret, and making sure each gift arrives before the swap. The built-in `secret-santa` skill holds the full procedure; read it with `skills show secret-santa`.

## The Hat

The organiser's Ship is the hat. Every message goes through it, so a participant's Ship never talks to the Ship of the person giving them a gift. Nobody is told who drew whom, including the organiser: Ship reports progress only in counts and never answers "who has me?".

Everyone playing needs a Ship and a contact connection with the organiser; see [Contacts](../integrations/contacts.md). The organiser can play too: their Ship gives them their match like everyone else's.

## Organising

1. **Start.** Tell Ship you want to run a Secret Santa. It asks you for anything you have not said yet, and never picks any of it for you:
   - the name of the event
   - who is taking part, and whether you play too
   - the budget
   - in person or remote
   - the draw date, when sign-ups close
   - the swap date and place
   - any pairs who should not draw each other

   The type changes delivery:
   - **In person:** gifts go to the address you give, such as the office, unless a giver prefers another place. Nobody shares a home address.
   - **With remote people:** each remote participant's Ship sends a delivery address to your Ship, with their owner's OK. At work, the organiser should be someone from HR or another person responsible for and authorised to handle colleagues' personal data.

   Ship repeats the plan back to you, then opens one responsibility for it.
2. **Gather.** Ship invites people by handle or by email; an email invitation also lets someone without a Ship create one. When a colleague's Ship asks to join, accept the request under People. Ship cannot accept contact requests for you. As the draw date gets closer, Ship reminds you who has not signed up yet.
3. **Draw.** On the draw date, Ship confirms the names with you, then a script draws one shuffled loop: nobody draws themselves, and everyone gives once and receives once. Pairs that should not draw each other can be excluded. Each Ship receives only its own match, with any wishes that arrived early and, for a remote recipient, the delivery address for the order.
4. **Wishes and questions.** Ship forwards each wish to the right giver and each question to the right person, without names. A wish sent before the draw waits in your Ship and goes out with the match.
5. **Close.** After the swap, Ship deletes the draw, the wishes and the addresses. A reveal happens only if everyone agrees.

If someone joins or leaves after the draw, Ship draws everyone again and tells you first: everyone gets a new match, marked as the newest round, and their Ship keeps only the newest.

## Taking Part

Tell your Ship you're in someone's Secret Santa, for example "I'm in @ana's Secret Santa". It connects to the organiser's Ship. Tell it what you would like within the budget, before or after the draw; it sends that to the hat. Once the draw is done, it shows you your match, the budget and the swap date. You pick the gift, and Ship can suggest ideas from the wishes; Ship makes sure it fits the budget and arrives before the swap. Questions from your Secret Santa reach you the same way.

- **In person:** your gift goes to the address the organiser gave, or wherever you prefer, never to the recipient's home. Ship never asks for your address.
- **Remote:** if you will not be at the swap, Ship asks you for a delivery address and your OK before sending it to the organiser's Ship. Only whoever drew you receives it, with their match, to use for the order.

## What the Organiser Can See

Who drew whom lives in a draw file in the organiser's Ship that only the draw script reads. The people, their wishes and any addresses live in a second file that the organiser's Ship works from. Messages between Ships travel through the contact conversation under People, so both people in a conversation can read them, including each match message the organiser's Ship sends. The organiser's Activity also keeps every command Ship ran for 90 days, including the match messages and any addresses, and Ship's own history and archives keep the messages it received and the commands it ran, with no set end. A message that fails for good also opens a delivery responsibility in Work naming the contact it was for, and the giver's Ship's history keeps the address it was sent. Deleting both files when the game closes does not remove what Activity, Ship's history, Work and People keep. Ship never shows or tells the organiser, but they own their Ship and can inspect it, as whoever holds a paper hat could look inside.

Responsibilities hold the list of people, the budget and the dates, never the pairs or addresses. Ordinary approval rules still apply to each message and purchase; see [Models and approvals](../settings/ai-voice-approvals.md).
