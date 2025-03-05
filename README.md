Customer Greeklish Token Filter for ElasticSearch 7.17.9
========================================

Versions
--------

SkroutzGreekStemmer Plugin | ElasticSearch | Branch
---------------------------|---------------|--------|
7.7.0.2                    | 7.17.9        | main   |


Local Setup
-----------
1) Build the Project: Run the following Maven command to clean and install the project:
   ```mvn clean install```

2) Package the Plugin: Build the plugin package with the following Maven command:
   ```mvn package```

3) Create the Plugin Zip: Create a .zip file containing the JAR and the plugin-descriptor.properties file. Ensure both files are included in the archive.

4) Install the Plugin: Install the plugin by executing the following command:
   ```/usr/share/elasticsearch/bin/elasticsearch-plugin install file:<path-to-file>/plugin.zip```
   Restart Elasticsearch: After the plugin is installed, restart the Elasticsearch 7.17.9 instance to load the SkroutzGreekStemmer plugin.

Note: The plugin.zip file already exists in the plugin/ folder.


Installation
-------------

To list all plugins in current installation:

    sudo bin/elasticsearch-plugin list

In order to install the latest version of the plugin run:

    sudo bin/elasticsearch-plugin install gr.skroutz:elasticsearch-analysis-greeklish:7.7.0.1

In order to install version 5.4.2 of the plugin run:

    sudo bin/elasticsearch-plugin install gr.skroutz:elasticsearch-analysis-greeklish:5.4.2.1

In order to install version 2.4.4 of the plugin, simply run:

    sudo bin/plugin install gr.skroutz/elasticsearch-analysis-greeklish/2.4.4.1

In order to install the plugin for versions prior to 1.5.x, run:

    sudo bin/plugin -install gr.skroutz/elasticsearch-analysis-greeklish/0.10

To remove a plugin (5.x.x/7.x.x):

    sudo bin/elasticsearch-plugin remove <plugin_name>

Expansions
----------

There are more than one combinations of latin characters that can substitute
each character of the greek alphabet. So, a greek token is expanded to as many
greeklish tokens as the the combinations of the latin characters for each
greek character of a token and in some cases this produces an enormous number
of expansions. In order to prevent this from happening, a threshold of the max
expansions is set.  The default value is 20.

However, a threshold of the max expansions can be set in the elasticsearch.yml
When this threshold is reached the remaining characters are substitute with
the most common variant of the greek character.

Example usage:

	index:
	  analysis:
	    filter:
	      greeklish_analysis:
	        type: greeklish
	        max_expansions: 15

Generation of Greek Word Variations
-----------------------------------

It is difficult to distinguish a greeklish word from an english one during a
query. So, if we wanted to stem the greeklish word in order to have the same
results for the different forms of this word, we should apply a stemmer in
both the greeklish and english words. In order to avoid that, the 0.7 version
of the plugin comes with a reverse stemmer for greek words, which produces the
different forms of the a greek word (from singular to plural and vice versa)
in order to produce their greeklish version.

Now the greeklish word converter has two phases. The first phase produces the
diffent forms of a greek word based on some grammar rules, and the second
phase produces the greeklish version of each of theses greek words.

This functionality is enabled by default. But, it can be disabled by setting
greek\_variants variable in the elasticsearch configuration file.

Example usage:

	index:
	  analysis:
	    filter:
	      greeklish_analysis:
	        type: greeklish
	        max_expansions: 15
	        greek_variants: false

Warning
-------

This filter acts only on greek lowercase characters and for this reason it
should be applied after greek lowercase filter.
# elasticsearch-analysis-greeklish
