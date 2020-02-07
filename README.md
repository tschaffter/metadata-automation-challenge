# metadata-automation-challenge

## Building docker images

```
docker build -t metadata-challenge-baseline -f Dockerfile.baseline .
docker build -t metadata-challenge-scoring -f Dockerfile.scoring .
```

## Running the baseline method
Here we describe how to apply the baseline method to automatically annotate a dataset (see [Data Description](https://www.synapse.org/#!Synapse:syn18065891/wiki/600449)).

1. Create the folders `input`, `data` and `output` in your current directory.
2. Place the input dataset in `input`, e.g. `input/APOLLO-2.tsv`
3. Run the following command

```
docker run \
  -v $(pwd)/input:/input:ro \
  -v $(pwd)/data:/data:ro \
  -v $(pwd)/output:/output \
  metadata-baseline APOLLO-2
```

where `APOLLO-2` is the name of the dataset in the folder `input` (without the extension `.tsv`).

The file `/output/APOLLO-2-Submission.json` is created upon successful completion of the above command.

## Validating the submission file




## Running the Validator

Using Python:
* Python > 3.6
* `pip install click jsonschema`

```
python schema/validate.py validate-input --json_filepath yourjson.json --schema_filepath schema/output-schema.json
```

If you do not have python environments set up, please install docker and run this command:

```
docker run -v /full/path/to/your/json/yourjson.json:/input.json docker.synapse.org/syn18065892/scoring_harness validate.py validate-input --json_filepath /input.json
```
