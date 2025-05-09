# Nexus: A Solitaire Card Game

*UNDER CONSTRUCTION*

## Overview and Objective

Nexus: A Solitaire Card Game is a web-based solitaire card game designed to be played either via a web app or with physical decks.  
In this game, you (the sole player) build sequences of cards to achieve a target number, lock them for points, and use special Fixit cards to manipulate locked sequences or correct misplays.

Your play deck is entirely facedown (like traditional Solitaire). You draw the top card from this deck one by one during your turn. Meanwhile, the Fixit deck (10 cards total) is kept apart, and you start with 2 Fixit cards shown face up so that you know what fixes are available—but you do not know what the next card from your play deck will be.

The game emphasizes strategy and suspense—stemming from the uncertainty of the next card in your facedown deck—while Fixit cards are visible so you know exactly what fixes you can apply.  
Once play starts, the deck remains as is; it cannot be reshuffled during normal play unless you use a special "SHUFFLE DECK" Fixit card.

## Basic Game Rules

- The objective is to build ascending sequences of cards that add up to a defined target number.
  - The target number is randomly generated in the web version by selecting five cards face down from a shuffled deck and summing their values.
  - The minimum possible target is 5 (if all selected cards have a value of 1) and the maximum is 65 (if all selected cards are 13).
  - When playing with physical cards, these same limits apply.
- At the start, the game shuffles a 52-card play deck (which is entirely facedown) and a 10-card Fixit deck.
- The play deck is held as a whole; you draw the top card one by one on each turn.
- The Fixit deck is kept separate; 2 Fixit cards are revealed face up from it at the start.
- On a player's turn, you may choose one of two actions:
  1. Draw the next card from your facedown play deck and play it to continue or complete a sequence.
     - The drawn card is used immediately to build or extend a sequence, and the game state updates accordingly.
  2. Play a Fixit card (from the pre-dealt Fixit cards, which are face up).
     - Once played (after revealing its effect), the Fixit card’s action (insert, reorder, remove, or retrieve) is applied immediately.
     - The use of a Fixit card immediately terminates the current action phase.
- Note: Once play begins, the facedown deck remains in its current order. It cannot be reshuffled during regular play; only a "SHUFFLE DECK" Fixit card may reshuffle the deck.
- Locked sequences earn points, with bonus points awarded for efficient use of Fixit cards.
- Illegal moves, such as playing a card that does not fit into a sequence, are blocked and leave the game state unchanged.
- Win/Loss Conditions:
  - You win by successfully locking sequences that meet or exceed the target number while following all game rules.
  - The game is lost if the play deck and any remaining drawn cards (if applicable) are exhausted without meeting the target number or if an illegal move disrupts game flow.
- Persisting the game state via localStorage enables game sessions to be resumed later.

[AI Prompt (in progress)](prompt.txt)

## Sample Playthrough

Turn 1:

- The game begins by shuffling both the play deck and the Fixit deck.
- You start with a complete facedown play deck and 2 Fixit cards are revealed face up.
- In the web version, the target number (e.g., 32) is generated by summing 5 random card values.
- You turn the entire play deck upside down and draw the top card to start a new ascending sequence.
- Tip: When drawing, aim to use a low or medium card to gradually build towards the target number without overshooting it.

Turn 2:

- The updated game state is rendered, showing the drawn card(s) forming your sequence, your score, and the remaining count of cards in your facedown play deck.
- You draw the next card from the play deck. If the card fits the sequence, you play it and update the sequence; otherwise, it may still form the start of a new sequence.
- Tip: Watch for cards that naturally extend your sequence. Avoid using high cards too early unless they perfectly bridge a gap to get closer to the target.

Turn 3:

- Facing a challenging situation, you opt to use a Fixit card.
- You select one of the available Fixit cards (face up), reveal its action (e.g., insert a missing card into your sequence), and apply the fix immediately.
- This Fixit move ends your turn, and the card is marked as used.
- Tip: Save Fixit cards for critical adjustments in your sequence, as they are limited in number.

Turn 4:

- The game state refreshes with your updated sequence and score.
- You draw the next card from your facedown deck.
- You evaluate your sequence and plan your next move based on the revealed outcome.
- Hand Strategy Tips:
  - Look for cards that maintain the ascending order gradually nearing the target.
  - Preserve high cards for later turns when you need to close out your sequence without overshooting.
  - The overall goal is to build a flexible sequence that can be fine-tuned to hit the target number exactly.

## Game Mechanics and Key Rules

- **Sequence Building:**  
  Create sequences by arranging cards in ascending order. Clarify how duplicates or near-complete sequences are handled.

- **Locking Mechanism:**  
  Lock sequences to secure points. Locked sequences may provide bonus points.

- **Fixit Cards:**  
  A deck of 10 special Fixit cards is included. These cards are drawn face up so that you can see what fixes are available. However, your play deck is always facedown—ensuring that you do not know the next card until it is drawn.

  - When a Fixit card is played:
    - Place the card face down then reveal it immediately.
    - Its action (e.g., inserting, reordering, removing, or retrieving a card) is applied.
    - The turn ends immediately after the Fixit move.

- **Scoring and Turn Mechanics:**  
  Define the target number (static or dynamic) and how bonus points or penalties (e.g., for unused Fixit cards) are applied. Further clarify when and how the action phase ends.

## Scoring and Endgame Conditions

- The game ends when the play deck is exhausted and your hand is empty, or when no legal moves are available.
- At game end, your score is computed by:
  - Summing points from locked sequences that meet or exceed the target number.
  - Adding bonus points for effective use of Fixit cards.
  - Subtracting penalty points for any remaining cards in your hand (if applicable).
- In a series of games (for example, 10 games), the goal is to achieve the lowest cumulative score.
- For the web version, a real-time dashboard will display metrics such as:
  - Cards left in the play deck.
  - Current score and bonus/penalty details.
  - Turn count and other relevant statistics.
- Physical players will need to track these metrics manually.

## Modular Architecture and File Structure

This project is built with ES6 modules for maintainability and testing. The key aspects are:

- **Entry Point:**  
  The main game logic is initialized in `/src/main.js`.  
  The `index.html` file (located at the project root) loads this entry point via:

  ```html
  <script type="module" src="./src/main.js"></script>
  ```

- **Modular Organization:**  
  Logic is separated into modules located in `/src/modules`:

  - **deckManager.js:** Handles deck operations like shuffling (Fisher-Yates algorithm) and dealing cards.
  - **gameState.js:** Manages the game state, including current turn, score, and locked sequences.
  - **uiRenderer.js:** Renders UI components using Tailwind CSS.
  - **fixitLogic.js:** Contains the logic for executing Fixit card moves and enforcing immediate turn termination.

- **Other Key Files:**
  - `package.json`: Manages dependencies such as Vite, Tailwind CSS, PostCSS, etc.
  - `vite.config.js`: Configures development and build settings.
  - `/public`: Contains static assets like images and icons for gameplay.

## Pseudocode Game Loop Implementation

Below is a highly abstracted description of the main events in the game loop.

Note that this is not functional code, but instead a conceptual outline meant to illustrate the game flow.

```plaintext

// Initialize game resources:
  - Create a 52-card play deck (with red backs) that is facedown.
  - Create a 10-card Fixit deck (with blue backs) where Fixit cards will be drawn face up.
  - Shuffle both decks using a Fisher-Yates algorithm.
  - From the Fixit deck, deal 2 cards face up (pre-dealt Fixit hand).
  - From the play deck, deal 5 cards to the player.
  - For web: set targetNumber = randomly generated number when the app starts.
  - For physical cards: targetNumber = sum(randomly drawn cards.
  - (Remember: targetNumber is the sum of five cards, with a range of 5 to 65.)
  - Initialize game state variables (e.g., currentTurn, score, target number, etc.).

// Main Game Loop:
WHILE gameIsRunning:
  - Render the current game state:
      - Display the player's hand, locked sequences, score, and remaining count of cards in the facedown play deck.
  - Prompt for player's input:
      - userInput = getUserInput()  // e.g., "playCard" or "playFixit"
  - Process the input:
      IF userInput is "playCard":
          - card = selectCardFromHand()        // Let the player choose a card
          - IF isValidMove(card):
                - updateGameStateWithCard(card)  // Integrate card into a sequence
                - log the event (card played)
          - ELSE:
                - notify the player of an invalid move (no state change)
      ELSE IF userInput is "playFixit":
          - IF fixitHand is not empty:
                - fixitCard = removeCardFromFixitHand()  // Pre-dealt Fixit card selected
                - reveal fixitCard and determine its action
                - applyFixitMove(fixitCard, targetSequence)  // Insertion, reorder, remove, retrieve
                - mark fixitCard as used
                - log the event and immediately terminate the current action phase
                - (Skip any remaining actions in this turn)
          - ELSE:
                - notify the player that no Fixit cards are available
  - Check for game end conditions:
      - IF (play deck is empty AND player's hand is empty) OR win/loss criteria met:
              - set gameIsRunning to false
      - ELSE:
              - Prepare for the next turn:
                    - Optionally, draw additional cards if the hand is below a threshold
                    - Increment currentTurn and reset temporary phase values

// End loop when gameIsRunning is false.
```

## Gameplay Notes

- **Game Flow:** Players begin by shuffling the decks and dealing cards. During each turn, they choose to play a normal card or a Fixit card. Playing a Fixit card immediately ends the turn.
- **Winning Conditions:** The game continues until the play deck and hand are empty, or a specific target number is reached as per the game rules.
- **Persistence:** Game state is saved and restored using localStorage, allowing players to resume their game between sessions.

## Next Steps

- Refine detailed game rules and scoring mechanisms.
- Implement unit tests to ensure randomness during shuffle and proper state updates.
- Finalize UI design using Tailwind CSS.
