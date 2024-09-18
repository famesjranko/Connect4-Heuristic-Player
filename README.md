# Connect4-Heuristic-Player

A Lisp-based Connect-4 game enhanced with a custom heuristic AI. This project implements a strategic heuristic that evaluates board states, enabling the AI to play both offensively and defensively. Includes minimax algorithm integration for optimal gameplay.

## Heuristic Overview

This project is built around a heuristic AI that evaluates Connect-4 board states, allowing the AI to play both offensively and defensively. The AI utilizes the minimax algorithm and custom heuristic strategies to make optimal moves based on current and future board states.

### Heuristic Design

I approached this heuristic in two key ways:

1. **Positional Evaluation**: I assigned values to each board state based on whether a move contributes to a possible win or blocks an opponent's potential win. Weighting current moves more heavily than future moves proved effective for both defensive and offensive play.

2. **Strategy Value Map**: Given that Connect-4 is a solved game, I implemented a value map overlay for the board. Each position was assigned a value based on its contribution to the optimal game outcome. Additionally, a diagonal strategy was added to give weight to potential diagonal win states.

### Defensive Weighting

The heuristic is weighted toward defensive play at a shallow search depth. I optimized the heuristic to defend against losses rather than pursuing unwinnable victories at lower depths. This allowed the AI to maintain a balance between offense and defense.

### Depth and Tree Search in Minimax

In the minimax algorithm, **search depth** refers to how many moves ahead the AI evaluates in the game tree. Each level in the tree represents a possible board state resulting from a move by the current player or their opponent. A greater depth means the AI can "look ahead" further, evaluating more future moves and making better decisions.

- **Depth 1**: The AI evaluates only its immediate next move.
- **Depth 2**: The AI considers both its next move and the opponent's immediate response.
- **Depth 3**: The AI evaluates two of its own moves and two responses from the opponent, and so on.

Increasing the depth improves the AI's ability to predict future outcomes, but it also increases the computational complexity. In this Connect-4 implementation, I tested the AI across depths of 1 to 4, and it performed competitively even at shallow depths.

### Testing and Results

I tested the heuristic across search depths of 1 to 4, playing multiple games at each depth. The AI was able to beat me consistently, even at depth 1, demonstrating that the heuristic works effectively regardless of the search depth. 

Interestingly, through testing, I found my own Connect-4 skills improving. However, the AI still managed to outperform me at every depth. With further fine-tuning of the weight factors and additional testing against stronger players, this heuristic could be further refined to improve its overall gameplay.

Here are the final game states from the tests:

```bash
# search depth=1     # search depth=2 
# heuristic win:     # heuristic win: 
Final position:	   Final position:	
---------------	   ---------------	
|O|X|O|O|X|O|O|	   |O|X| |O| |X|O|	
---------------	   ---------------	
|X|O|X|O|X|X|X|	   |X|X| |O| |O|O|	
---------------	   ---------------	
|O|O|O|X|O|O|O|	   |X|X| |X| |X|X|		
---------------	   ---------------	
|X|X|X|O|O|X|X|	   |O|O| |O|O|O|O|	
---------------	   ---------------	
|X|O|X|O|X|O|O|	   |O|X| |O|X|X|X|	
---------------	   ---------------	
|X|O|X|X|X|O|X|	   |X|O|X|X|O|O|X|	
---------------	   ---------------	
 0 1 2 3 4 5 6        0 1 2 3 4 5 6 
I win.               I win.		
121                  438		

# search depth=3     # search depth=4 
# heuristic win:     # heuristic win: 
Final position:	   Final position: 
---------------      --------------- 
|O|O|O|X| |O|O|	   | | | | | | | | 
---------------	   --------------- 
|X|X|X|O| |X|X|	   | | | | |O| | | 
---------------	   --------------- 
|O|O|X|O|O|X|X|	   | | |X|O|O| | | 
---------------	   --------------- 
|X|X|O|X|X|O|O|	   | |X|O|O|X| | | 
---------------	   ---------------	 
|O|O|X|O|O|X|O|	   | |O|X|X|O| | |	
---------------	   --------------- 
|X|X|O|X|X|X|O|	   |X|O|X|X|X|O| | 
---------------	   --------------- 
 0 1 2 3 4 5 6        0 1 2 3 4 5 6 
I win.               I win. 		
1775                 6038 		
```

## How to Run the Connect-4 Program

This project consists of three Lisp files:

1. **minimax.lisp**: Contains the Lisp code for the minimax algorithm used by the AI player.
2. **connect-4.lisp**: Contains the implementation of the Connect-4 game.
3. **heuristic.lisp**: Contains the heuristic function for the computer player.

### Prerequisites

You will need **CLISP** to run the program.

### Instructions

1. **Start the CLISP interpreter:**
   - If you're on a Debian-based system, you can start the interpreter by typing:
     ```
     $ clisp
     ```

2. **Load the minimax algorithm:**
   In the CLISP interpreter, load the `minimax.lisp` file:
   ```lisp
   (load "minimax.lisp")
   ```

3. **Load the Connect-4 game:**
   Load the `connect-4.lisp` file:
   ```lisp
   (load "connect-4.lisp")
   ```

4. **Load the heuristic file:**
   Load the `heuristic.lisp` file (this contains the heuristic for the AI):
   ```lisp
   (load "heuristic.lisp")
   ```

5. **Start the game:**
   Once the files are loaded, you can start playing Connect-4 by running:
   ```lisp
   (play)
   ```
