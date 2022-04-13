# Day-11---Capston-Project-100-days-of-python-
Blackjack Program
############### Blackjack Project #####################

############### Our Blackjack House Rules #####################

## The deck is unlimited in size. 
## There are no jokers. 
## The Jack/Queen/King all count as 10.
## The the Ace can count as 11 or 1.
## Use the following list as the deck of cards:
## cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
## The cards in the list have equal probability of being drawn.
## Cards are not removed from the deck as they are drawn.
## The computer is the dealer.


import random
from art import logo
from replit import clear


def deal_card():
    cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
    card = random.choice(cards)
    return card
    

def calculate_score(cards):
    if sum(cards) == 21 and len(cards) == 2:
        return 0
    if 11 in cards and sum(cards) > 21:
        cards.remove(11)
        cards.append(1)
    return sum(cards)
        
def compare(user_score, computer_score):
    if user_score > 21 and computer_score > 21:
        return "You went over. You lose 😤"
    
    
    if user_score == computer_score:
        return "Draw 🙃"
    elif computer_score == 0:
        return "Lose, opponent has Blackjack 😱"
    elif user_score == 0:
        return "Win with a Blackjack 😎"
    elif user_score > 21:
        return "You went over. You lose 😭"
    elif computer_score > 21:
        return "Opponent went over. You win 😁"
    elif user_score > computer_score:
        return "You win 😃"
    else:
        return "You lose 😤"
def play_game():
    print(logo)
    user_cards = []
    computer_cards = []
    game_over = False
    
    for i in range(2):
        user_cards.append(deal_card())
        computer_cards.append(deal_card())
        
    while not game_over:
        user_score = calculate_score(user_cards)
        computer_score = calculate_score(computer_cards)

        print(f"Your cards: {user_cards}, your current score {user_score}")
        print(f"computer first card: {computer_cards[0]}")
        
        if computer_score == 0 or user_score == 0 or user_score > 21:
            game_over = True
        else:
            another_card = input("Do you want another card? Type 'y' for yes and 'n' for no: ")
            if another_card == "y":
                user_cards.append(deal_card())
            else:
                game_over = True
    while computer_score != 0 and computer_score < 17:
        computer_cards.append(deal_card())
        computer_score = calculate_score(computer_cards)
    else:
        print(f"Your cards: {user_cards}, your final score {user_score}")
        print(f"Computer cards: {computer_cards}, computer final score {computer_score}")
        print(compare(user_score, computer_score))
def play_again():
    play_again = input("Would you like to play a game of blackjack? type 'y' for yes and 'n' for no: ")
    return play_again
while play_again() == "y":
    clear()
    play_game()
