
Wrote a small python script to check number of transactions and wallet balance, just needed it to run for a couple of days to keep track of some payments.

```
import time
import requests

def check(wallet):
	try:
		page = requests.get("https://blockchain.info/address/"+wallet)
		print "[+] Wallet:" , wallet + " got " + page.text.split('No. Transactions')[1].split("</td>")[1].split('<td id="n_transactions">')[1] + " transactions"
		btc = page.text.split("Final Balance")[1].split('<td id="final_balance">')[1].split('</span>')[0].split(">")
		print "[+] Wallet balance: " + btc[2] + "\n"
	except:
		print "[-] Something went wrong"

wallets = ["16Hz84sGs3xr4vLJZfPjQJAfFso9p5MvR","16buJrpoSNkqmGsjiw5Diws8uYnxEySHSp","16NivQ5sVKJ3kHatP51b44EZFMxMe12RaS","1AdUw4i68CFF3m2zYrjmfhcH4ortjbwVzB"]
while(1):
	for wallet in wallets:
		check(wallet)
	print "[+] Sleeping for 1 hour before checking again"
	time.sleep(3600)


```
The wallets are not mine, just took some random.

Output:

```
[+] Wallet: 16Hz84sGs3xr4vLJZfPjQJAfFso9p5MvR got 1 transactions
[+] Wallet balance: 0.03190556 BTC

[+] Wallet: 16buJrpoSNkqmGsjiw5Diws8uYnxEySHSp got 1 transactions
[+] Wallet balance: 0.03743655 BTC

[+] Wallet: 16NivQ5sVKJ3kHatP51b44EZFMxMe12RaS got 1 transactions
[+] Wallet balance: 0.02361067 BTC

[+] Wallet: 1AdUw4i68CFF3m2zYrjmfhcH4ortjbwVzB got 2 transactions
[+] Wallet balance: 0 BTC

[+] Sleeping for 1 hour before checking again
```
