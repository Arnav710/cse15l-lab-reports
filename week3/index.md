# Researching Commands

---

In this lab report, we would be looking at the various command-line options that are offered in conjuntion with the `grep` command. This command is used to search for patterns in a single file or a collection of various files. It has various options associated with it as well, whichw we would be going over. The following are 4 of them:

* `-i` : ignore case

* `-r` : recursive search

* `-c` : count matching lines

* `-n` : line number

---

## `-i, --ignore-case`
Ignore case distinctions in patterns and input data, so that characters that differ only in case match each other. *(Source: MAN documentation)*

We will now be running a few commands to illustrate the use of this command.

### Example 1
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:507$ grep -i "DISEMBARKED" `find written_2 -name "*.txt"`
written_2/travel_guides/berlitz2/Bali-WhereToGo.txt:Before the days of flying, most visitors to Bali arrived in the north. The first Dutch military expeditions disembarked** near Singaraja, which became the island’s administrative capital and the colony’s chief port. Now, almost everyone arrives and stays in southern Bali, and only a fraction of them ever take a trip to the north coast, although the journey takes less than two hours by road.
written_2/travel_guides/berlitz2/Cuba-History.txt:When Christopher Columbus disembarked on eastern Cuba on 27 October 1492, he quickly penned a note exclaiming that the land was “the most lovely that eyes have ever seen.” Indian tribes including the Siboney from Central and South America had lived on the island since at least 1000 b.c.
written_2/travel_guides/berlitz2/Cuba-WhereToGo.txt:Baracoa really shines the week of 1 April, when heady street parties every night commemorate the date General Antonio Maceo disembarked at nearby Playa Duaba in 1895, marking the beginning of Cuba’s War of Independence.
```
<p align = "center">
<img width="785" alt="image" src="https://user-images.githubusercontent.com/63532613/218268050-edf66f12-fe45-4d96-ba4b-f1dab7167a09.png">
</p>
It can clearly be seen that despite the fact that we are searching for `DISEMBARKED` the results with mismatched case are also displayed (eg. `disembarked").


### Example 2
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:509$ grep -i "DecLarED IndePenDenCe" `find written_2 -name "*.txt"`
written_2/travel_guides/berlitz2/Algarve-History.txt:The war left Portugal further weakened, and in 1822 its major empire outpost, Brazil, declared independence. At the same time, a dispute over the crown continually raged between Pedro IV, the absentee monarch who preferred to reign as Emperor of Brazil rather than return to Portugal, and his brother Miguel. The power struggle, with strong overtones of absolutism versus liberalism, excited the interest and intervention of other powers. With British help, Pedro defeated Miguel off Cape St. Vincent in 1833, and his expeditionary force marched to Lisbon. Pedro took the throne, though armed struggle continued for months and the lingering bitterness long after that.
written_2/travel_guides/berlitz2/Athens-History.txt:As the nineteenth century commenced, a swell of nationalist fervor rose in the oppressed people of Greece. On 25 March 1821, Archbishop Germanos raised a new blue-and-white banner in Patras in the Peloponnese and declared independence, but it took 11 years and some formidable foreign help for the Greeks to win their war against Turkish rule. Athens changed hands more than once during the long struggle in which many English, Scots, Irish, and French fought alongside the Greeks. Byron, who popularized the cause abroad, died at Missolonghi in 1824 (of disease, not from fighting).
```
<p align = "center">
<img width="898" alt="image" src="https://user-images.githubusercontent.com/63532613/218268255-31988e2f-1116-48a9-ab75-56b4cb871850.png">
</p>
It can clearly be seen that despite the fact that we are searching for `DecLarED IndePenDenCe` the results with mismatched case are also displayed (eg. `declared independence").

In files, we can have title cased strings right after a line ends with a `.`. Moreover, it is likely that proper nouns would also start with an uppercase letter. This command can come in very handy in situations where we just want to look for a substring within a given file and we are not concerned with the case. In fact, in most situations, we might want to ignore the case while looking or substrings for most practical purposes.

---

## `-r, --recursive`
Read all files under each directory, recursively, following symbolic links only if they are on the command line. *(Source: MAN documentation)*

We will now be running a few commands to illustrate the use of this command.

### Example 1
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:510$ grep -r "Arawak Cay" written_2/ 
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:Head back to the main coast road and you will find two small cays lying immediately offshore. The first is 
Arawak Cay, home to the local fishing fleet. A number of colorful shacks line the approach road where you can buy conch and fried fish, always fresh and always delicious. Weekends can be busy with local families. Travel through Arawak Cay to reach Silver Cay, where there is a small resort with a pretty beach. Here you will find Crystal Cay, site of a marine park where you can take a close look at the undersea world without getting wet. A man-made coral reef has been created on the sea bottom and you can watch all the marine activity from an underwater observatory. The reef attracts many kinds of aquatic creatures that are free to come and go as they please. The observatory looks decidedly futuristic and can be seen quite clearly from the road as you travel along the coast. Other activities at Crystal Cay include a sea turtle environment, a touch pool where you can stroke a sting ray or pet a conch, and a snorkel trail, if you want to get into the water yourself.
```
<p align = "center">
<img width="899" alt="image" src="https://user-images.githubusercontent.com/63532613/218268584-234b9cdd-fc12-407c-b71f-5b77c4e838a9.png"></p>

### Example 2
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:511$ grep -r "Duchy of Warsaw" written_2/
written_2/travel_guides/berlitz2/Poland-History.txt:In desperation, Poland looked to Napoleon Bonaparte and Revolutionary France for assistance against its oppressors. Napoleon defeated the Prussian army in several key battles and established a semi-independent Duchy of Warsaw from 1807 to 1815. Napoleon gained an ally in Józef Poniatowski, a heralded military leader and the nephew of the last king. The 1812 Polish War re-established the Poland-Lithuania border, but Napoleon’s troops were crushed as they advanced on Moscow. Napoleon suffered a great defeat, but his ally Poniatowski refused to surrender, preferring to sacrifice himself and his troops. The suicidal mission became an important rallying cry for Poles during the remainder of the 19th century.
written_2/travel_guides/berlitz2/Poland-History.txt:The Congress of Vienna of 1815, with an aim to reorganize Europe after Napoleon’s escapades, did not re-establish an independent Poland. Rather, it again partitioned the country, placing the territory of the Duchy of Warsaw under the control of the Russian czar. For three decades, Kraków existed as an independent city-state, though it was again incorporated into the Austrian partition in 1846.
written_2/travel_guides/berlitz2/Poland-History.txt:The former Duchy of Warsaw, called the Congress Kingdom, enjoyed some autonomy and prosperity in the early 19th century. Poles launched a series of armed insurrections against its occupiers in 1830 and, after defeat, again in 1846 and 1863. The last rebellion counted on support from England and France that never arrived. Many Poles, fearful that an independent Poland would never again be realized, emigrated to France and then the United States during this period. Those who remained focused on preserving Polish language and culture if not the Polish state.
```
<p align = "center">
<img width="897" alt="image" src="https://user-images.githubusercontent.com/63532613/218268645-ead1449f-f8de-4afc-85cc-61503fcca27b.png"></p>


The `grep` command takes as it's command line arguments the substring to search for and the files within which we have to search for. In most cases we are dealing with complex directory structures, so listing out all files directly or even using the `*` notiation can become quite tedious. We cans solve this problem using the `find` command in conjuction with the `grep` command. However, the `-r` option presents a very convenient way to do so.

---

## `-c, --count`
Suppress normal output; instead print a count of matching lines for each input file. *(Source: MAN documentation)*

We will now be running a few commands to illustrate the use of this command.

### Example 1
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:514$ grep -c "Duchy of Warsaw" written_2/travel_guides/berlitz2/Poland-History.txt
3
```
### Example 2
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:518$ grep -c "the" written_2/travel_guides/berlitz2/Poland-History.txt
37
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:519$ grep -c -i "the" written_2/travel_guides/berlitz2/Poland-History.txt
40
```
It is interesting to see how the count of the string `the` changed when we use the `-i` option alongside the `-c` option. 

In many cases we want to look for the number of instances of a given word present in the file. This command can come in very handy using such scenarios. As shown in the second example of this section we can combine various options as well, giving us more flexibility and control over the tasks we may want to preform. 

---

## `-n, --line-number`
Prefix each line of output with the 1-based line number within its input file. *(Source: MAN documentation)*

We will now be running a few commands to illustrate the use of this command.

### Example 1
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:523$ grep -n "Prince Mieszko" written_2/travel_guides/berlitz2/Poland-History.txt
9:Prince Mieszko, leader of the Piast dynasty that ruled the Polonians, undertook the bold step to unify the Polanie (literally, “people of the fields”) and neighboring tribes. Mieszko adopted Christianity — most likely a savvy political move to place the new state on equal footing with nearby Christian states with ties to Rome — and married a Czech princess, Dobrava, in 965. His religious conversion won him the support of the papacy, and Mieszko effectively founded the Polish state the following year. By the end of the 10th century, he had united his tribal territory, Wielkopolska (Great Poland), with that of another tribe, Malopolska (Little Poland) — regional names that remain current today. Silesia, settled by a different tribe, would eventually become the third component of the nascent Polish state.
```

In this case, `Prince Mieszko` is present on the 9th line in the text file.  

### Example 2
```
[cs15lwi23aaq@ieng6-203]:skill-demo1-data:525$ grep -n "Stade de France" written_2/travel_guides/berlitz2/Paris-WhatToDo.txt
27:Rugby and football (soccer) can be seen at the spectacular new Stade de France on the northern outskirts at St-Denis or at Parc-des-Princes at the south end of the Bois de Boulogne. Nearby, tennis tournaments are held at Roland-Garros, or indoors over at the Palais Omnisports de Paris-Bercy, near the Gare de Lyon. Paris-Bercy is also the venue for everything from rock concerts to tango competitions, as well as cycle races and indoor windsurfing.
```
In this case, `Stade de France` is present on the 27th line in the text file.  

In many instances we may be concerned with finding where exactly in a substring is contained within the file. In such scenarios, the `-n` option can be used in order out figure out the line number so that we can look for it in the file with ease.

---
