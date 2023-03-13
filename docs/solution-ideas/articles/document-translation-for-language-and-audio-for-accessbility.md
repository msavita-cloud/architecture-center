[!INCLUDE [header_file](../../../includes/sol-idea-header.md)]

This solution idea explains how to leverage [Azure Cognitive Services](https://learn.microsoft.com/en-us/azure/cognitive-services/) in a user-friendly manner by offering options for translation of documents, accommodating both language and audio preferences to meet accessibility standards and reach a global audience.

## Architecture

<B>Without OpenAI</B>
![Diagram that shows how to ingest, extract and translate documents in language and audio.](https://github.com/msavita-cloud/architecture-center/blob/main/docs/solution-ideas/media/document-translation-for-language-and-audio-for-accessbility.png)

<B>With OpenAI</B>
![Open AI Summarization and gain further insights.](https://github.com/msavita-cloud/architecture-center/blob/main/docs/solution-ideas/media/document-translation-for-language-and-audio-for-accessbility-openai.svg)

*Download a [file](https://arch-center.azureedge.net/document-translation-for-language-and-audio-for-accessbility.vsdx) of this architecture.*

### Dataflow
 
Here is the process:

1. <B>Ingest</B>: PDF documents, text files, and images can be ingested from multiple sources, such as Azure Blob storage, Outlook, OneDrive, SharePoint, or a 3rd party vendor.

1. <B>Move</B>: PowerAutomate triggers and moves the file to Azure Blob storage. Azure function Blob triggers then get the original file and call an Azure Function.

1. <B>Extract Text and Translate</B>: The Azure Function calls [Azure Computer Vision Read API](https://learn.microsoft.com/en-us/azure/cognitive-services/Computer-vision/how-to/call-read-api) to read multiple pages of a PDF document in natural formatting order, extract text from images, and generate the text with lines and spaces, which is then stored in Azure Blob storage. The [Azure Translator](https://azure.microsoft.com/en-us/products/cognitive-services/translator/) then translates the file and stores it in a blob container. The [Azure Speech](https://azure.microsoft.com/en-us/products/cognitive-services/speech-services/) generates a WAV or MP3 file from the original language and translated language text file, which is also stored in a blob container.

1. <B>Summarize & Extract Insights</B>:[OPTIONAL] Add [HTTP connector](https://learn.microsoft.com/en-us/training/modules/http-connectors/) in PowerAutomate to summarize and gain further insights the original language text file and translated text file.
 
3. <B>Notify</B>: PowerAutomate triggers and moves the file to the original source location and notifies users in outlook and MS teams with an output audio file.

## Alternatives
The Azure architecture utilizes Azure Blob storage as the default option for file storage during the entire process. However, it's also possible to use alternative storage solutions such as Sharepoint, ADLS or third-party storage options. For processing a high volume of documents, consider using Azure Logic Apps as an alternative to PowerAutomate. Azure Logic Apps can prevent you from exceeding consumption limits within your tenant and is a more cost-effective solution. To learn more about Azure Logic Apps, please refer to the [Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-overview).

For OpenAI summarization and further insights Azure function can be used as well.


### Components

These are the key technologies used for this technical content review and research:

* [Azure Translator](https://azure.microsoft.com/en-us/products/cognitive-services/translator/)
* [Azure Computer Vision](https://azure.microsoft.com/services/cognitive-services/computer-vision)
* [Azure Speech](https://azure.microsoft.com/en-us/products/cognitive-services/speech-services/)
* [Azure Function App](https://azure.microsoft.com/en-au/products/functions//)
* [Azure OpenAI](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/)


## Scenario details

This solution uses multiple [Cognitive Services](https://learn.microsoft.com/en-us/azure/cognitive-services/) from Azure to automate the business process of translating PDF documents and creating audio files in wav/mp3 audio format for accessibility and global audience. It's a great way to streamline the translation process and make content more accessible to people who may speak different languages or have different accessibility needs.

### Potential use cases

By leveraging this cloud-based solution idea that can provide comprehensive translation services on demand, organizations can easily reach out to a wider audience without worrying about language barriers. This can help to break down communication barriers and ensure that services are easily accessible for people of all cultures, languages, locations, and abilities.

In addition, by embracing digital transformation, organizations can improve their efficiency, reduce costs, and enhance the overall customer experience. Digital transformation involves adopting new technologies and processes to streamline operations and provide a more seamless experience for customers. 

 It is particularly relevant to industries that have a large customer base or client base, such as e-commerce, tourism, hospitality, healthcare, and government services.

## Contributors

*This article is maintained by Microsoft. It was originally written by the following contributors.*

Principal author:

* [Savita Mittal](https://www.linkedin.com/in/savitamittal) | Senior Cloud Solution Architect

*To see non-public LinkedIn profiles, sign in to LinkedIn.*

## Next steps

* Learn about [extracting data from documents and forms by using OCR and Form Recognizer](/Shows/AI-Show/Extracting-Data-From-Documents-and-Forms-with-OCR-and-Form-Recognizer).
* Explore [Azure OpenAI to gain insights from the documents](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/).


## Related resources

- [Extract PDF context the Computer Vision Read API](https://learn.microsoft.com/en-us/azure/cognitive-services/Computer-vision/how-to/call-read-api)
