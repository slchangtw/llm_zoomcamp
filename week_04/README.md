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

2. Visit http://localhost:3000 to view the Grafana dashboard. The username and password are both `admin` by default.

3. Add a new connection to the PostgreSQL database.
HostURL: `postgres`
Database Name: `course_assistant`
Username: `your_username`
Password: `your_password`
TSL/SSL: `disable`

4. Once the connection is established, you can query data and create visualizations on the dashboard.

## Stop the app

Run the following command to stop the app:

```bash
docker compose down
```