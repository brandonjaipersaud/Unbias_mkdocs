<!DOCTYPE html>
<html>
<head>
    <title>UnBIAS Toolkit Documentation</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
        .header { background-color: #f8f8f8; padding: 10px; text-align: center; } /* Updated to light gray color */
        .footer { background-color: #f4f4f4; padding: 10px; text-align: center; }
        .nav-bar { display: flex; justify-content: space-between; align-items: center; background-color: #333; padding: 10px; }
        .nav-bar img { height: 50px; }
        .nav-bar nav { display: flex; }
        .nav-bar a { color: white; padding: 10px; text-decoration: none; }
        .nav-bar a:hover { background-color: #ddd; color: black; }
        .main { padding: 20px; }
        section { margin-bottom: 20px; }
        .footer p { margin: 5px 0; }
        code { background-color: #eee; padding: 2px 5px; border-radius: 3px; }
    </style>
</head>
<body>

<div class="header">
    <div class="nav-bar">
        <img src="./images/logo.png" alt="Vector Institute Logo"/>
        <nav>
            <a href="#welcome">Welcome</a>
            <a href="#overview">Overview</a>
            <a href="#features">Features</a>
            <a href="#installation">Installation</a>
            <a href="#usage">Usage</a>
            <a href="#demo">Demo</a>
            <a href="#contact">Contact</a>
        </nav>
    </div>
</div>



<div class="main">
    <section id="welcome">
        <h1>Welcome to UnBIAS</h1>
        <p>Explore the forefront of unbiased text analysis with UnBIAS.</p>
    </section>

    <section id="overview">
        <h2>Overview</h2>
       <p style="text-align: justify;">
    UnBIAS is an innovative text analysis and debiasing toolkit, expertly crafted by the Vector Institute to identify and mitigate biases in textual content. Utilizing advanced Transformer models like BERT, RobERTa, and Meta - LLama-2-7B large language models (LLMs). UnBIAS ensures fairness and neutrality in AI-driven text analysis. With its cutting-edge technology, and aligned to our mission, <b>Vector is supporting and developing toolkits like UnBIAS to promote ethical AI practices and fostering a more equitable digital world</b>.
</p>


<p><strong>PyPI</strong>: <a href="https://pypi.org/project/UnBIAS/">https://pypi.org/project/UnBIAS/</a></p>
   

    </section>


    <section id="features">
        <h2>Features</h2>
<ul>
    <li><strong>Advanced Bias Classification</strong>: Employs sophisticated algorithms to automatically detect and classify biases in texts, promoting fairness and equality in content analysis.</li>
    <li><strong>Named Entity Recognition (NER) for Bias Identification</strong>: Pinpoints specific biased terms and entities within texts, significantly enhancing content integrity and impartiality.</li>
    <li><strong>Comprehensive Text Debiasing</strong>: Processes and neutralizes biases in texts, ensuring content is free from prejudices related to gender, race, age, or other sensitive attributes.</li>
    <li><strong>User-Friendly API Integration</strong>: Offers an intuitive and straightforward interface, enabling easy integration into a variety of applications without extensive technical knowledge.</li>
</ul>

    </section>
<div align="center">
    <img src="./images/fig1.jpg" width="300">
</div>

    <section id="installation">
        <h2>Installation</h2>
        <p style="text-align: justify;"> UnBIAS can be easily installed using pip. Open your terminal or command prompt and execute the following command:</p>
        <code>pip install UnBIAS</code>
    </section>

    <section id="usage">
    <h2>Usage</h2>
    <p style="text-align: justify;">Integrate UnBIAS into your projects with ease. For detailed guidelines, refer to our <a href="usage/">usage documentation</a>.</p>
    </section>


 <section id="demo">
    <h2>Demo</h2>
    <p style="text-align: justify;">Experience UnBIAS firsthand with our interactive demos:<sup>1</sup></p>
    <ul>
        <li><a href="https://drive.google.com/file/d/1RivDKlnQEUc1JcvC78DKUPca_JfkJnx2/view?usp=sharing">Open in Google Colab</a></li>
    </ul>
    <p id="footnote"><sup>1</sup> Please note: For optimal performance, this demo requires a T4 GPU or better. Availability of specific GPU types may vary in the free version of Google Colab.</p>
</section>



<section id="vision">
    <h2>Vision</h2>
    <p style="text-align: justify;">The <a href="https://vectorinstitute.ai/">Vector Institute for Artificial Intelligence</a> is committed to leading the transformation of AI research and development, focusing on ethical, equitable, and sustainable solutions. Our vision is to harness the full potential of AI to benefit society and drive positive global change. By fostering collaborative innovation and nurturing top AI talent, we aim to be at the forefront of creating a future where AI is a force for good, enhancing human capabilities and addressing the world's most pressing challenges.</p>
</section>

<div class="footer">
    <!-- Contact Information Section -->
    <section id="contact" style="margin-bottom: 20px; border-bottom: 1px solid #ccc; padding-bottom: 20px;">
        <h2>Contact Information</h2>
        <p style="text-align: center;">
            Dr. Shaina Raza<br>
            Applied Machine Learning Scientist - Responsible AI<br>
            Email: <a href="mailto:shaina.raza@utoronto.ca">shaina.raza@vectorinstitute.ai</a><br>
            <!-- Include any additional contact information here if needed -->
        </p>
    </section>
</div>

<div>
    <!-- Acknowledgements Section -->
    <section id="acknowledgment" style="font-size: small; margin-top: 20px;">
        <h2>Acknowledgements</h2>
        <p style="text-align: justify;">We would like to express our profound gratitude to the <b>Vector Institute for Artificial Intelligence</b> for the invaluable support and resources that have been pivotal in developing this toolkit.</p>
        <p style="text-align: justify;">A special thanks to Oluwanifemi Bamgbose, Mizanur Rahman, Brandon Jaipersaud, Shardul Ghuge from the Vector Institute for facilitating the development of this project.</p>
    </section>
</div>



