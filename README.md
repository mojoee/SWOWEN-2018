# SWOWEN-2018
Import, preprocessing, and basic analysis pipeline for the English [Small World of Words project](https://smallworldofwords.org/project/)




## Getting started
In addition to the scripts, you will need to retrieve the word association data.
These can be found on the Small World of Words [research page](https://smallworldofwords.org/project/research/). Choose the English data (the Dutch data still need to be updated to be used with an R pipeline).


## Participant data
The datafile consists of participant information about age, gender, native language and location.
For a subset of the data, we also provided information about education (we only started collecting this later on).

* `participantID`: unique identifier for the participant
* `created_at`: time and date of participation
* `age`: age of the participant
* `nativeLanguage`: native language from a short list of common languages
* `gender`: gender of the participant (Female / Male / X)
* `education`: Highest level of education:  1 = None, 2 = Elementary school, 3 = High School, 4 = College or University Bachelor, 5 = College or University Master
* `city`: city (city location when tested, might be an approximation)
* `country`: country (countr location when tested)



## Word association data

### Raw data
The raw data consist of the original responses and spell checked responses. The spell-checked was performed at the server side and for now this script is not included in the current repository.
However, you can find a list spelling corrections and English capitalized words in the `./data` subdirectory.

* `section`: identifier for the snowball iteration (e.g. set2017)
* `cue`: cue word
* `R1Raw`: raw primary associative response
* `R2Raw`: raw secondary associative response
* `R3Raw`: raw tertiary associative response
* `R1`: corrected primary associative response
* `R2`: corrected secondary associative response
* `R3`: corrected tertiary associative response


### Preprocessed data
The preprocessed data consist of normalizations of cues and responses by spell-checking them, correcting capitalization and Americanizing. This file is generated by the `preprocessData.R` script.

In addition to normalizing cues and responses, this script will also extract a balanced dataset, in which each cue is judged by exactly 100 participants. Because each participant generated three responses, this means each cue has 300 associations. The participants were selected to favor native speakers.


## Graphs
Use `createSWOWENGraph.R` to extract the largest strongly connected component  for graphs based on the first response (R1) or all responses (R123). The results are written to `output/adjacencyMatrices` and consist of a file with labels and a sparse file consisting of three values corresponding to row- and column-indices followed by the association frequencies.
In most cases, associative frequencies will need to be converted to associative strengths by dividing with the sum of all strengths for a particular cue.
Vertices that are not part of the largest connected component are listed in a report in the `output/reports` subdirectory.


## Derived statistics
### Response statistics
### Cue statistics
### R1 - R2 response chaining