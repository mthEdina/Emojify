# Emojify

Eredeti adathalmaz: 
- https://www.kaggle.com/datasets/e0xextazy/pairs-comment-reply-from-reddit
- 4270191 input

train.csv: 80% az eredetiből
test.csv: 20% az eredetiből

tiny_test.csv: 1.000 input a test.csv-ből
tiny_train.csv: 10.000 input a train.csv-ből

---------------------------------------------------------------

predictions.csv: 
- kulcsszó-kiszedő algoritmus kimenete
- a tiny_test.csv-ben lévő szövegek kulcsszavait tartalmazza

- Dice-score a tiny_train.csv-n: 0.6788