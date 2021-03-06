# Deep Referendum

## Synopsis

This is the UCL IRDM 2016 group project for

## Members

1. Jonny Manfield
1. Vlad Kolesnyk
1. Gabriel Bila

## Installation

### BrexitTcf 

BrexitTcf is responsible for downloading previous #Brexit tweets. It uses the Twitter search API to download tweets between 2 dates.

BrexitTcf is written in Scala and uses Gradle for dependency management and build automation.

To run BrexitTcf search API, make sure you have the following installed first:

1. JDK 8 (make sure JAVA_HOME points to the right jdk directory)
1. Scala (latest version)
1. Gradle (latest version)

From the BrexitTcf directory, run ```gradle installDist``` to generate the project JARs and launch scripts. They will be placed under ```BrexitTcf/build/install/BrexitTcf```

Then, to launch the Brexit search, ```cd``` to ```build/install/BrexitTcf/bin``` and run ```./BrexitTcf <start-date> <end-date>```. For example ```./BrexitTcf 2016-04-10 2016-04-12```.

This will query the Twitter API for #Brexit-related tweets. The tweets will be output in the current directory. One separate JSON file will be created for each day.

This only works for tweets 1 week old or less. Twitter API doesn't return historical tweets older than this.

## Reference

<!--List all Python scripts and other components here. Use alphabetical order to keep things nice and clean.--> 

* ```app/cooccurence.py```: - Python script to built a co-occurence matrix of all the words in a tweet which can return the most common words associated with a tweet

* ```app/FrequencyAnalysis.ipynb``` - An iPython notebook covering the analysis of frequency distributions within the Brexit dataset

* ```app/geo.py``` - Generates tweet coordinates into ```geo_data.json```, the file used by ```map.html``` for visualising tweets over the map of the UK.

* ```app/map.html``` - Displays tweet heat map over the UK: blue represents tweets for staying in the EU, red represents tweets for leaving the EU. Selecting 'Overlap heatmaps' plots both 
'leave' and 'stay' heat maps on top of each other. Blue will then represent majority pro-stay areas, red - majority pro-leave, and purple - highly-contested areas. 

   First, you need to generate data for the heat maps. To do so, run ```python geo.py``` first.

* ```app/location_coord_dict.py``` - Assigns geolocation to tweets based on their ```user.location``` value. Queries OSM Nominatim to convert the user's address to a pair of coordinates.
  The output is a dictionary in the format ```{address -> [lat, long]}```. This dictionary is stored in ```app/location_dict.json```

* ```app/reprocess.py``` - Function to remove extraenous HTML or special characters via Regex

* ```app/sentiment.py``` - Python script to calculate sentiment analysis via unsupervised "Semantic Orientation"

* ```app/SentimentClassification.ipynb```  - iPython notebook covering the subjectivity and sentiment classification steps neccessary to convert a tweet to a resultant vote for the UK EU referendum

* ```app/stream.py``` - __TCF Streaming API__. Python scripts for listening to the Twitter Streaming API for new tweets related to the #Brexit track

* ```app/vis.py``` - Function to plot the occurence of the word 'stay' or 'leave' in a tweet within a 5 minute resample

* ```BrexitTcf``` __TCF Search API__. See the corresponding __Installation__ section on how to install and run.

*  ```./sentiment_tf/run_tf.sh``` - script to run training loop; you can set your own parameters, folders, hook interations
*  ```./sentiment_tf/decode_tf.sh``` - script to run load sentiment classifier from the model genearated during training (by default in /data folder)
*  ```tensorboard --logdir=${PWD}``` - to visualise events during training, run tensorboard inside the folder where events file is stored (e.g. /data)

