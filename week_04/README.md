# Monitoring the Performance of LLM

This week's project involves presenting and monitoring the performance of LLMs using Grafana.

## How to start the app

1. Change directory to the folder `app` and run the following command:

```bash
docker compose up
```

2. When the app is ready (not generating logs anymore), run the `prep.py` script to setup the Elasticsearch index and postgreSQL database.

```bash
python prep.py
```

3. Pull `Phi-3` model in the `ollama` container.

```bash
docker exec -it ollama ollama pull phi3
```

## Check the app is running

Visit http://localhost:8501 to see a Q&A app running. You can ask a question and view the model's response.


## Monitoring performance on Grafana

1. Run the `generate_data.py` script to generate data for Grafana.
```bash
python generate_data.py
```

When you feel the data is sufficient, you can stop the script by pressing `Ctrl + C`.

2. Visit http://localhost:3000 to view the Grafana dashboard. The username and password are both `admin` by default.

3. Using the hamburger menu on the top left, you can add a new connection to the PostgreSQL database.
![Imgur](https://imgur.com/kqzrtpC.jpg)
The connection details are as follows: 
HostURL: `postgres`
Database Name: `course_assistant`
Username: `your_username`
Password: `your_password`
TSL/SSL: `disable`

1. Once the connection is established, you can query data and create visualizations.
![Imgur](https://imgur.com/HEjjozV.jpg)
Select `grafana-postgresql-datasource` as the source. Then, switch to the `Code` tab, where you can write SQL queries to fetch data from the database. Here's an example query
    ```sql
    SELECT
    model_used,
    COUNT(*) as count
    FROM conversations
    GROUP BY model_used
    ```
    After running the query, you can either create your own visualization or choose from the suggested options.
    ![Imgur](https://imgur.com/pGYPJgv.jpg)

1. You can query data from different tables and create a dashboard to monitor the performance of the LLMs.

## Stop the app

Run the following command to stop the app:

```bash
docker compose down
```