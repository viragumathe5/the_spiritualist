Text Extraction
==============================

**Text Extraction**

The dataset has the provided OCR XMLs from which the data for the newspapers were 
extracted in the form of JSONs in which each JSON contains all the data for the single paper.

The data contains the important meta data like paper id, page number and text related to the page number.
The extracted text was as per OCR XMLs hence it contains alot of lossy extraction.

The future plans is to use the OCR correction fto improve the texts.

The following snippets shows the JSON structure in which the data got extracted.


.. code-block:: JSON
   :linenos:

   {
    "paper_id": "<PAPER_ID>",
    "newspaper_name": "Spiritualist",
    "newspaper_issue": "<ISSUE_NUMBER>",
    "date": "<DATE>",
    "Page1": "",
    "Page2": "",
    "Page3": "",
    "Page4": "",
    "Page5": "",
    "Page6": "",
    "Page7": "",
    "Page8": "",
    ..
    ..
    ..
    "text":  "<CONCATINATED_TEXT>"
   }

The articles are saved in the specific files which can be downloaded on request by the Dr.Rosa Filgueira.



.. toctree::
   :maxdepth: 10
   :caption: Contents: