# Orchestrating LLM Pipeline using Mage

This week's project involves orchestrating the LLM pipeline using [mage](https://github.com/mage-ai/mage-ai).

## How to start the app

1. Pull the latest version of mage image.

```bash
docker pull mageai/mageai:latest
```

2. Change your directory to the folder `app` and run the following command to start the app.

```bash
./scripts/start.sh
```

3. Open your browser and navigate to [http://localhost:6789](http://localhost:6789) to access the mage dashboard.

## Dashboard Overview

The dashboard comes with default pipelines already created. Navigate to the `Pipelines `tab to view them. You can open any pipeline to see the steps involved.

![Imgur](https://imgur.com/6IR2XEq.jpeg)

## Orchestration Pipeline

The orchestration pipeline consists of the following steps:
1. Ingest
2. Chunk
3. Tokenization
4. Embedding
5. Export

### Ingestion
The ingest step is responsible for reading and storing the data. Navigate to the `Ingest` tab and edit the code in the editor. You can copy the code provided below and paste it directly into the editor. Then, add the link below in the *Endpoint URL* field and execute this code block

> [Code](scripts/ingest.py)

> Endpoint URL: https://raw.githubusercontent.com/DataTalksClub/llm-zoomcamp/main/01-intro/documents.json

![Imgur](https://imgur.com/gm717Hr.jpg)

# Chunking
To produce manageble chunks of data, this step will concatenate the course, section, question, and answer from the ingested documents. Go to the `Chunk` tab and add the code below to the editor and run this block.

> [Code](scripts/chunk.py)

![Imgur](https://imgur.com/Tv5dP5u.jpg)


# Tokenization
This step involves tokenizing and lemmatizing the texts. Navigate to the `Tokenization` tab and select `Lemmatization (spaCy)`. Insert the following code into the editor and execute this block. This code will perform tokenization and lemmatization while displaying the progress.

> [Code](scripts/tokenize.py)

![Imgur](https://imgur.com/a64J1bV.jpg)

# Embedding
This step involves embedding the text using spaCy embeddings. Navigate to the `Embedding tab` and select `spaCy embeddings`. Insert the following code into the editor. This block may take some time to execute.

> [Code](scripts/embed.py)

![Imgur](https://imgur.com/5ODFh5M.jpg)

# Export
To store the embeddings in database for later retrieval, this step will export the embeddings to Elasticsearch. Navigate to the `Export` tab, select `Vector Database`, and then choose `Elasticsearch`. Finally, insert the following code into the editor and the connection string in the *Connection string* field.

> [Code](scripts/export.py)

> Connection string: http://elasticsearch:9200/

![Imgur](https://imgur.com/5ODFh5M.jpg)

# Retrieval
To retrieve the embeddings from the database, navigate to the `Inference` and select `Retrieval` and choose `Iterative retrieval`. Insert the code into the editor and the connection string in the *Connection string* field. You can run this block to get the response.

> [Code](scripts/retrieve.py)

![Imgur](https://imgur.com/S6gYBrE.jpg)

# Setting up a trigger
To schedule the pipeline to run daily, go back to the `Pipelines` tab and click on the `Triggers` button. Add a new trigger using Schedule with the following settings:

1. Trigger name: Daily document refresh
2. Frequency: Daily
3. Start time and date: sometime in the past
4. Timeout: 3600
5. Status for runs that exceed timeout: Failed
6. Check the box for *Skip run if previous run still in progress*
7. Check the box for *Create initial pipeline run if start date is before current execution period*

After setting up the trigger, you can save the changes and enable the trigger. You can run the pipeline manually to see the results.

![Imgur](https://imgur.com/tUDdWLe.jpg)
