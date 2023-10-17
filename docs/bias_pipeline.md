# BiasPipeline: Class

This class can be used to individually run the bias classification and NER for bias stages of the pipeline. See the example code snippets below on how to do this. It is also used by the [`run_pipeline_on_texts`](core_functions.md) function to perform the entire pipeline on a list of texts. 

To individually run the debiasing stage of the pipeline see the [`get_debiased_sequence`](core_functions.md) function.

<!-- ## Usage -->

<!-- ```py
from UnBIAS.unbias import BiasPipeline
import pandas as pd 

biased_texts = pd.read_csv("<dataset_path>.csv")
# Assuming your CSV has a column called 'Text' that you want to debias
biased_texts = list(biased_texts['Text'])
# run the pipeline and save results
results = run_pipeline_on_texts(biased_texts)
results.to_csv('<save_path>.csv', index=False)
```  -->

### `__init__() -> None`
Called upon initialization. It calls `load_resources()` below.

### `load_resources() -> None`
Loads the bias classifier and NER tokenizers and models.

### `predict_entities(text:str) -> list[str]`
: Retrieves biased entities from a text. 

    <h4> Parameters </h4>
    : **text**: The text to retrieve biased entities from.

    <h4> Returns </h4>
    : A list of biased entities in the text.

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias

    sentence = """Last Tuesday, Elon Musk announced a new project on Mars, 
                which would be funded with $6 billion from Tesla, and he discussed  
                this in New York during a United Nations meeting."""

    bias_pipeline = unbias.BiasPipeline()
    biased_entities = bias_pipeline.predict_entities(sentence)
    print(biased_entities)
    ```

    <h4> Output </h4>
    `['new-B-BIAS',
    'project-I-BIAS',
    'funded-B-BIAS',
    'discussed-B-BIAS',
    'this-I-BIAS',
    'new-B-BIAS',
    'united-B-BIAS',
    'nations-I-BIAS',
    'meeting-I-BIAS']`

    B-BIAS stands for beginning of entity and I-BIAS stands for inside of entity. This is because a biased entity can span multiple words.

    !!! warning

        If running the above multiple times in a Jupyter Notebook, you might have to do `del bias_pipeline` before running it again to avoid out-of-memory errors.

### `predict_bias(texts:str|list[str]) -> list[dict[str: str, str: float]]`
: Performs bias classification on a text or a list of texts. 

    <h4> Parameters </h4>
    : **texts**: The text or list of texts to classify.

    <h4> Returns </h4>
    : An array of dictionaries where each dictionary is of the form: 
    `{'label': Non-biased|Biased, 'score': <bias_score>}`. 

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias

    sentences = ["The weather is cold outside.", "Men are dumb."]
    bias_pipeline = unbias.BiasPipeline()
    sentence_classifications = bias_pipeline.predict_bias(sentences)
    print(sentence_classifications)
    ```

    <h4> Output </h4>
    `[{'label': 'Non-biased', 'score': 0.9980363249778748},
    {'label': 'Biased', 'score': 0.9899910688400269}]`

   



