# Furniture store product extraction

## Fine-tuned fast model 
We fine-tuned the "fast" tagger from Flair, which was pre-trained on the Ontonotes NER dataset (containing the PRODUCT entity). This model uses an ensemble of classical embeddings, with some Linear layers and an LSTM on top. We trained this model with stochastic weight averaging.
### Pros:
- It has a high precision in finding furniture products.
### Cons:
- It sometimes misses simple, obvious product names;
- It has a tendecy to find very long product names.

## Pre-trained large model
This model is also pre-trained on the Ontonotes NER dataset. It uses XLM-RoBERTa embeddings, followed by a linear layer.

### Pros:
- It has a high recall in finding products.
### Cons:
- It's not fine-tuned on furniture stores, so it tags sequences such as "Google Chrome" as products;
- It has a tendecy to cut product names too short.

## Ensemble
Since these models are so complementary, we use both of them for tagging and filter their predictions by confidence and sequence length. We also use a short blacklist (made up 5 words), in order to mitigate RoBERTa's mistakes. This way, we're able to obtain a strong model.

## Examples:

### Raw product extraction from annotated pages:
- "Cirrus LED Reading Light"   [− Labels: PRODUCT (0.9977)]
- "Beadlight"   [− Labels: PRODUCT (0.9097)]

- "Eames Style"   [− Labels: PRODUCT (0.7843)]
- "Waterfall Seat Edge"   [− Labels: PRODUCT (0.9779)]
- "Waterfall"   [− Labels: PRODUCT (0.8756)]

- "American Oak Side Table"   [− Labels: PRODUCT (0.9974)]

- "The Layabout Suite"   [− Labels: PRODUCT (0.9993)]
- "Modular Lounge"   [− Labels: PRODUCT (0.8485)]
- "Bronte Left Hand Chaise"   [− Labels: PRODUCT (0.8429)]
- "Playpen"   [− Labels: PRODUCT (0.8059)]

### Raw product extraction from new pages:
- "Mattress"   [− Labels: PRODUCT (0.8336)]

- "Toby Chairs"   [− Labels: PRODUCT (0.9625)]
- "The Oak Toby Tables"   [− Labels: PRODUCT (0.9963)]
- "Toby Chairs"   [− Labels: PRODUCT (0.9146)]
- "The Oak Toby Tables"   [− Labels: PRODUCT (0.8587)]
- "Toby Tables"   [− Labels: PRODUCT (0.964)]
- "The Oak Toby Tables"   [− Labels: PRODUCT (0.8257)]

- "Tulip Side Chair"   [− Labels: PRODUCT (0.9991)]
- "Tulip Arm Chair"   [− Labels: PRODUCT (0.9993)]
- "Tulip Chair"   [− Labels: PRODUCT (0.9988)]
- "the Tulip"   [− Labels: PRODUCT (0.9001)]
- "Tulip Table"   [− Labels: PRODUCT (0.9998)]
 
- "Stressless Reno Recliner Chair"   [− Labels: PRODUCT (0.9976)]
- "Footstool"   [− Labels: PRODUCT (0.9033)]
- "Stressless"   [− Labels: PRODUCT (0.9871)]

- "Solar Ball Stake Light"   [− Labels: PRODUCT (0.9695)]
)]

- "Leather Crank Stool"   [− Labels: PRODUCT (0.9999)]
