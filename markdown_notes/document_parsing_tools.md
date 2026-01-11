This is a collection of document parsing tools.

1. [MinerU](https://mineru.net/)

Able to parse a PDF into Markdown or JSON. Tables can easily be targeted by boxes and parsed into HTML tables.

Using locally, it either runs against small local models on CPU in pipeline. Or it runs against large models on GPU.

Able to merge across-page tables.

1st [output sample in JSON](resources/mineru_output_sample_1.JSON) and [its input](resources/mineru_input_sample_1.pdf).

2nd [output sample in JSON](resources/mineru_output_sample_2.JSON) and [its input](resources/mineru_input_sample_2.pdf).

2. [Unstract](https://unstract.com/)

Adapt to multiple input file types and output foramts(JSON, table, text). Provide workflow and API. 

Learn how Unstract does it from [here](https://docs.unstract.com/unstract/index.html).

The open-source version doesn't have some LLM-based functions, including review and summarization.

Sign up to try for free.

The locating of contents is on the basis of LLM and prompts.

3. [Docling](https://docling-project.github.io/docling/)

Adapt to multiple input file types and produces multple outbound formats(markdown, JSON, HTML).

Easy to integrate to a Python project.

Use a template in string, dict or Pydantic model. There is an [exmaple](https://docling-project.github.io/docling/examples/extraction/#using-a-string-template). Must it return page by page?

Able to find the tables.

Adapt to online file.

Provides ORC engine options. 

Chuncking abilities simplifying RAG.

