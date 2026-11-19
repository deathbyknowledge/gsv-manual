# Shop With Ship

[Talk With Ship And Manage Work](index.md)

Ship helps with buying things: checking whether something is on sale, comparing products and prices, choosing a gift, buying, and following the order until it arrives. The built-in `shopping` skill holds the full procedure; read it with `skills show shopping` before starting.

## The Steps

Ship works through six steps in order:

1. **Understand.** Ship checks memory first: online or in store, who it is for, budget, favored stores, taste, purpose and timing. It starts searching with what it knows and states its assumptions with the first options instead of asking everything upfront.
2. **Research.** Ship narrows toward three options, then reads forums, reviews and other non-sponsored buyer experience rather than trusting product descriptions. It says which stores it checked and which it could not.
3. **Recommend.** Each of three options arrives in its own message with an image, what people like and dislike, and one to three places to buy it with price, delivery and a working product link. Stock, size and color are checked first, and the full cost is shown.
4. **Buy.** Online only. By default Ship sends the product page and offers to finish the purchase.
5. **Track delivery.** Online only. Ship follows the order and reports only changes.
6. **Close.** Ship asks how the product and delivery went and updates preferences.

New input during Recommend goes back to Understand. A decision moves to Buy.

## When Ship Asks First

- **Purchases and store accounts.** Ship buys or creates an account only after the owner has explicitly allowed it to do so by default. Until then it hands over the product page. A first payment or sign-in on a store is always the owner's step, in the live browser or through a handoff link; see [Use a browser target](../devices-workplaces/browser-targets.md).
- **Support and claims.** Ship confirms with the owner before contacting a store's support or opening a claim about a late or wrong delivery.
- **Taste and needs.** Ship never assumes a taste or a need without confirming it. Casual browsing may be for someone else.
- **Scope.** Ship recommends and buys only what was asked for, with no added items, bundles or upgrades.

Ordinary approval rules still apply to each action; see [Models and approvals](../settings/ai-voice-approvals.md).

## What Ship Keeps

- **Preferences** go in the personal wiki: the owner's taste, budgets, favored and avoided stores, and the standing purchase permission with its scope. A gift's outcome goes on that person's page. See [Memory, context, and skills](../files-knowledge/context-files-knowledge.md).
- **Open purchases** are responsibilities. One is created when there is a need with a date, and it follows the order through delivery:

```bash
r12y list
r12y show <responsibility-id>
```

- **Order and shipping email** goes to Ship's own address where possible; see [Use Ship's email address](../integrations/email.md).

## How Ship Talks While Shopping

Ship does not narrate its steps. It only asks and says what is needed to move forward.

On a messenger, when a search will take more than a minute, Ship sends one short message saying what it is checking and roughly how long it will take, then the results. It does not narrate browsers, tools or retries. Websites are reached as described in [Use a browser target](../devices-workplaces/browser-targets.md).
