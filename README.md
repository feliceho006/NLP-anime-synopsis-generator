# Anime Script Generator

### 1 Introduction
Anime, typically animated works made in Japan, has always been a popular source of entertainment over the years. However, the quality of anime storylines has been declining in recent times, and through this project, we hope to be able to draw on the storylines of popular anime to generate storylines of better quality, or even inspire creativity in future storylines. Our project features models which are able to generate story synopses which could potentially stimulate more creativity in scriptwriters.

### 2 Approach
**2.1 Dataset** <br>

The dataset we decided to proceed with is from https://www.kaggle.com/marlesson/myanimelist-dataset-animes-profiles-reviews . In this dataset, there are **16214** unique values in the **animes.csv** file. However, after taking a look at the data, we found that there are repeated synopsis, for example animes with many seasons will reuse the synopsis, there are entries with no synopsis, and there are synopsis of very short length. Hence in our text generation, we remove those entries.
