A vector database stores data as *embeddings*: lists of numbers that represent meaning.

It is designed for similarity search, meaning it finds items that are semantically close, not only exact keyword matches.

>[!example] 
>A keyword search for “car accident” may miss a document that says “vehicle crash”.


## Embeddings: Meaning to Numbers
An embedding is a numerical representation of data. Text, images, or other content are transformed into vectors in a high-dimensional space. 

Items with similar meaning are placed closer together in that space.

>[!example] 
>- “dog” and “puppy” → vectors close together 
>- “dog” and “airplane” → vectors far apart

## Vector Search
Nearest neighbor search (similarity search):
1) Nearest neighbor search (similarity search):
2) The embeddings are stored in the vector database
3) A user query is also converted into an embedding
4) The database finds the nearest vectors to the query vector
5) The closest results are returned

## How to Make Embeddings?
Embeddings are made by an *embedding model*, a trained neural network that takes input like text, images, audio, or video and converts it into a vector.

## Applications
- Semantic search in documents and websites
- Image and multimedia search
- Recommendation systems
- Fraud detection or anomaly matching in feature space

