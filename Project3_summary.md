### Project 3 summary

## Audio classification

Katrina Bykova

------

**Introduction**

​	 Home assistant AIs are becoming a normal part of our life. Our interaction with the AI is currently unidirectional. We tell the assistant what to do and it executes the command. To take the interaction with the home assistant to the next level we would need to enable the AI to "see" our activities and let it act upon them. In this project I am exploring a feasibility of using sound by home AI to sense the environment and identify human activities inside a home.

**Data**

*Google AudioSet*.  [A library of manually annotated sound recordings](https://research.google.com/audioset/download.html). The dataset contains 2,084,320 10-second sound recordings extracted from YouTube videos with 527 labeled sound events. The library is availbale in two different formats: as a list of YouTube video IDs and in a form pre-processed features derived from VGGish CNN model. The latter format was used in this project. 

*Self recorded audio events*. Recorded video clips of home-related activities were  converted into WAV sound files. The sound files were then used to extract embeddings for classification by developed models.

**Results**

​	10 sound classes describing home related activities were selected from the google AudioSet:

| Cooking/cleanin | Entertainment | Moving around |
| --------------- | ------------- | ------------- |
| water           | music         | footsteps     |
| microwave       | speech        | opening doors |
| blender         | clarinet      | -             |
| vacuum cleaner  | cat           | -             |

​	2-class sound data set was used to develop a pipe-line for data transformation, model tuning and selection. Voting and stacking classifiers were also tested with the pre-trained models on the 2-class sound data.  Model training on the 10-class data set was done with an AWS instance. 

​	Gradient Boosting was the best performing model with the F1 score of 0.7304. Other tested models showed the following results: Random Forest (0.6874), Logistic Regression (0.6799), Multinomial Naive Bayes (0.6398) and K-Nearest Neighbors (0.6000). 

​	Self-recorded sound clips of home-related activities were classified with the pre-trained models. The sound class recognition varied between classes. The following classes - "water", "clarinet", vacuum cleaner", "cat" were recognized more successfully than "footsteps", "door opening" or "microwave" classes. Additional recordings might need to be added to the training set to improve the recognition of more challenging classes.

**Conclusions**

​	Sound can be used for recognition of home related activities. Gradient Boost model can successfully classify 10 home sound classes. Logistic Regression should be used instead of Gradient Boost if training time is important. The latter showed 100 time faster training than Gradient Boost within the parameters of this project.

**Future work**

​	An ability to classify sounds can dramatically expand the house assistant AI's functions. By "knowing" what the human is currently doing the house assistant can help with the activity, offer next steps or simply be more human-like and comment about the activity. Specifically, we could add  custom skills to Alexa that are evoked by certain sounds/activities. For instance, a school morning AI assistant could monitor kids' activities and "remind" them to pack their lunches and get ready for school on time.

