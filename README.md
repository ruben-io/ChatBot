*Features*
- corenlp.py -- A file that interfaces with CoreNLP through NLTK and attempts to use a corenlp.pth file to find your local install.
- utils.py -- Contains numerous utility functions for working with natural language, including wrappers for CoreNLP's PSG/NER/OpenIE engine. 
It enables finding nodes in a parse tree, unicode processing, parse tree and text pre/postprocessing, extremely basic conjugation, and finding 
Subject/Verb/Object relations in arbitrary text.
- igdb_scrape.py -- What I used to scrape IGDB to construct games.sqlite3. The client_id and client_secret we used have been invalidated. 
It does not populate the arbitrary fact table; that's done by the bot's preprocess_facts() function.
- bot.py -- The "meat" of the project: provides a loop that interfaces with the user. Use bot.preprocess_facts() to generate arbitrary 
subject/verb/object relations to populate the general information table in the games.sqlite database (this takes a LONG time, often several hours, 
so I packaged out database with most of the preprocessing done). It also provides bot.loop(), which interfaces with the user and lets them ask 
questions and state facts. The process() function takes a single line and gets its PSG, from which it figures out if it's a statement 
(which goes to process_statement, for "tell me something," "forget about me," or any arbitrary fact) or a question (which it processes directly, 
first looking for common ways to ask about rating, story, description, or franchise, then it tries to find arbitrary "fact" relations about with the 
find_relations_like() function). It does another few things, like using PERSON/LOCATION NER to try to find game titles.
