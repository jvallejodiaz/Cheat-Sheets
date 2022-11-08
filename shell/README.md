# Shell

## Script to wait until we get a response

```@bash 
while [[ "$(curl --silent -L 'http://127.0.0.1:9500/_cluster/health' | jq -e '.status')" != *"green"* ]]; do
    echo "Elasticsearch status is: $(curl --silent -L 'http://localhost:9200/_cluster/health' | jq -e '.status')"
    echo "Waiting for ES to be ready. Sleeping for 30 seconds..."
    ((c++)) && ((c==10)) && break
    sleep 30
done

```