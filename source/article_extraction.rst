Article Extraction
==============================

**Article Extraction Process**

For creating an open knowledge project the plan is to build a RAG which can be esaily accessible using simple queires.
for that purpose the articles and other contents are needed to extracted.

The project uses very specific prompt engineering to extract the articles from the articles. The first approach is to divide the concatinated text into the two different segments and feed it to gpt-4o to get the articles but it was more expensive and time consuming and therefore the new extraction process was used for extracting the articles from each page. So the each paper is calling the API for the each page in the newspaper.

The follwoing snippit shows the exracted format for the articles from the specific paper id and page numer.

.. code-block:: JSON
   :linenos:


    {
      "135908619": {
        "Page2": [
          {
            "title": "",
            "article": ""
          }
        ],
        "Page3": [
          {
            "title": "",
            "article": ""
          }
        ],
        "Page4": [
          {
            "title": "",
            "article": ""
          },
        ],
        "Page5": [
          {
            "title": "",
            "article": ""
          },
          {
            "title": "",
            "article": ""
          },
          {
            "title": "",
            "article": ""
          }
        ],
        "Page7": [
          {
            "title": "",
            "article": ""
          },
          {
            "title": "",
            "article": ""
          },
          {
            "title": "",
            "article": ""
          },
          {
            "title": "",
            "article": ""
          }
        ]
      }
    }


This JSONs helps trace back the articles when they are retrieved and indexed. After the generation of the respone it can be referred back as the generated content reference.

**Documents**

As a part of the RAG pipeline, Each article is considered as a document. Hence it needs to have its own meta data to retrieve the information about the article. The important meta data which needs to be traced back is paper id, page number, title and text. All the extracted information get paarsed and the documets are stored in the JSON for preparaiton of the vector database.

The following snippit shows the possible JSON format in which the documents are saved.

.. code-block:: JSON
   :linenos:

    {
      "id": "<PAPER_ID>",
      "page_number": "<PAGE_NUMBER>",
      "title": "<ARTICLE_TITLE>",
      "text": "<ARTICLE_TEXT>"
    
    }


This format will help the efforless creation of the vector database and retrieval of the documents.


.. toctree::
   :maxdepth: 10
   :caption: Contents: