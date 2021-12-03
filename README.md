# Assignment-10.1

from ntpath import join
import random

# creating a single card class
class Card:
    # instance variable to assign card titles
    _card_titles = {
        1:"Ace",
        2:"Two",
        3:"Three",
        4:"Four",
        5:"Five",
        6:"Six",
        7:"Seven",
        8:"Eight",
        9:"Nine",
        10:"Ten",
        11:"Jack",
        12:"Queen",
        13:"King"
    }

    def __init__(self, suit, number):
        self.suit = suit
        self.number = number
        self.title = self._card_titles[number]
    
    def get_card_name(self):
        return f"{self.title} of {self.suit}"


# creating a deck of cards class
class Deck:

    # each deck will have a unique identifier
    def __init__(self, identifier):
        self.identifier = identifier
        current_deck = []
        for suit in ["Spades", "Clubs", "Hearts", "Diamonds"]:
            for num in range(1,14):
                current_deck.append(Card(suit, num))
        self.current_deck = current_deck

    # gets the ID of the deck
    def get_id(self):
        return self.identifier

    # making the len method return the length of the current deck
    def __len__(self):
        return len(self.current_deck)

    # draws a card from the remaining deck
    def get_rand_card(self, with_replace = False):

        rand_index = random.randint(1,len(self))

        if not with_replace:
            return self.current_deck.pop(rand_index)
        else:
            return self.current_deck[rand_index]
            
    # gets the top card of the deck
    def get_top_card(self, with_replace = False):
        top_card = self.current_deck[0]
        self.current_deck = self.current_deck[1:]
        return top_card

    # sets the top card of the deck
    def set_top_card(self, card):
        self.current_deck.insert(0, card)
    
    # removes card from the deck
    def remove_card(self, card):
        self.current_deck = self.current_deck.remove(card)

    # reorders the cards to their original order while removing the cards that are missing
    def set_in_order(self):
        new_deck = Deck()
        # remove missing cards
        for card in new_deck.current_deck:
            if card not in self.current_deck:
                new_deck.remove_card(card)

        self.current_deck = new_deck.current_deck


    
def demo_program():
    print("Creating a new deck of cards")
    demo_deck = Deck("Demonstration Deck")
    print("We created the following:")
    print(demo_deck.get_id())
    print("Drawing the top card")
    print(demo_deck.get_top_card().get_card_name())
    print("Drawing the next top card")
    print(demo_deck.get_top_card().get_card_name())
    print("Setting the top card then drawing it")
    demo_deck.set_top_card(Card("Clubs", 8))
    print(demo_deck.get_top_card().get_card_name())
    print("Drawing some random cards")
    print(demo_deck.get_rand_card().get_card_name())
    print(demo_deck.get_rand_card().get_card_name())
    print(demo_deck.get_rand_card().get_card_name())
    print(demo_deck.get_rand_card().get_card_name())
    print("Now our deck is of length:")
    print(len(demo_deck))
    print("Reordering the deck to its original state")
    demo_deck.set_in_order()
    print("All done!")
    return(demo_deck)
