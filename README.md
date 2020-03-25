# Magic the Gathering Deck Builder Framework
I wrote this class after playing around with [this](https://www.deckedbuilder.com/) app which provides a "stats" page about each deck file.

### Example Usage
Found a exmaple deck [here](https://www.channelfireball.com/all-strategy/articles/the-real-mono-black-devotion-modern/)
```python
from deck_builder import Deck
deck = Deck()

# Land
deck.add_card('Swamp', 20)

# Creatures
deck.add_card("Bloodghast", 4)
deck.add_card("Gatekeeper of Malakir", 4)
deck.add_card("Geralf's Messenger", 4)
deck.add_card("Gray Merchant of Asphodel", 4)
deck.add_card("Relentless Dead", 4)

# Spells
deck.add_card("Disfigure", 4)
deck.add_card("Dismember", 4)
deck.add_card("Go for the Throat", 4)
deck.add_card("Inquisition of Kozilek", 4)
deck.add_card("Thoughtseize", 4)

# Sideboard
deck.add_card("Pithing Needle", 4, to_sideboard=True)
deck.add_card("Smother", 4, to_sideboard=True)
deck.add_card("Whip of Erebos", 4, to_sideboard=True)
deck.add_card("Surgical Extraction", 4, to_sideboard=True)

print("Deck size      : {}".format(len(deck.cards)))
print("Side board size: {}".format(len(deck.side_board)))
Deck size      : 60
Side board size: 16

# Import and export usage
export = deck.export_json()
new_deck = Deck(export_json=export)

# Simple stats
cards = deck.get_non_land_cards()

print("Mean CMC: {}".format(cards['cmc'].mean()))
print("Median CMC: {}".format(cards['cmc'].median()))
print("Standard Deviation CMC: {}".format(cards['cmc'].std()))
print("Max  CMC: {}".format(cards['cmc'].max()))
print("Min  CMC: {}".format(cards['cmc'].min()))
Mean CMC: 3.851063829787234
Median CMC: 4.0
Standard Deviation CMC: 2.340370868085871
Max  CMC: 9
Min  CMC: 1

# Sample graphs with matplot
cards['cmc'].plot.bar().xaxis.set_major_locator(plt.NullLocator())
deck.cards.explode('types').groupby('types').count().plot.pie(y='number')
```
