# Pairaphrase API


The Pairaphrase translation API is an interface for processing translations using HTTP and JSON. The translation API makes it easy to create web and desktop applications.
Pricing is simple, just $0.0005 per word translated. Volume discounts are available. Learn more about why you should use the Pairaphrase API for your app, versus others on the market.
When you get your Pairaphrase API Token (account required), please note the use of https:// in the Primary API URL. All Pairaphrase API communication is encrypted over HTTPS.
Any nonsecure requests are automatically rejected, so we recommend establishing a test connection with the secure API entry point before sending sensitive data.

API Calls
 

String Translation
Translate single sentences or paragraphs. This request uses standard form POST to allow a binary POST, e.g., content-type: multipart/form-data.

POST Request https://app.pairaphrase.com/apiv2/translate?token=[token]&source=enUS&target=fr-FR

Body / Data

text=Hello, my name is Jack. What is your name?

Response

{"status": 200, "translation":"Bonjour, je m'appelle Jack. Comment vous appelez-vous?" }

 

Return All Translation Memories NEW
Return all translation memories that have been generated or added to Pairaphrase.

GET Request

GET https://app.pairaphrase.com/apiv2/tms?token=[token]

Response

{"status": 200, "tm": [{"_id": "id", "language pair": "EN / FR", "type":"CSV"}] }

 

Return Translation Memory Segments NEW
Return all translation memory segments that have been generated or added to Pairaphrase.

GET Request

GET https://app.pairaphrase.com/apiv2/tm?token=[token]&id=[tm_id]

Response

{"status": 200, "translation":[{"source": "source_text", "target": "target_text"}, {"source": "source_text", "target": "target_text"}] }

 

Upload Documents for Translation
Prepare a single or batch of files for translation. The immediate response will include the translation ID and word count.

POST Request https://app.pairaphrase.com/apiv2/addfiles?token=[token]

Body / Data (Binary)

document[]=@excel.csv document[]=@books.docx document[]=@resume.pdf

Response

{"status": 200, "result":{ "id":"[document ID]", "status":"Accepted", "word_count":10530 } }

 

Submit File for Translation
Submit a document's ID for full translation. Multiple target languages can be submitted using "target" (e.g., "fr-FR,fr-CA").

GET Request

GET https://app.pairaphrase.com/apiv2/translatefile?token=[token]&id=[document ID]&source=en-US&target=fr-FR

Response

{“status”: 200 }

 

Document Translation Status
Fetch the document translation status as well as the translated document location.

GET Request

GET https://app.pairaphrase.com/apiv2/file?token=[token]&id=[document ID]

Response

{"status": 200, "file": "excel.csv", "file_status":"Ready", "export": "https://..." }

 

Submit Segment into TM or Glossary NEW
Submit an individual modified source/target text to TM or Glossary.

POST Request

POST https://app.pairaphrase.com/apiv2/submitsegment?token=[token]&source=en-US&target=fr-FR&type=tm

Body / Data (JSON)

{"source":"Good day!", "target":"Bonne journée!"}

Response

{"status": 200}

 

Language Detection
Detect a block of text's language.

POST Request

POST https://app.pairaphrase.com/apiv2/detect?token=[token]

Body / Data

text=Hello, my name is Jack. What is your name?

Response

{"status": 200, "detected":"EN" }

 

Return All Documents
Return all documents that have been added to Pairaphrase. Limited to 100 translations per page.

GET Request

GET https://app.pairaphrase.com/apiv2/files?token=[token]&page=0

Response

{"status": 200, "files": [{"_id": "id", "file": "excel.csv", "status":"Ready"}, {"_id": "id", "file": "excel.csv", "status":"Ready"}] }

 

Return Document Segmentation
Return a document's segmentation.

GET Request

GET https://app.pairaphrase.com/apiv2/filesegmentation?token=[token]&id=[document ID]

Response

{"status": 200, "translation":[{"source": "source_text", "target": "target_text"}, {"source": "source_text", "target": "target_text"}] }

 
Return Active Translation Engine NEW
Return the active translation engine being used for translation.

GET Request

GET https://app.pairaphrase.com/apiv2/translationengine?token=[token]

Response

{"status": 200, "active_engine":"microsoftAPI", "available_engines":"microsoftAPI,googleAPI,..." }

 
Set Active Translation Engine NEW
Set the active translation engine to use for translation.

POST Request

POST https://app.pairaphrase.com/apiv2/settranslationengine?token=[token]

Body / Data

engine=googleAPI

Response

{"status": 200}
