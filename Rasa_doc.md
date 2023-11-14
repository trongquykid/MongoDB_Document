# **Tuning Your NLU Model**
## **Choose a Pipeline**

- In Rasa, incoming messages are processed by a sequence of components. These components are executed one after another in a so-called processing pipeline defined in your config.yml. Choosing an NLU pipeline allows you to customize your model and finetune it on your dataset.

    ### Doing Multi-Intent Classification
    - To do multi-intent classification, you need to use the [**DIETClassifier**](https://rasa.com/docs/rasa/components#dietclassifier) in your pipeline. You'll also need to define these flags in whichever tokenizer you are using
        - *intent_tokenization_flag*: Set it to True, so that intent labels are tokenized.
        - *intent_split_symbol*: Set it to the delimiter string that splits the intent labels. In this case +, default _
    ### DIETClassifier
    - Dual Intent Entity Transformer (DIET) used for intent classification and entity extraction
    - Output-Example:

    ```
    {
        "intent": {"name": "greet", "confidence": 0.7800},
        "intent_ranking": [
            {
                "confidence": 0.7800,
                "name": "greet"
            },
            {
                "confidence": 0.1400,
                "name": "goodbye"
            },
            {
                "confidence": 0.0800,
                "name": "restaurant_search"
            }
        ],
        "entities": [{
            "end": 53,
            "entity": "time",
            "start": 48,
            "value": "2017-04-10T00:00:00.000+02:00",
            "confidence": 1.0,
            "extractor": "DIETClassifier"
        }]
    }
    ```
    - Configuration:
        > If you want to use the DIETClassifier just for intent classification, set *entity_recognition* to False. If you want to do only entity recognition, set intent_classification to False. By default DIETClassifier does both, i.e. *entity_recognition* and intent_classification are set to True.
    
    - More configurable parameters: [DIETClassifier](https://rasa.com/docs/rasa/components#dietclassifier)

# **Pipeline Components**
## **Language Model**
- [MitieNLP](https://rasa.com/docs/rasa/components#mitienlp)
- [SpacyNLP](https://rasa.com/docs/rasa/components#spacynlp)
## **Tokenizers**
- [WhitespaceTokenizer](https://rasa.com/docs/rasa/components#whitespacetokenizer)
- [JiebaTokenizer](https://rasa.com/docs/rasa/components#jiebatokenizer)
- [MitieTokenizer](https://rasa.com/docs/rasa/components#mitietokenizer)
- [SpacyTokenizer](https://rasa.com/docs/rasa/components#spacytokenizer)
## **Intent Classifiers**
- [MitieIntentClassifier](https://rasa.com/docs/rasa/components#mitieintentclassifier)
- [LogisticRegressionClassifier](https://rasa.com/docs/rasa/components#logisticregressionclassifier)
- [SklearnIntentClassifier](https://rasa.com/docs/rasa/components#sklearnintentclassifier)
- [KeywordIntentClassifier](https://rasa.com/docs/rasa/components#keywordintentclassifier)
- [DIETClassifier](https://rasa.com/docs/rasa/components#dietclassifier)
- [FallbackClassifier](https://rasa.com/docs/rasa/components#fallbackclassifier)
