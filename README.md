# Emojify

one_text.ipynb notebook segítségével kipróbálható tetszőleges szövegre az emojify 

-----------------------------------------------------------
Eredeti adathalmaz: 
- https://www.kaggle.com/datasets/e0xextazy/pairs-comment-reply-from-reddit
- 4270191 input


- train.csv: 80% az eredetiből
- test.csv: 20% az eredetiből


- tiny_test.csv: 1.000 input a test.csv-ből
- tiny_train.csv: 10.000 input a train.csv-ből

---------------------------------------------------------------

predictions.csv: 
- kulcsszó-kiszedő algoritmus kimenete
- a tiny_test.csv-ben lévő szövegek kulcsszavait tartalmazza
- Dice-score a tiny_train.csv-n (keyphraseness módszerrel): 0.6788

---------------------------------------------------------------
### Emojik mapelése


tweets_with_emojis_initial.csv: 
- emojik párosítása a kulcsszavakhoz a tiny_test.csv-ből

---------------------------------------------------------------

tweets_with_emojis_predicted.csv: 
- emojik párosítása a kiválogatott kulcsszavakhoz a predictions.csv-ből

---------------------------------------------------------------

A kimeneti képeken: 
- a legtöbbször előforduló kulcsszavakból generált szófelhő
látható;
- a párosítás során leggyakrabban használt emojik eloszlása található.

---------------------------------------------------------------

A mapelés folyamata: 

1. **Adatbetöltés:**  
   Kétféle formátum:
   - `initial` mód: súlyozott kulcsszavak (`{'szó': súly}`).
   - `predicted` mód: egyszerű kulcsszólista (`['szó1', 'szó2']`).

2. **Emoji-k előkészítése:**  
   Az összes Unicode emoji és annak szöveges leírása beágyazásra kerül a `SentenceTransformer` modellel.

3. **Kulcsszavak → Emojik párosítása:**  
   Minden kulcsszóhoz megtalálja a leginkább hasonló jelentésű emojit szövegalapú hasonlóság alapján.

4. **Eredmények mentése:**  
   Az output fájl tartalmazza az `id`, `tweet szöveg`, és a hozzárendelt `emojik` oszlopokat.

5. **Vizualizáció:**  
   - Emoji gyakorisági diagram (top 15 emoji)
   - Kulcsszavas szófelhő

6. **Használat:**
    ```bash
    pip install emoji sentence-transformers wordcloud tqdm seaborn

    main(mode="initial")   # ha súlyozott kulcsszavak
    main(mode="predicted") # ha listás kulcsszavak

---------------------------------------------------------------

### Emojik összehasonlítása

Összehasonlítjuk a két fájl esetén generált emojik milyen arányban egyeznek.
Az összehasonlítás során soronként:
- Az emojik halmazként kerülnek összevetésre
- Kiszámítjuk:
  - **Precision** – mennyi a találatok aránya a predikcióban
  - **Recall** – mennyi valódi emoji került eltalálásra
  - **F1-score** – a kettő harmonikus átlaga
  - **Exact match** – pontos egyezés esetén 1

A végső eredmény tartalmazza az összehasonlítás részletes eredményeit soronként:
- `id`
- `true_emojis`
- `predicted_emojis`
- `precision`, `recall`, `f1_score`
- `exact_match` (0 vagy 1)


---------------------------------------------------------------