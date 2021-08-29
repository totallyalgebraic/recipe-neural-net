# **A hilariously bad, soup making neural network**

## Instructions

1. Start bash in the container
    * `docker run --rm -ti {container name} bash`

2. Preprocess the data

    * `python scripts/preprocess.py --input_txt data/soup.txt --output_h5 data/soup.h5 --output_json data/soup.json`

3. Train

    * `th train.lua -input_h5 data/soup.h5 -input_json data/soup.json -gpu -1`

4. Sample
    * `th sample.lua -checkpoint cv/checkpoint_10000.t7 -length 2000 -gpu -1`

## Sampling

Given a checkpoint file (such as those written to cv) we can generate new text. For example:

* `th sample.lua -checkpoint cv/checkpoint_10000.t7 -length 2000 -gpu -1`


There are multiple options you can configure, including but not limited to:

1. Length. Play around with the length flag to generate samples with different lengths. For example, ```-length 10000```  would generate 10,000 characters (default = 2000).

2. Temperature. An important parameter you may want to play with is `-temperature`, which takes a number in range (0, 1] (default = 1). 
Lower temperatures will cause the model to make more likely, but also more boring and conservative predictions. Higher temperatures cause the model to take more chances and increase diversity of results, at a cost of more mistakes.

3. Priming. It's also possible to prime the model with some starting text using `-primetext`. This starts out the RNN with some hardcoded characters to warm it up with some context before it starts generating text. An example might be `-primetext "The best soup is "`.

