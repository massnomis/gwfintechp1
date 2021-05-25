# gwfintechp1
GW defi WhitePaper


Dependencies

Web3.py

https://web3py.readthedocs.io/en/stable/

GraphQL

https://thegraph.com/explorer/subgraph/aave/aave-v2-matic?selected=playground
https://github.com/graphql/graphiql
https://github.com/aave/protocol-v2-subgraph
https://github.com/profusion/sgqlc

APIs

https://thegraph.com/explorer/subgraph/aave/aave-v2-matic?selected=playground
https://aave-api-v2.aave.com/data/markets-data/0xd05e3e715d945b59290df0ae8ef85c1bdb684744

AAVE.js

https://github.com/aave/aave-js
https://github.com/aave/protocol-v2/blob/master/markets/matic/rateStrategies.ts
https://github.com/aave/protocol-v2

Pricing
https://docs.1inch.io/api/
https://towardsdatascience.com/connecting-to-a-graphql-api-using-python-246dda927840

Development
Calling Data
Lending Data
Borrowing Data
Price Data
Market Data 
Gas Data

Formatting Data
Format data to help make decisions

Strategy Table
We need a list of strategies and the math with them 
User input for stratgiers

Notification Suite
Tell user, maybe show user the options

Execution Suite
Actually execute it on chain
Testing
Historical - Go through compound, aave rates backtest strategies

May need SQL for this

Monte carlo testing on positions (Yonathan)














import requests
import json
import pandas as pd
query = """query {  
  reserves(first:10) {
    symbol
    name
    price {
      priceHistory (first: 10) {
        id
        asset {
          id
        }
        price
        timestamp
      }
    }
    stableBorrowRate
    variableBorrowRate
  }
}"""
url = 'https://api.thegraph.com/subgraphs/name/aave/aave-v2-matic'
r = requests.post(url, json={'query': query})
print(r.status_code)
print(r.text)
json_data = json.loads(r.text)
df_data = json_data['data']['reserves']
df = pd.DataFrame(df_data)
df


