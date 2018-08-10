# [Learn Blockchains by Building One](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46)
The fastest way to learn how Blockchains work is to build one.

You’re here because, like me, you’re psyched about the rise of Cryptocurrencies. And you want to know how Blockchains work—the fundamental technology behind them.

我们因为同样的对于加密钱币的激动与兴趣来到这里，并且同样想知道区块链工作所依赖的基础技术。

But understanding Blockchains isn’t easy—or at least wasn’t for me. I trudged through dense videos, followed porous tutorials, and dealt with the amplified frustration of too few examples.

但是理解区块链并不容易，至少对我是这样的。我在多如繁星的视频和教程中穿梭，简单的几个例子却给了我巨大的挫折感。

I like learning by doing. It forces me to deal with the subject matter at a code level, which gets it sticking. If you do the same, at the end of this guide you’ll have a functioning Blockchain with a solid grasp of how they work.

我喜欢在编码中学习，从而迫使自己在代码基本处理问题并坚持下去，在教程的最后，我们将拥有一个功能正常的区块链，从而使我们牢牢掌握其工作原理。

## Before you get started…

Remember that a blockchain is an immutable, sequential chain of records called Blocks. They can contain transactions, files or any data you like, really. But the important thing is that they’re chained together using hashes.

If you aren’t sure what a hash is, [here’s an explanation](https://learncryptography.com/hash-functions/what-are-hash-functions).

Who is this guide aimed at? You should be comfy reading and writing some basic Python, as well as have some understanding of how HTTP requests work, since we’ll be talking to our Blockchain over HTTP.

What do I need? Make sure that [Python 3.6+](https://www.python.org/downloads/) (along with `pip`) is installed. You’ll also need to install Flask and the wonderful Requests library:

```
pip install Flask==0.12.2 requests==2.18.4 
```

Oh, you’ll also need an HTTP Client, like [Postman](https://www.getpostman.com/) or cURL. But anything will do.

Where’s the final code? The source code is [available here](https://github.com/dvf/blockchain).

## Step 1: Building a Blockchain

Open up your favourite text editor or IDE, personally I ❤️ [PyCharm](https://www.jetbrains.com/pycharm/). Create a new file, called `blockchain.py`. We’ll only use a single file, but if you get lost, you can always refer to the [source code](https://github.com/dvf/blockchain).

### Representing a Blockchain

We’ll create a `Blockchain` class whose constructor creates an initial empty list (to store our blockchain), and another to store transactions. Here’s the blueprint for our class:

```

class Blockchain(object):
    def __init__(self):
        self.chain = []
        self.current_transactions = []
        
    def new_block(self):
        # Creates a new Block and adds it to the chain
        pass
    
    def new_transaction(self):
        # Adds a new transaction to the list of transactions
        pass
    
    @staticmethod
    def hash(block):
        # Hashes a Block
        pass

    @property
    def last_block(self):
        # Returns the last Block in the chain
        pass
```

Our `Blockchain` class is responsible for managing the chain. It will store transactions and have some helper methods for adding new blocks to the chain. Let’s start fleshing out some methods.

### What does a Block look like?

Each Block has an index, a timestamp (in Unix time), a list of transactions, a proof (more on that later), and the hash of the previous Block.

Here’s an example of what a single Block looks like:
```
block = {
    'index': 1,
    'timestamp': 1506057125.900785,
    'transactions': [
        {
            'sender': "8527147fe1f5426f9dd545de4b27ee00",
            'recipient': "a77f5cdfa2934df3954a5c7c7da5df1f",
            'amount': 5,
        }
    ],
    'proof': 324984774000,
    'previous_hash': "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
}
```
At this point, the idea of a chain should be apparent—each new block contains within itself, the hash of the previous Block. This is crucial because it’s what gives blockchains immutability: If an attacker corrupted an earlier Block in the chain then all subsequent blocks will contain incorrect hashes.

Does this make sense? If it doesn’t, take some time to let it sink in—it’s the core idea behind blockchains.

### Adding Transactions to a Block

We’ll need a way of adding transactions to a Block. Our new_transaction() method is responsible for this, and it’s pretty straight-forward:

```
class Blockchain(object):
    ...
    
    def new_transaction(self, sender, recipient, amount):
        """
        Creates a new transaction to go into the next mined Block
        :param sender: <str> Address of the Sender
        :param recipient: <str> Address of the Recipient
        :param amount: <int> Amount
        :return: <int> The index of the Block that will hold this transaction
        """

        self.current_transactions.append({
            'sender': sender,
            'recipient': recipient,
            'amount': amount,
        })

        return self.last_block['index'] + 1
```
After new_transaction() adds a transaction to the list, it returns the index of the block which the transaction will be added to—the next one to be mined. This will be useful later on, to the user submitting the transaction.

--- more ---

please go to [source page.](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46)

