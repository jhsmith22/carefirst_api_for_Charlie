## Bash commands to setup endpoint. Inside carefirst_api folder:

## 0. Update the .env file with your own OPENAI API Key (it's okay if you are do a couple pings using mine, but for lots, please use your own)
OPENAI_API_KEY=

## 1. Setup Poetry Environment
poetry shell

## 2. Start app (yes there are a bunch of warnings about depreciated langchain packages)
 poetry run uvicorn src.main:app 

## Should be good to go. Now you can ping the endpoint. Test it with this. Should return 200
curl -o /dev/null -s -w "%{http_code}\n" -X POST "http://localhost:8000/conversations/9999" -H 'Content-Type: application/json' -d \
'{"query": "how should i treat a bee sting"}'

## Example python code to get response from endpoint

conversation_id = '9999'
URL = 'http://localhost:8000/conversations/' + conversation_id

json = {'query': 'how deep is my cut?'}
r = requests.post(url=URL, json=json)
response = r.text
print(response)