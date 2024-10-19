# Receiptor: Simplifying Gmail Receipt Extraction for Developers

---

## The Birth of Receiptor: A Developer's Personal Journey

As a developer, I found myself deep in the trenches of building a feature called "Receipt Radar." What seemed like a straightforward task - extracting receipt data from Gmail - quickly turned into a labyrinth of complex documentation, confusing OAuth processes, and the intricate dance of access and refresh tokens.

I vividly remember the frustration of sifting through Google's API documentation, trying to decipher how to generate access tokens, manage refresh tokens, and navigate the maze of Gmail's API ecosystem.

I thought to myself, "There has to be a better way. Why should every developer go through this struggle?" That's when I decided to create a Python library that would shield other developers from the complexities I faced.

---

## Overview

Receiptor is the culmination of my journey - a straightforward Python-based solution designed to extract, parse, and structure Gmail receipt and invoice data. It's built with one goal in mind: to let developers integrate Gmail receipt data ingestion functionality easily, without the need to juggle through Gmail documentation or spend hours looking at examples.

In today's digital age, Gmail has become a primary tool for tracking purchases, managing expenses, and storing important financial information. Every day, millions of people receive receipts, invoices, and order details through their Gmail accounts. For developers building personal finance apps, expense management software, or business analytics tools, accessing this data efficiently is crucial.

---

## How Receiptor Simplifies the Process

Receiptor addresses the challenges I faced head-on:

**1.No More API Confusion:**
 Say goodbye to the days of deciphering multiple Gmail APIs. Receiptor handles all the complex interactions behind the scenes.

 **2.OAuth Made Easy:**
 Remember my struggle with understanding Google OAuth? Receiptor simplifies this process, making it straightforward to set up and manage authentication.

 **3.Effortless Data Extraction:**
 With just a few lines of code, you can now fetch, parse, and structure receipt data from Gmail. No more headaches trying to navigate through email content and attachments.

 **4.Structured Output:**
 Receiptor doesn't just extract data; it presents it in a clean, structured format ready for your application to use.


---
## Why did I Build Receiptor ?

I built Receiptor because I believe that developers should focus on creating amazing features and applications, not on wrestling with API documentation. By encapsulating my learnings and solutions into this library, I hope to save other developers the time and frustration I experienced.
Whether you're building the next big fintech app, a simple expense tracker, or anything in between, Receiptor is designed to be your go-to tool for Gmail receipt data extraction. It's my way of contributing to the developer community and making our collective lives a little easier.

---

## Getting Started

**1. Fetching and Parsing Data with Minimal Code**

Receiptor provides a clean, straightforward implementation to interact with Gmail and extract receipt data. With only a few lines of code, developers can set up Receiptor and fetch receipt information directly from their Gmail accounts. Here’s a quick overview:

- **Install Receiptor**: The package can be installed via pip, making it accessible to any Python developer:
- 
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
## Example Outputs

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

## Conclusion: Why Receiptor is a Game-Changer for Developers

Receiptor is more than just a library; it's a solution born from real-world developer challenges.Hope receiptor makes your life easy for build data ingestion pipeline from gmail !!
I hope that Receiptor helps you build amazing things without the headaches I encountered. 
Happy coding!
