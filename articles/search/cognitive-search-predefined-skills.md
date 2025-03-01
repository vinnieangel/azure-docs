---
title: Built-in text and image processing during indexing
titleSuffix: Azure Cognitive Search
description: Data extraction, natural language, and image processing skills add semantics and structure to raw content in an Azure Cognitive Search enrichment pipeline.

author: HeidiSteen
ms.author: heidist
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 09/09/2022
---
# Built-in skills for text and image processing during indexing (Azure Cognitive Search)

This article describes the skills provided with Azure Cognitive Search that you can include in a [skillset](cognitive-search-working-with-skillsets.md) to extract content and structure from raw unstructured text and image files. A *skill* is an atomic operation that transforms content in some way. Often, it is an operation that recognizes or extracts text, but it can also be a utility skill that reshapes the enrichments that are already created. Typically, the output is text-based so that it can be used in full text queries. 

## Built-in skills

Built-in skills are based on pre-trained models from Microsoft, which means you cannot train the model using your own training data. Skills that call the Cognitive Resources APIs have a dependency on those services and are billed at the Cognitive Services pay-as-you-go price when you [attach a resource](cognitive-search-attach-cognitive-services.md). Other skills are metered by Azure Cognitive Search, or are utility skills that are available at no charge.

The following table enumerates and describes the built-in skills.

| OData type  | Description | Metered by |
|-------|-------------|-------------|
|[Microsoft.Skills.Text.CustomEntityLookupSkill](cognitive-search-skill-custom-entity-lookup.md) | Looks for text from a custom, user-defined list of words and phrases.| Azure Cognitive Search ([pricing](https://azure.microsoft.com/pricing/details/search/)) |
| [Microsoft.Skills.Text.KeyPhraseExtractionSkill](cognitive-search-skill-keyphrases.md) | This skill uses a pretrained model to detect important phrases based on term placement, linguistic rules, proximity to other terms, and how unusual the term is within the source data. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.LanguageDetectionSkill](cognitive-search-skill-language-detection.md)  | This skill uses a pretrained model to detect which language is used (one language ID per document). When multiple languages are used within the same text segments, the output is the LCID of the predominantly used language. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.MergeSkill](cognitive-search-skill-textmerger.md) | Consolidates text from a collection of fields into a single field.  | Not applicable |
| [Microsoft.Skills.Text.V3.EntityLinkingSkill](cognitive-search-skill-entity-linking-v3.md) | This skill uses a pretrained model to generate links for recognized entities to articles in Wikipedia. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.V3.EntityRecognitionSkill](cognitive-search-skill-entity-recognition-v3.md) | This skill uses a pretrained model to establish entities for a fixed set of categories: `"Person"`, `"Location"`, `"Organization"`, `"Quantity"`, `"DateTime"`, `"URL"`, `"Email"`, `"PersonType"`, `"Event"`, `"Product"`, `"Skill"`, `"Address"`, `"Phone Number"` and `"IP Address"` fields. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.PIIDetectionSkill](cognitive-search-skill-pii-detection.md)  | This skill uses a pretrained model to extract personal information from a given text. The skill also gives various options for masking the detected personal information entities in the text.  | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.V3.SentimentSkill](cognitive-search-skill-sentiment-v3.md)  | This skill uses a pretrained model to assign sentiment labels (such as "negative", "neutral" and "positive") based on the highest confidence score found by the service at a sentence and document-level on a record by record basis. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Text.SplitSkill](cognitive-search-skill-textsplit.md) | Splits text into pages so that you can enrich or augment content incrementally. | Not applicable |
| [Microsoft.Skills.Text.TranslationSkill](cognitive-search-skill-text-translation.md) | This skill uses a pretrained model to translate the input text into a variety of languages for normalization or localization use cases. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Vision.ImageAnalysisSkill](cognitive-search-skill-image-analysis.md) | This skill uses an image detection algorithm to identify the content of an image and generate a text description. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) | 
| [Microsoft.Skills.Vision.OcrSkill](cognitive-search-skill-ocr.md) | Optical character recognition. | Cognitive Services ([pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)) |
| [Microsoft.Skills.Util.ConditionalSkill](cognitive-search-skill-conditional.md) | Allows filtering, assigning a default value, and merging data based on a condition. | Not applicable |
| [Microsoft.Skills.Util.DocumentExtractionSkill](cognitive-search-skill-document-extraction.md) | Extracts content from a file within the enrichment pipeline. | Azure Cognitive Search ([pricing](https://azure.microsoft.com/pricing/details/search/))
| [Microsoft.Skills.Util.ShaperSkill](cognitive-search-skill-shaper.md) | Maps output to a complex type (a multi-part data type, which might be used for a full name, a multi-line address, or a combination of last name and a personal identifier.) | Not applicable |

## Custom skills

[Custom skills](cognitive-search-custom-skill-web-api.md) are modules that you design, develop, and deploy to the web. You can then call the module from within a skillset as a custom skill.

| Type  | Description | Metered by |
|-------|-------------|-------------|
| [Microsoft.Skills.Custom.WebApiSkill](cognitive-search-custom-skill-web-api.md) | Allows extensibility of an AI enrichment pipeline by making an HTTP call into a custom Web API | None unless your solution uses a metered Azure service |
| [Microsoft.Skills.Custom.AmlSkill](cognitive-search-aml-skill.md) | Allows extensibility of an AI enrichment pipeline with an Azure Machine Learning model | None unless your solution uses a metered Azure service |

For guidance on creating a custom skill, see [Define a custom interface](cognitive-search-custom-skill-interface.md) and [Example: Creating a custom skill for AI enrichment](cognitive-search-create-custom-skill-example.md).

## See also

+ [How to define a skillset](cognitive-search-defining-skillset.md)
+ [Custom Skills interface definition](cognitive-search-custom-skill-interface.md)
+ [Tutorial: Enriched indexing with AI](cognitive-search-tutorial-blob.md)
