---
layout: post
title: "NLP classification with spacy"
date: 2022-02-01 17:30:00 +0200
categories: python
---


The recommended way to run spacy training is from command line
```
python -m spacy train config.cfg --output ./output --paths.train ./train.spacy --paths.dev ./dev.spacy
```
The [spacy documentation](https://spacy.io/usage/training) shows how to prepare `config.cfg` and how to prepare datasets for a NER task.
However it doesn't describe how to prepare the datasets for a (multiclass) classification task, so this is how to do it:
```
import spacy
from spacy.tokens import DocBin

train_data = [('some text', {'category_1': 1, 'category_2': 0}),
              ('other txt', {'category_1': 0, 'category 2': 1})]

nlp = spacy.blank("en")  # or the appropriate language
db = DocBin()
for text, label in train_data:
    doc = nlp.make_doc(text)
    doc.cats = label
    db.add(doc)
db.to_disk('path/to/train.spacy')
```


Some useful links:
- <https://spacy.io/usage/training>
- <https://towardsdatascience.com/sarcasm-text-classification-using-spacy-in-python-7cd39074f32e>
