===============
Post Statistics
===============

``Post Stats`` is a plugin for `Pelican <http://docs.getpelican.com/>`_,
a static site generator written in Python.

``Post Stats`` calculates various statistics about a post and store them in
an article.stats dictionary:

- ``wc``: how many words
- ``read_mins``: how many minutes would it take to read this article, based
   on 250 wpm
   (`source <http://en.wikipedia.org/wiki/Words_per_minute#Reading_and_comprehension>`_)
- ``word_counts``: frquency count of all the words in the article; can be
  used for tag/word clouds
- ``fi``: Flesch-kincaid Index/ Reading Ease
  (`more info <http://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests>`_)
- ``fk``: Flesch-kincaid Grade Level


Installation
============

The easiest way to install ``Post Stats`` is through the use of pip. This
will also install the required dependencies automatically.

.. code-block:: sh

  pip install minchin.pelican.plugins.post_stats

Then, in your ``pelicanconf.py`` file, add ``Post Stats`` to your list of
plugins:

.. code-block:: python

  PLUGINS = [
              # ...
              'minchin.pelican.plugins.post_stats',
              # ...
            ]

You may also need to configure your template to make use of the statistics
generated.


Requirements
============

``Post Stats`` depends on (and is really only useful with) Pelican. The
plugin also requries Beautiful Soup 4 to process your content. If the plugin
is installed from pip, these will automatically be installed. These can also
be manually installed with pip:

.. code-block:: sh

   pip install pelican
   pip install beautifulsoup4



Configuration and Usage
=======================

This plugin calculates various statistics about a post and store them in
an article.stats dictionary.

Example:

.. code-block:: python

    {
        'wc': 2760,
        'fi': '65.94',
        'fk': '7.65',
        'word_counts': Counter({u'to': 98, u'a': 90, u'the': 83, u'of': 50, ...}),
        'read_mins': 12
    }

This allows you to output these values in your templates, like this, for example:

.. code-block:: html+jinja

	<p title="~{{ article.stats['wc'] }} words">~{{ article.stats['read_mins'] }} min read</p>
	<ul>
	    <li>Flesch-kincaid Index/ Reading Ease: {{ article.stats['fi'] }}</li>
	    <li>Flesch-kincaid Grade Level: {{ article.stats['fk'] }}</li>
	</ul>

The ``word_counts`` variable is a python ``Counter`` dictionary and looks something like this, with each unique word and it's frequency:

.. code-block:: python

	Counter({u'to': 98, u'a': 90, u'the': 83, u'of': 50, u'karma': 50, .....

and can be used to create a tag/word cloud for a post.

There are not user-configurable settings.


Credits
=======

Original plugin from the `Pelican-Plugins repo
<https://github.com/getpelican/pelican-plugins>`_.


License
=======

The plugin code is assumed to be under the AGPLv3 license (this is the
license of the Pelican-Plugins repo).

