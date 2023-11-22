<!DOCTYPE html>
<html>
<head>
    <title>Usage - UnBIAS Toolkit</title>
</head>
<body>
    <h1>Usage - UnBIAS Toolkit</h1>

    <h2>How to install UnBIAS PyPi Package</h2>
    <p>To use UnBIAS, you'll need to have <a href="https://www.python.org/downloads/">Python</a> installed on your system. UnBIAS supports Python3 and above.</p>

    <h3>Installation via pip</h3>
    <p>The recommended way to install UnBIAS is via <a href="https://pip.pypa.io/en/stable/">pip</a>, the Python package manager. Open your terminal or command prompt and run the following command:</p>
    <pre><code>pip install UnBIAS</code></pre>

    <h2>Quickstart</h2>
    <p>The UnBIAS library provides a function: <a href="/project/UnBIAS/core_functions/">run_pipeline_on_texts</a> which will perform bias classification, NER for bias, and generate a debiased version of your text. A simple usage of the library is as follows:</p>
    <pre><code>from UnBIAS import run_pipeline_on_texts

biased_texts = ["Men make better programmers than women", 
                "People who wear Y clothing are untrustworthy."]
results = run_pipeline_on_texts(biased_texts)
results.to_csv('&lt;save_path&gt;.csv', index=False)</code></pre>

    <p>If you have a dataset CSV file, you can extract the text column and run the pipeline on it as follows:</p>
    <pre><code>from UnBIAS import run_pipeline_on_texts
import pandas as pd 

biased_texts = pd.read_csv("&lt;dataset_path&gt;.csv")
biased_texts = list(biased_texts['Text'])
results = run_pipeline_on_texts(biased_texts)
results.to_csv('&lt;save_path&gt;.csv', index=False)</code></pre>

    <p>Refer to the <a href="/project/UnBIAS/core_functions/">API Reference</a> for more information about <code>run_pipeline_on_texts</code>.</p>

    <p><strong>Disclaimer:</strong> The Jupyter Notebooks linked from this package use GPU resources on Google Colab Pro. Intensive GPU usage may be limited by Google Colab's policies. If resource limitations are a concern, consider using <a href="https://drive.google.com/file/d/1RivDKlnQEUc1JcvC78DKUPca_JfkJnx2/view?usp=sharing">this notebook on Google Colab</a>.</p>

    <h2>Additional Highlights</h2>
    <ul>
        <li><strong>Pre-trained Models:</strong> Uses specialized models from the renowned <a href="https://huggingface.co/docs/transformers/index">Hugging Face's Transformers library</a>. We have also tailored Transformer-based models for bias detection and debiasing tasks <a href="https://huggingface.co/newsmediabias">newsmediabias-hub</a>.</li>
        <li><strong>Efficient Pipelines:</strong> Designed with intuitive pipelines, making it easier to incorporate into applications or other projects.</li>
        <li><strong>Analytical Tools:</strong> Handy tools available to transform results into structured data for further analysis.</li>
    </ul>

    <h2>What to do next?</h2>
    <ul>
        <li>You can individually run each stage of the pipeline. For instance, maybe you only care about debiasing text without concern for classification or NER for bias. To see how to do this, refer to the <a href="/project/UnBIAS/bias_pipeline/">BiasPipeline</a> class in the API.</li>
        <li>Debiasing text works by prompting the Llama2 LLM with a specific prompt. You can modify this prompt to suit your needs. See the <a href="/project/UnBIAS/constants/">Constants</a> section for more information.</li>
    </ul>
</body>
</html>
