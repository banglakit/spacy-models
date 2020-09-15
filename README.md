<a href="https://github.com/banglakit"><img src="https://avatars3.githubusercontent.com/u/20180620?s=125&amp;v=4" width="125" height="125" align="right" /></a>

# Bangla (Bengali / বাংলা) spaCy models
This repository contains [releases](https://github.com/banglakit/spacy-models/releases)
of Bengali/Bangla language models for the [spaCy](https://github.com/explosion/spaCy) NLP library.

> **⚠️ Important note:** Because the models can be very large and consist mostly
> of binary data, we can't simply provide them as files in a GitHub repository.
> Instead, we've opted for adding them to
> [releases](https://github.com/banglakit/spacy-models/releases) as `.tar.gz`
> files. This allows us to still maintain a public release history.

## Releases
### spaCy v2.x

| Date | Model | Version | Dep | Ent | Vec | Size | License | | |
| --- | --- | --- | :---: | :---: | :---: | ---: | --- | --- | --- |
| `2018-08-27` | `bn_core_news_sm` | 2.0.0 | ✘ | ✔ | ✔ | 290 MB | MIT | [![][i]][i-bn_core_news_sm-0.1.0] | [![][dl]][bn_core_news_sm-0.1.0]

[bn_core_news_sm-0.1.0]: https://github.com/banglakit/spacy-models/releases/download/bn_core_news_sm-0.1.0/bn_core_news_sm-0.1.0.tar.gz

[i-bn_core_news_sm-0.1.0]: https://github.com/banglakit/spacy-models/releases/bn_core_news_sm-0.1.0

[dl]: http://i.imgur.com/gQvPgr0.png
[i]: http://i.imgur.com/OpLOcKn.png

## Model naming conventions

In general, spaCy expects all model packages to follow the naming convention of
`[lang]_[name]`. For our models, we also chose to divide the name into three
components:

* **type**: Model capabilities (e.g. `core` for general-purpose model with vocabulary, syntax, entities and word vectors, or `depent` for only vocab, syntax and entities)
* **genre**: Type of text the model is trained on (e.g. `web` for web text, `news` for news text)
* **size**: Model size indicator (`sm`, `md` or `lg`)

For example, `en_depent_web_md` is a medium-sized English model trained on
written web text (blogs, news, comments), that includes vocabulary, syntax and
entities.

### Model versioning

Additionally, the model versioning reflects both the compatibility with spaCy,
as well as the major and minor model version. A model version `a.b.c`
translates to:

* `a`: **spaCy major version**. For example, `2` for spaCy v2.x.
* `b`: **Model major version.** Models with a different major version can't be loaded by the same code. For example, changing the width of the model, adding hidden layers or changing the activation changes the model major version.
* `c`: **Model minor version.** Same model structure, but different parameter values, e.g. from being trained on different data, for different numbers of iterations, etc.

For a detailed compatibility overview, see the [`compatibility.json`](compatibility.json).
This is also the source of spaCy's internal compatibility check, performed when you
run the `download` command.

## Downloading models

To increase transparency and make it easier to use spaCy with your own models,
all data is now available as direct downloads, organised in
[individual releases](https://github.com/banglakit/spacy-models/releases). spaCy
1.7 also supports installing and loading models as **Python packages**. You can
now choose how and where you want to keep the data files, and set up "shortcut
links" to load models by name from within spaCy. For more info on this, see the
new [models documentation](https://spacy.io/usage/models).

```bash
# pip install .tar.gz archive from path or URL
pip install /Users/you/bn_core_news_sm-2.0.0.tar.gz
pip install https://github.com/banglakit/spacy-models/releases/download/bn_core_news_sm-2.0.0/en_core_web_sm-2.0.0.tar.gz

# set up shortcut link to load installed package as "en_default"
python -m spacy link en_core_web_sm en_default

# set up shortcut link to load local model as "my_amazing_model"
python -m spacy link /Users/you/data my_amazing_model
```

## Loading and using models

`import` it directly and then call its `load()` method with no arguments.

> **⚠️ Important note:** Because the the Bangla models use a custom `SentenceSegmenter`,
> it is dynamically loaded with `model.load()`. Thus the sentence segmenter will
> not work if you load with `spacy.load('modelname')`.

```python
import spacy
import bn_core_news_sm

nlp = bn_core_news_sm.load()
doc = nlp(u'আমি বাংলায় গান গাই। তুমি কি গাও?')
```

## Manual download and installation

In some cases, you might prefer downloading the data manually, for example to
place it into a custom directory. You can download the model via your browser from
the [latest releases](https://github.com/banglakit/spacy-models/releases), or
configure your own download script using the URL of the archive file. The archive
consists of a model directory that contains another directory with the model data.

```yaml
└── bn_core_news_sm-2.0.0.tar.gz       # downloaded archive
    ├── meta.json                      # model meta data
    ├── setup.py                       # setup file for pip installation
    └── bn_core_news_sm                # model directory
        ├── __init__.py                # init for pip installation
        ├── meta.json                  # model meta data
        └── bn_core_news_sm-2.0.0      # model data
```

You can place the model data directory anywhere on your local file system. To
use it with spaCy, simply assign it a name by createing a shortcut link for the data directory.

**📖 For more info and examples, check out the [models documentation](https://spacy.io/usage/models).**


## Issues and bug reports

To report an issue with a model, please open an issue on the
[spaCy issue tracker](https://github.com/banglakit/spacy-models).
Please note that no model is perfect. Because models are statistical, their
expected behaviour **will always include some errors**. However, particular
errors can indicate deeper issues with the training feature extraction or
optimisation code. If you come across patterns in the model's performance that
seem suspicious, please do file a report.
