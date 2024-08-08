# Chunk 
To concatenate course, section, question and answer

# Tokenization
Use custom code to print out the data to know the progress

# Embedding
The code can take a while to run.

# Export
The connection string is `http://elasticsearch:9200/`

# Trigger
1. Trigger name: Daily document refresh
2. Frequency: Daily
3. Start time and date: sometime in the past
4. Timeout: 3600
5. Status for runs that exceed timeout: Failed
6. Check the box for "Skip run if previous run still in progress"
7. Check the box for "Create initial pipeline run if start date is before current execution period"

Save changes -> Enable trigger
