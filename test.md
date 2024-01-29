---
title: "test"
order: 4
in_menu: true
---
link(href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;500&display=swap", rel="stylesheet")

// secret codes
- var codes = ["6543", "1324", "4135", "5614"];
- var rounds = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
- var numrounds = 10;
- var slots = [1, 2, 3, 4];

form
  label#info(for="hideInit") i
  input(id="color-blind", type="checkbox")
  label#color-blind-label(for="color-blind") Add letters
  // rounds
  div#board
    h1#mastermind MASTERMIND
    each val in codes
      input(type="radio", tabindex=-1, value=val, name="code", id="code-"+val, checked=(val === "6543"))

    each round in rounds
      input(type="checkbox", tabindex=-1, id="completed-"+round, class="completed")
      input(type="radio", tabindex=-1, id="round-"+round, name="round")
      each val in slots
        each color in [1,2,3,4,5,6]
          input(type="radio", tabindex=-1, value=color, name="slot-"+val+"-round-"+round, id="slot-"+val+"-round-"+round+"-color-"+color)
      div(class="round-container round-"+round)
        label(for="completed-"+round) 
          span NEXT
        each num in [1,2,3,4]
          a(href="#round-"+round+"-slot-"+num, tabindex=0, class="slot-circle slot-"+num+"-round-"+round+"-trigger")
        div(class="valid valid-"+round)
          each num in [1,2,3,4]
            div(class="correct-"+num)
          each num in [1,2,3,4]
            div(class="partial-"+num)
          each num in [1,2,3,4]
            div(class="empty-"+num)

    input(type="radio", value=val, name="round", id="round-"+(numrounds+1))
    
    input(type="checkbox", id="hideInit")
    #init.popup
      div
        h1 Let's play CSS Mastermind!
        p 
          |  
          a(href="https://en.wikipedia.org/wiki/Mastermind_(board_game)",target="_blank") Mastermind 
          | is a challenging code-breaking game. There are 6 colors and a 4-length code to decipher. Can you break the code? 
        p Select the colors for each code peg by clicking in an active slot. When you are ready, click on the "Next" button on the left side of the active round.
        p The results will be displayed using key pegs on the right. A black key peg indicates that a color is in the right place, while a white key peg indicates that a color is present but not in the right place.
        p.games Pick a game to play:
        p.games
          each val in codes
            label(class="close", for="code-"+val, class="game-selector") Game
        div#start-button
          label(for="round-1", class="green-button") START GAME
        label.close(for="hideInit") Close
          
    div.lost.popup 
      div 
        h2 Game Over!
        p Oh, no! You reach the end of the game before cracking the code... Click on the button to try again!
        div
          input(type="reset", value="Play again", class="green-button")
    div.won.popup
      div 
        h2 Congratulations! You won!
        p Yay! You are amazing and cracked the code successfully! Click on the button below to restart the game.
        div
          input(type="reset", value="Play again", class="green-button")
          
    div#confetti
      - n = 1;
      while n < 100
        div(class="confetti confetti-"+n)
        - n++

    each round in rounds
      div(id="transition-"+round, class="popup transition")
        div
          h2 Not there yet!
          p Review the hints on the right side and make some changes in the next round.
          div
            label(for="round-"+(round+1), class="close") Next round!
      each num in [1,2,3,4]
        div(id="round-"+round+"-slot-"+num, class="popup") 
          div 
            h2 Round #{round} Slot #{num}
            div.color-labels
              each color in [1,2,3,4,5,6]
                label(for="slot-"+num+"-round-"+round+"-color-"+color,tabindex=1)
            a(href="#", class="close") Close 