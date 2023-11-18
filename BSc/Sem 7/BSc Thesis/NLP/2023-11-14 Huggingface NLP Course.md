## Transformer Models

### Some pipelines

- feature-extraction
- fill-mask
- ner (named entity recognition)
- question-answering
- sentiment-analysis
- summarization
- text-generation
- translation
- zero-shot-classification
	- Classify in one/many specified categories
	- Zero shot: No training for this type of classification
	- Also available in one or many shot with some fine tuning

### Structure

![[transformers.svg]]

- Transfer learning
	- Pre-train + fine tuning
- Encodings
	- Also embeddings, features
- Encoder
	- Receives entire input, builds embedding
	- Encodings include context of words around the encoded word
- Decoder
	- Gets embedding and additional input, generates target sequence
	- Can only "pay attention" to already translated words, in addition to input encoding (vs encoder, that gets input all in one go)
- Encoder-Decoder
	- We may not always have both. Middle connection in particular only exists in encoder-decoder models
	- Can choose different encoders and decoders
- Attention Layers
	- TL;DR Layers that tell the model to pay specific attention to certain words in sentence
	- E.g. "You like this course" EN to FR -> to translate "like", pay attention to only "You" and "like", rest is irrelevant

## Using Huggingface

### Pipeline structure

![[full_nlp_pipeline.svg]]


