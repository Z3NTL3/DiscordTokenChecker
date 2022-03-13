# DiscordTokenChecker
A Discord multiple Tokens validity Checker

# Usage
```comment
Load your tokens into tokens.txt
python3 tokencheck.py

The tool will save all the working tokens into 'goods.txt'
```
# Image
![Screenshot_1](https://user-images.githubusercontent.com/48758770/158063431-b412eed0-214b-46ee-8c4f-58ce5d7e9483.png)

# Source:
For github newbies belike
```python
import threading
import requests


def GetTokens():
    l = open('tokens.txt','r').read().strip(' ').split('\n')
    return l

TOKENS = GetTokens()
API = f"https://discord.com/api/oauth2/authorize"

valids = 0

def Check(*, token):
    global valids
    r = requests.post(API, headers={'Authorization': f'{token}'})
    response = r.content.decode('utf-8')

    if r'{"client_id": ["This field is required"], "scope": ["This field is required"]}' in response:
        token_check = True
        v = '\033[32mValid\033[0m'
        valids += 1
    else:
        token_check = False
        v = '\033[31mInvalid\033[0m'

    if token_check:
        with open('goods.txt','w')as w:
            w.write(f'{token}\n')

    print(f"{token} > {v}")
def Start():
    with open('tokens.txt','r')as q:
        lines = len(q.readlines())

    amount = lines

    print(f"""
[ Discord Token Checker ]
         Z3NTL3

Checking \033[36m{amount}\033[0m token amounts

""")

   
    for t in TOKENS:
        th = threading.Thread(target=Check(token=t))
        th.start()
    print(f"""
[ Process Ended ]
Valids: {valids}
""")
if __name__ == '__main__':
    Start()

# Do not forget to create a 'tokens.txt' file next to the location of this tool with your tokens being pasted in the tokens.txt file.
```
