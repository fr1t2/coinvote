# coinvote
Coin-weighted vote tracking

Work-in-progress

Proof-of-concept scripts which tracks specific message_tx in the QRL blockchain. Specific ID's may be supplied and the vote weighting of the emitted coin supply is displayed real time by coinvote.py

Data of ongoing message_tx ID's is pickled into a file, to be parsed by coinvoteread.py.

## Requirements

This package requires Python 3.5 and pyqrlib to work. Install with 

`sudo apt-get install -y python3.5`

Then for the pyqrlib

`pip3 install -U pyqrllib`


To speed up connections you may want to run a local node. See the [QRL Docs](https://docs.theqrl.org) for instructions for this. YOu will also need to change the configuration to reflect the local node. 


## Usage

This script checks the QRL Blockchain for any message that contains the parameters you enter in the configuration. This allows users to vote on a topic by signing a message onto the network. Every vote is weighted based on the amount of coins in the wallet.


Clone the repo, and enter the directory. Once installed it is as simple as running the coinvote.py script and letting it scrape the chain. 

`python3.5 coinvote.py` this will run for awhile, and once caught iup will continue to look for new votes in any found blocks. I recomend running this in a screen session or in background process.

Once you have scraped the chain, run the `coinvoteread.py` script to collect the results. By default the script is setup tp find `ID_001` and `ID_002` in the chain. You will want to change the parameters for your vote accordingly.


## Configuration


#### Node Config

The Node configuration is located in the `q.py` file.

To connect to a locally run node, change the address located on line 20 from
`def __init__(self, node='35.178.79.137:19009', verbose=False):`

to this:

`def __init__(self, node='127.0.0.1:19009', verbose=False): `


### Script Config

you can scan the entire chain in sub 30 minutes by switching your sleep down to 0.01 - 0.005s in `coinvote.py`

change the line:
`time.sleep(0.75)`

to
`time.sleep(0.05)`


Change info in this line to configure what the script looks for in votes.
`ID = ['ID_0001', 'ID_0002']`

for example, we are using this to track if we should wear blue, or red socks we would ask people to vote with a signed message stating either:

`socks-vote-RED` for red socks

`socks-vote-BLUE` for blue socks.

so in the configuration file enter;
`ID = ['socks-vote-RED', 'socks-vote-BLUE']`

Run the `coinvote.py` script and leav running. this will scrape the chain from the blockheight stated and collect any results. To see what the results are, run the `coinvoteread.py` script.


Set the starting blockheight to track the chain from with variable blocks. No need to look any time before you started the vote. Enter the blockheight to start looking for votes.

`blocks = 175000`
