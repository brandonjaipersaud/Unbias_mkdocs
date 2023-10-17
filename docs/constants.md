

### `sys_message:str` 

- **default value**: Task: Please just generate a bias-free version of the text provided, ensuring it's free from biases related to  age, gender, politics, social nuances, or economic background, while keeping it roughly the same length as the original:

### `instruction:str` 

- **default value**: Instruction: As a helpful, respectful and trustworthy debiasing assistant, your task is to receive a text and return its unbiased version, Don't add additional comment. Just return the  un biased version of the input text:

<h4> Modification </h4>
The above two parameters are used to prompt Llama2 to debias text. Feel free to change these constants to suit your task. You can even play around with various debiasing prompts to see if it performs better than what we currently use for debiasing.

Here is an example of modifying the constants for the summarization of complex information:


```py
import UnBIAS.unbias as unbias

unbias.sys_message = "Task: Please generate a simplified version of the provided text, ensuring it's easy to understand, devoid of technical jargon, and accessible to readers of all education levels, while keeping it concise and retaining the original's core information:"
unbias.instruction = "Instruction: As a friendly, approachable, and reliable simplification assistant, your task is to receive a text and return its simplified version. Don't add personal opinions or extraneous explanations. Just return the text in a form that's easier to understand for the average reader:"

long_text = "In the field of quantum computing, the Planck scale (named after Max Planck), is the scale of energy (approximately 1.22 x 10^19 GeV) at which quantum effects of gravity become strong. At this scale, it is believed that the effects of quantum mechanics and general relativity converge, necessitating a unified framework, commonly referred to as quantum gravity, to adequately describe phenomena. However, achieving a comprehensive theory of quantum gravity has remained elusive, and it presents one of the most significant challenges in theoretical physics."

simplified_text = unbias.get_debiased_sequence(long_text)
print(simplified_text)
```

<h4> Output </h4>
`In quantum computing, the Planck scale (named after Max Planck), marks the point where the effects of gravity become significant and require a unified framework to describe phenomena.`

