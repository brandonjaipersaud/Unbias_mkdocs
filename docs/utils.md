!!! note
    These are internal functions used by UnBIAS to help run various parts of the pipeline. You will likely not need to use these. 

### `re_incomplete_sentence(text:str) -> str`
: Removes incomplete sentences from a text. This may occur when Llama2 stops generating text due to a maximum token generation limit. For instance, a generated sentence may look like: `The man was hungry. He went to`, in which case it would remove `He went to` from the text.

    <h4> Parameters </h4>
    : **text**: The text to clean.

    <h4> Returns </h4>
    : The text with any incomplete sentences removed.

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias

    cleaned_sentence = unbias.re_incomplete_sentence('The man was hungry. He went')
    print(cleaned_sentence)
    ```

    <h4> Output </h4>
    `The man was hungry.`

### `tokenize_for_prediction(text:str, tokenizer:PreTrainedTokenizer) -> list[int], list[int]`
: Tokenizes the text and returns the corresponding `input_ids` and `attention_mask`.

    <h4> Parameters </h4>
    : **text**: The text to tokenize.
    : **tokenizer**: A [Hugging Face Tokenizer](https://huggingface.co/docs/transformers/main_classes/tokenizer).

    <h4> Returns </h4>
    : **input_ids**: List of integers representing tokenized text.
    : **attention_mask**: A list with the same length as input_ids, consisting of 1s and 0s, where 1 indicates a real token, and 0 indicates a padding token. This tells the model which tokens should be [attended](https://machinelearningmastery.com/the-transformer-attention-mechanism/) to.

    <h4> Example </h4>

    ```py
    import UnBIAS.unbias as unbias
    from transformers import AutoTokenizer

    model = "newsmediabias/UnBIAS-LLama2-Debiaser-Chat-QLoRA"
    tokenizer = AutoTokenizer.from_pretrained(model)
    tokenized_text = unbias.tokenize_for_prediction('The man was hungry.', tokenizer)
    print(tokenized_text)
    ```

    <h4> Output </h4>
    `[ints representing token ids], [0s and 1s]`