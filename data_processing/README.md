# Milestone 2: Data Loaders and Processors

In the followings we will illustrate the basic schema of each dataset that we will use,  
as well as the `TODO`s and how to test your implementations.


## Dummies

This dummy dataset is intended to be used as a demo for most of the components through  
out this project as well as a reference to other dataset processors.

### Data Schema

```bash
{
    "id": {
        "id": an integer id,
        "sentence": a string,
        "label": an integer label, binary
    },
    ...
}
```

Execute the following command:
```bash
# At the root directory.
python3 -m data_processing.dummy_data
```
You should see the followings as outputs:
```bash
DummyExample(guid=0, text='I am a good boy.', label=1)
DummyExample(guid=1, text='I am a good girl.', label=1)
DummyExample(guid=2, text='I am a bad boy.', label=0)
```


## Com2Sense

### Data Schema

```bash
[
    {
        "sent_1": statement 1,
        "sent_2": statement 2 (a complement to statement 1),
        "label_1": one of {"True", "False"},                            # could be missing for test set
        "label_2": one of {"True", "False"} (a complement to label 1),  # could be missing for test set
        "domain": one of {"physical", "social", "temporal"},
        "scenario": one of {"causal", "comparative"},
        "numeracy": one of {"True", "False"},
        # If you see other fields in some data please ignore them.
    },
    ...
]
```

You need to finish the `TODO` blocks in `_read_data` function in `com2sense_data.py`.

Once done, execute the following command to test your implementation:
```bash
# At the root directory.
python3 -m data_processing.com2sense_data
```
You should see something like the followings as outputs:
```bash
Coms2SenseSingleSentenceExample(guid=0, text='If you are baking two pies, you should double your recipe.', label=1, domain='physical', scenario='causal', numeracy=True)
...
```

## Sem-Eval 2020 Task 4

### Data Schema

```csv
Correct Statement, Incorrect Statement, Right Reason1, Confusing Reason1, Confusing Reason2, Right Reason2, Right Reason3
```

The datasets in Sem-Eval are of csv files, and we highly recommend using [csv.DictReader](https://docs.python.org/3/library/csv.html) to load the files.
Or else, you can consider using [pandas.read\_csv](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) but it might be more straightforward to use the generic `csv` package mentioned above.

The `TODO` here is **optional**, but Sem-Eval may be helpful for the model performance on Com2Sense. You need to implement the `_read_data` function in `semeval_data.py`.

Once done, execute the following command to test your implementation:
```bash
# At the root directory.
python3 -m data_processing.semeval_data
```
You should see something like the followings as outputs:
```bash
SemEvalSingleSentenceExample(guid=0, text='when it rains humidity forms', label=1, right_reason1='hotness will evaporate water', right_reason2='Laundry will not be dry because of the humidity.', right_reason3='Water makes humidity, not temperature.', confusing_reason1='Humidity is a measure of moisture in the atmosphere.', confusing_reason2='Laundry will not be dry because of the humidity.')
...
```


# The Dataset Class

In `processors.py` please carefully read the `DummyDataset`.
Using this, complete the `TODO` for `__getitem__` function in `Com2SenseDataset` class in `processors.py` file.

Once done, execute the following command to test your implementation:
```bash
# At the root directory.
python3 -m data_processing.processors -d com2sense
```

You may **optionally** finish the `TODO` for `__getitem__` function in `semeval_data.py` as well, which may be helpful for improving the model performance on Com2Sense.

# Initializations

Please take a look at the `__init__.py` to make sure that you understand how to call the data processors and classes in other codes.
