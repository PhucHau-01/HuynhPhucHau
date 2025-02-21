Provide your CLI command here:
grep '"symbol": "TSLA"' transaction-log.txt | grep '"side": "sell"' | jq -r '.order_id' | xargs -I {} curl -s https://example.com/api/{} >> output.txt
