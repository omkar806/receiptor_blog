# Receiptor: Simplifying Gmail Receipt Extraction for Developers

---

### Overview

In today’s digital age, Gmail has become a primary tool for communication, managing work, and tracking purchases. Every day, millions of people receive receipts, invoices, and order details through their Gmail accounts. For developers, accessing and structuring this data can be quite challenging. Whether it’s building personal finance apps, creating expense management software, or developing business analytics tools, the need for efficient and automated Gmail receipt extraction is critical.

**Receiptor** is designed to address these challenges by providing a straightforward Python-based solution to extract, parse, and structure Gmail receipt and invoice data. This README delves into the complexities developers face when working with Gmail APIs, how Receiptor streamlines this process, and the technicalities behind its operation.

---

### The Pain Points of Extracting Gmail Receipt Data

Ingesting receipt data from Gmail, despite its ubiquity, remains a complex task. Developers often need to navigate Gmail’s APIs, which can be intricate and overwhelming. Let’s explore these pain points in detail:

#### Navigating the Complicated Gmail API Landscape

Gmail’s API ecosystem offers numerous functionalities, but accessing specific receipt data requires understanding several distinct APIs and how they work together. Developers must interact with multiple endpoints to:

- **List Gmail messages**: Developers use the Gmail API to list messages, filtering by criteria like date, subject, or sender. However, this only provides a list of email IDs, not the actual email content.
- **Access individual emails**: Once an email ID is retrieved, developers need to call another API to access the email’s content and metadata. This often requires careful handling of API requests and responses.
- **Parse attachments**: Receipts and invoices are commonly sent as attachments in PDF, image, or other file formats. Extracting and decoding these attachments demands another level of API interaction, requiring specific parsing logic.
- **Handle pagination**: Gmail’s API uses pagination to manage large sets of emails. Developers need to manage page tokens to ensure that all relevant emails are fetched, which adds complexity.

#### Deciphering API Responses

The responses provided by Gmail’s API are often not straightforward. They include a large amount of metadata, and developers need to extract the essential information like subject lines, email body text, and attachment details. Understanding and filtering through the extensive data provided in these responses is time-consuming and can be error-prone.

#### The Tedious Task of Structuring Extracted Data

Once developers manage to retrieve and parse the necessary data, they face another challenge: structuring it into a usable format, such as JSON. Structuring data manually, especially from diverse email formats and attachments, can be incredibly tedious. Moreover, this process must be repeated for each new receipt type or source, further complicating data ingestion efforts.

---

### Receiptor: The Solution Developers Have Been Waiting For

Receiptor is a Python package built specifically to address the aforementioned challenges. It simplifies the extraction, parsing, and structuring of Gmail receipt, invoice, and order data, offering developers an easy-to-use interface that abstracts the complex interactions with Gmail’s APIs.

#### How Receiptor Works ?

Receiptor is designed with the developer’s ease of use in mind. Here’s how it streamlines the Gmail data extraction process:

**1. Fetching and Parsing Data with Minimal Code**

Receiptor provides a clean, straightforward API to interact with Gmail and extract receipt data. With only a few lines of code, developers can set up Receiptor and fetch receipt information directly from their Gmail accounts. Here’s a quick overview:

- **Install Receiptor**: The package can be installed via pip, making it accessible to any Python developer:
  ```python
    
    pip install receiptor
    ```

**2. Set Up Gmail Access**

Receiptor requires a Gmail access token, which can be obtained using OAuth2. This token enables secure and authenticated access to Gmail data .

**3. Library Usage**
- **Import required modules**
```bash

from receiptor import Receiptor
from receiptor.llm_parser.gpt_4o_mini_parser.gpt_4o_mini import DocumentStructureExtractor
```
- **Setup OpenAi Api Keys as follows**
 Pass the API keys into the function.

```python
structured_data = DocumentStructureExtractor.structure_document_data(
       raw_text=data.attachments[0].attachment_raw_text
       ,openai_api_key = "" , org_id = ""
   )
```
Note : org_id is optional , if you are using any organisation project then you may require this org_id , which can be obtained through open ai account dashboard. For more information you can go through open ai official (documentation)[https://platform.openai.com/docs/api-reference/making-requests]

- **Initialize the Receiptor object**
```python

obj = Receiptor()

```
- **Set up Gmail access token**
Obtain a Gmail access token through the OAuth2 flow. Store this token securely.

```python

access_token = "Your_Gmail_access_token_here"
```
- **Fetch and process receipt data**
```python

for data in obj.fetch_receipt_data(access_token=access_token):
    print(data)
    if data.attachments:
        # Print the raw text of the first attachment
        print(data.attachments[0].attachment_raw_text)
        
        # Structure the attachment text using DocumentStructureExtractor
        structured_data = DocumentStructureExtractor.structure_document_data(
            raw_text=data.attachments[0].attachment_raw_text ,openai_api_key = "your api key" , org_id = "org id but this is optional"
        )
        print(structured_data)

```
- **Example Output**

Main Data
```python
{
"message_id": "1dsse2342dfs3",
"body": "body text",
"company": "zomato.com",
"attachments": [
"<models.attachment.Attachment object at 0x1040d45c0>",
"<models.attachment.Attachment object at 0x10407b440>",
"<models.attachment.Attachment object at 0x103f90980>"
],
"attachment_extension": "pdf"
}
```
Attachment Raw Text

```python

Zomato Food Order: Summary and Receipt


```
Structured Document Data

```python

{
"brand": "brand name",
"total_cost": "189",
"location": "New york",
"purchase_category": "Food",
"brand_category": "Culinary Services",
"Date": "01-01-2024",
"currency": "INR",
"filename": "filename",
"payment_method": null,
"metadata": null
}

```

With just these steps, Receiptor handles the complexity of interacting with multiple Gmail APIs, fetching the required emails, and retrieving all relevant information, including attachments.

### Conclusion: Why Receiptor is a Game-Changer for Developers

For developers dealing with email receipt data extraction, Receiptor offers an efficient, streamlined, and powerful solution. It takes the guesswork out of navigating Gmail’s APIs and provides tools that not only extract data but also structure it into a usable format for further processing. Whether you are building expense trackers, data analytics platforms, or business intelligence tools, Receiptor can save time, reduce complexity, and improve productivity.
