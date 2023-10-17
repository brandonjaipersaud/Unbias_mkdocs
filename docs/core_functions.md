
### `get_debiased_sequence(text:str) -> str`
: Debiases the given text by prompting Llama2.

    <h4> Parameters </h4>
    : **text**: The text to debias.

    <h4> Returns </h4>
    : The debiased text.

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias

    debiased_sequence = unbias.get_debiased_sequence("Men are dumb.")
    print(debiased_sequence)
    ```

    <h4> Output </h4>
    `I apologize, but it's important to avoid making gender-based generalizations or insults. Men and women are individuals with their own unique perspectives and experiences.`

    !!! note

        The output of debiasing this sentence can vary since Llama2 is a probabilistic model. This is why it varies from when we debiased it in the `run_pipeline_on_texts` example.


### `create_bias_analysis_dataframe(texts:list[str], pipeline_instance:BiasPipeline) -> pd.DataFrame`
: Runs the pipeline on each text in the list and returns a dataframe with the results.

    <h4> Parameters </h4>
    : **texts**: The text to debias.
    : **pipeline_instance**: A [BiasPipeline](bias_pipeline.md) instance used to run the pipeline.

    <h4> Returns </h4>
    : A Pandas DataFrame with columns: [Original_Text, Label_Bias, Biased_Phrases, Debiased_Text].

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias

    # Define your test sentences
    biased_texts =  ["The weather is cold outside.", "Men are dumb."]

    # Use the function. Gets saved to debiased_results.csv
    results = unbias.run_pipeline_on_texts(biased_text)
    print(results)
    ```
    <h4> Output </h4>

    | Original_Text               | Label_Bias      | Biased_Phrases                 | Debiased_Text                                   |
    |-----------------------------|-----------------|--------------------------------|-------------------------------------------------|
    | The weather is cold outside.| NON-BIASED(99%) | [cold-B-BIAS, outside-I-BIAS]  | The temperature is currently cold.              |
    | Men are dumb.               | BIASED(98%)     | [men-B-BIAS, are-I-BIAS, dumb-I-BIAS] | Men may have different cognitive abilities or understanding perspectives. It is not accurate or fair to make broad generalizations about any particular group of people. |


### `run_pipeline_on_texts(texts:list[str]) -> pd.DataFrame`

: Runs all three stages of the pipeline on the provided list of texts and saves the resulting DataFrame to a file named `debiased_results.csv`.

: This function calls `create_bias_analysis_dataframe` to generate the DataFrame and then saves it to  `debiased_results.csv`.

    <h4> Parameters </h4>
    : **texts**: The list of texts to run the pipeline on.

    <h4> Returns </h4>
    : A Pandas dataframe with columns: [Original_Text, Label_Bias, Biased_Phrases, Debiased_Text].

    <h4> Example </h4>

    You can use this function in the same way as `create_bias_analysis_dataframe()`. The only difference is the generated DataFrame gets saved to `debiased_results.csv`.

    !!! note
        
        This function will overwrite any existing file called `debiased_results.csv` in your working directory.






