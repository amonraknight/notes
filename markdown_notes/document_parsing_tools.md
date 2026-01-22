# Tools can be useful.

1. [MinerU](https://mineru.net/)

Able to parse a PDF into Markdown or JSON. Tables can easily be targeted by boxes and parsed into HTML tables.

Using locally, it either runs against small local models on CPU in pipeline. Or it runs against large models on GPU.

Able to merge across-page tables.

1st [output sample in JSON](resources/mineru_output_sample_1.JSON) and [its input](resources/mineru_input_sample_1.pdf).

2nd [output sample in JSON](resources/mineru_output_sample_2.JSON) and [its input](resources/mineru_input_sample_2.pdf).

More samples:
- [output](resources/MinerU_invoice_sample_1_Contractor Customer Invoice.json) / [input](resources/invoice_sample_1_Contractor Customer Invoice.pdf)
- [output](resources/MinerU_invoice_sample_2 Contractor Invoice.json) / [input](resources/invoice_sample_2 Contractor Invoice.pdf)
- [output](resources/MinerU_invoice_sample_3 Project Customer Invoice.json) / [input](resources/invoice_sample_3 Project Customer Invoice.pdf)
- [output](resources/MinerU_cross_page_table_sample_1.json) / [input](resources/cross_page_table_sample_1.pdf)

2. [Unstract](https://unstract.com/)

Adapt to multiple input file types and output foramts(JSON, table, text). Provide workflow and API. 

Learn how Unstract does it from [here](https://docs.unstract.com/unstract/index.html).

The open-source version doesn't have some LLM-based functions, including review and summarization.

Sign up to try for free.

The locating of contents is on the basis of LLM and prompts.

Source code [here](https://github.com/Zipstack/unstract).


3. [Docling](https://docling-project.github.io/docling/)

Adapt to multiple input file types and produces multple outbound formats(markdown, JSON, HTML).

Easy to integrate to a Python project.

Use a template in string, dict or Pydantic model. There is an [exmaple](https://docling-project.github.io/docling/examples/extraction/#using-a-string-template). Must it return page by page?

Able to find the tables.

Adapt to online file.

Provides ORC engine options. 

Chuncking abilities simplifying RAG.

4. [AWS Textract](https://ap-northeast-2.console.aws.amazon.com/textract/home?refid=924a57b7-e471-4fb8-a874-cc5547ee2932&region=ap-northeast-2#/)

Textract is able to find key-values and tables out of docs.

To try it locally, please refer to [this](https://docs.aws.amazon.com/textract/latest/dg/program-access.html).

Refer to [this page](https://docs.aws.amazon.com/textract/latest/dg/analyzing-document-text.html) about how to analyze a document.
To parse a file having multiple pages, refer to [another page](https://docs.aws.amazon.com/textract/latest/dg/async-analyzing-with-sqs.html).


The precondition of using asynchronized document analysis includes:
    - minimum roles: AmazonTextractFullAccess, AmazonS3ReadOnlyAccess, AmazonSNSFullAccess, AmazonSQSFullAccess
    - User role has permission to pass IAM roles to Amazon Textract.
    - has a bucket, upload target PDF file in S3 bucket
    - an Amazon SNS topic
    - an Amazon SQS queue
    - Give the topic permission to send messages to the queue.
    - Giving Amazon Textract Access to Your Amazon SNS Topic. Create a role for Textract and assign it with the roles to visit S3, SNS and SQS.


There are 2 main parse types, FORM and TABLES. In type FORM Textract is going to extract content to key-value sets. TABLES mode finds tables with header, footer and cells.


1st [output sample in JSON](resources/textract_output_sample_1.json) and [its input](resources/mineru_input_sample_1.pdf).

AWS Textract is not good at parsing Chinese.

2nd [output sample in JSON](resources/textract_output_sample_2.json) and [its input](resources/textract_input_sample_2.pdf).

More samples:
- [output](resources/textract_invoice_sample_1_Contractor Customer Invoice.json) / [input](resources/invoice_sample_1_Contractor Customer Invoice.pdf)
- [output](resources/textract_invoice_sample_2 Contractor Invoice.json) / [input](resources/invoice_sample_2 Contractor Invoice.pdf)
- [output](resources/textract_output_sample_cross_page_table_sample_1.json) / [input](resources/cross_page_table_sample_1.pdf)
- [output](resources/textract_output_sample_invoice_sample_3 Project Customer Invoice.json) / [input](resources/invoice_sample_3 Project Customer Invoice.pdf)


5. [LangExtract](https://langextract.com/zh-hans)

Open-source unstructured text documents parser. Based on Gemini, requires an API key. Act as a Python lib.

Needs a prompt and an example.

But this is not for parsing images or PDFs.

Doesn't natively support Chinese.

Allow [customized provider](https://github.com/google/langextract/blob/main/langextract/providers/README.md#creating-a-new-provider).

6. [MarkItDown](https://github.com/microsoft/markitdown)

Now in usage. Not able to keep the table structure.

7. [gptpdf](https://github.com/CosmosShadow/gptpdf)

Use GPT to parse PDF.

# Ideas

1. Embody a parse result in JSON into a tree. The user should be able to browse the tree and choose where his target lies. A user should always select a leave note (table body, text and others).
Use [primeng](https://primeng.org/tree) to represent tree strcture.

2. The Textract parse result of each page can also be transformed from a flat structure into a Json object of a cascading structure.

page --> lines & tables

table --> cells
      --> table title
      --> table footer

The children of each cell in words should be concatenated and play as the text content of that cell.

The lines sharing the same words with cells, table titles should be ignored.

Concatenate all the children words of a table title as its text content.

key of key-value set --> value of key-value set

The children of the key in a set should be concatenated and play as the text content. The value node is likewise.

There can be overlaps between key-value pairs and tables.

Decide how many columns are there by 

Textract didn't detect the 2nd half of the table on the 2nd page. MinerU detected it.