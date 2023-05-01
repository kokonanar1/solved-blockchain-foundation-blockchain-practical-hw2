Download Link: https://assignmentchef.com/product/solved-blockchain-foundation-blockchain-practical-hw2
<br>
Before we begin, let us go over a few things first:

<ul>

 <li>To use the given code, either use PyCharm and automatically install the requirements or run <strong>pip install -r requirements.txt </strong>to do so. Note that the codes are only compatible with <strong>Python3</strong>.</li>

 <li>All codes must be in the same folder, including the codes you will add. Otherwise they won’t work. The codes provided are already in the same folder, But when you add your own files, take this into consideration.</li>

 <li>We are going to submit transactions on the Bitcoin network and learn the Bitcoin script along the way. Since Bitcoins are a bit costly, we will be working with the testnet<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> • First we are going to generate key pairs for you, Alice and Bob on the Bitcoin Testnet. Using lib/keygen.py, generate private keys for my private key, alice secret key BTC and bob secret key BTC, and record these keys in lib/config.py. Note that Alice and Bob’s keys will only come into play for question 6. Please make sure to create different keys for Alice and Bob, you wouldn’t want them to be able to forge each others’ transactions!</li>

 <li>Next, we want to get some test coins for my private key and alice secret key BTC. To do so:

  <ol>

   <li>Go to the Bitcoin Testnet faucet <a href="https://coinfaucet.eu/en/btc-testnet/"><strong>this faucet</strong></a><a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> and paste in the corresponding addresses of the users. Note that faucets will often rate-limit requests for coins based on Bitcoin address and IP address, so try not to lose your test Bitcoin too often.</li>

   <li>Record the transaction hash the faucet provides, as you will need it for the next step. Viewing the transaction in a block explorer <a href="https://live.blockcypher.com/btc-testnet/"><strong>blockcypher</strong></a> will also let you know which output of the transaction corresponds to your address, and you will need this utxo index for the next step as well.</li>

  </ol></li>

 <li>The <strong>faucet </strong>doesn’t allow you to try too many times and it might block or delay your Bitcoin address and/or IP address. Since you are going to need a lot of TX outputs for the following parts, we suggest you use <strong>split test coins.py </strong>to split the given output to many parts. A perfect run needs around 15 outputs but we suggest 30 to give room for error. Split Alice’s coins as well.</li>

 <li>Next, we are going to create generate key pairs for Alice and Bob on the BlockCypher testnet.

  <ol>

   <li>Sign up for an account with Blockcypher to get an API token <a href="https://accounts.blockcypher.com/">here</a>.</li>

   <li>Create BCY testnet keys for Alice and Bob and place into lib/config.py.(run this command in cmd!)</li>

  </ol></li>

</ul>

<h1>curl -X POST https://api.blockcypher.com/v1/bcy/test/addrs?token=$YOURTOKEN</h1>

<ul>

 <li>Give Bob’s address bitcoin on the Blockcypher testnet (BCY) to get some funds. <strong>curl -d ‘</strong>{<strong>“address”: “BOBS BCY ADDRESS”, “amount”: 1000000</strong>}<strong>’ https://api.blockcypher.com/v1/bcy/test/faucet?token=$YOURTOKEN Note: </strong>if you are using windows cmd use this code instead <strong>curl -d “</strong>{<strong>“address</strong><strong>”: </strong><strong>“BOBS BCY ADDRESS</strong><strong>”, </strong><strong>“amount</strong><strong>”: 1000000</strong>}<strong>” https://api.blockcypher.com/v1/bcy/test/faucet?token=$YOURTOKEN</strong></li>

 <li>Let’s also split Bob’s coins using split test coins.py. Make sure to edit the parameters at the bottom of the file. Each time you are switching between the Bitcoin and BlockCypher testnets, make sure to visit lib/config.py and adjust the network type variable. Make sure to record the transaction hash.</li>

 <li>Be very careful about uppercase and lowercase letters. Python is case sensitive and so is the framework where the codes are prepared upon.</li>

</ul>

<h1>Acknowledgment</h1>

The code provided is based on a course project code in CS251 Stanford. We like to thank the instructors and their assistants, whose endeavors made the preparation of this homework easier.

<h1>Problem 1 – Standard Bitcoin Script</h1>

To start, we are going to write a standard transaction script that is used everywhere. Major parts of the code is already provided in <strong>ex1.py</strong>. Complete the <strong>TODO </strong>parts and run the code. You will get the transaction data. Copy the transaction hash and use it to find the transaction in <strong>blockcypher</strong>. If it is confirmed, copy this hash to <strong>transactions.py</strong>. You will repeat similar steps in the next problems as well.

<strong>Hint: </strong>Just put the appropriate script commands and variables in <strong>return </strong>part of the function. For example: return [OP DUP,address,OP HASH160,OP EQUALVERIFY] (This is not the right answer!!)

<h1>Problem 2 – Linear Redeemer</h1>

A student has suggested his own protocol to redeem an output. Redeeming will happen when the solution (x, y) to the following set of linear equations have been found and submitted in the

ScriptSig:

<em>x </em>+ <em>y </em>= <em>the first half of your studentID x </em>− <em>y </em>= <em>the second half of your studentID</em>

(If x and y turn out to be fractional, add or subtract one value from your Student ID to make sure the solution is integer.)

In this part, you will edit <strong>ex2a.py </strong>and <strong>ex2b.py</strong>, where in <strong>ex2a.py </strong>you will make a transaction that can only be redeemed with the solution and in <strong>ex2b.py</strong>, you will redeem it to verify that your script works. Your scripts should be as small as possible. Note that the ScriptSig must only consist of pushing x and y to the stack. Don’t forget to add the hashes of the produced transactions to <strong>transactions.py</strong>.

<h1>Problem 3 – Bitcoin company</h1>

Faraz and Ata want to start a company together. They have decided to put their companies funds in the Bitcoin blockchain to invest in cryptocoins and also show how up to date they are. They decided to use the MULTISIG feature of the Bitcoin script, such that if both sides agree, the transaction is confirmed.

After some years the company grew and now has 5 other shareholders. They changed their policy and now each transaction is confirmed if:

<ol>

 <li>Faraz and Ata both agree on the transaction.</li>

 <li>Either Faraz or Ata and 3 other shareholders agree on the transaction.(note that shareholderscan not spend the funds without agreeing with Ata or Faraz)</li>

</ol>

1.Using conditional branches (OP IF) implement a script code for the company’s policy by creating two transactions for the idea In this solution, the first one creates an output that can only be redeemed by the way you proposed. The second transaction redeems that output, with the method you proposed, to verify your idea works.

2.Now suppose Faraz and Ata are having problems and never can agree on a transaction (case <strong>i </strong>never happens); implement a script code for the case <strong>ii </strong>without using conditional branches (OP IF).

Copy the code from <strong>ex2a.py </strong>to <strong>ex31a.py </strong>and <strong>ex32a.py </strong>and copy the content of <strong>ex2b.py </strong>to <strong>ex31b.py </strong>and <strong>ex32b.py</strong>. Modify the codes to make the two transactions.

The modification may require you to change parts beyond than the <strong>TODO </strong>parts, possibly even functions that are defined in <strong>utils.py</strong>. Don’t change <strong>utils.py </strong>though. Copy the function declaration to the new files and proceed from there.

Don’t forget to copy the transaction hashes to <strong>transactions.py</strong>.

<h1>Problem 4 – Happy Birthday</h1>

<ol>

 <li>Uncle Saeed decided to give a birthday present for his nephew, Hamed, so when his birthdaycomes, he can use the money. After getting introduced to Bitcoins, he has become extremely fond of this technology and decided to put the funds in the Bitcoin blockchain. Propose a way he can make sure Hamed can’t use the bitcoins sent to her address before his birthday, even if he has the private key.</li>

</ol>

After this, copy the code from <strong>ex2a.py </strong>and <strong>ex2b.py </strong>to <strong>ex4a.py </strong>and <strong>ex4b.py </strong>respectively. Modify the codes to make two transactions. One whose output cannot be redeemed until a specific time in the future. One who redeems that output after the specified time. Again, like before, write the hashes of these transactions in <strong>transcations.py</strong>

The modification might mean you have to change codes further than the <strong>TODO </strong>parts, possibly even functions that are defined in <strong>utils.py</strong>. Don’t change <strong>utils.py </strong>though. Copy the function declaration to <strong>ex4a.py </strong>or <strong>ex4b.py </strong>and proceed from there.(150 points)

<ol start="2">

 <li>His other uncle, Homayoun, wants to write a happy birthday letter to Hamed. He found outthat you can put messages on bitcoin’s blockchain and they last for as long as bitcoin lasts. He really liked the idea and decided to put the happy birthday message on bitcoin.</li>

</ol>

Write a python code (<strong>happybirthday.py</strong>) to help Homayoun by getting a costume message as an input and putting it on bitcoin’s blockchain. Try your code with ’Happy Birthday Hamed’ and save the transaction hash in <strong>transactions.py</strong>

<h1>Problem 5 – I have it</h1>

Salar wrote an incredible article recently and decided to have it published in Nature in a few months. Mohammad told him that if he proves he has the article right now, Mohammad will give him 400$ . Salar has known Mohammad for a long time and knows that if he gives the article to him, he will publish it with his own name. Yet he still wants that 400$. Easy enough, he computes the hash of the article he wrote and gives it to MOhammad, and tells him to check if the hash is valid when it is published. Mohammad doesn’t accept this and says he is not organized enough to keep the hash for a few months and find it at that time and will probably lose the hash. Salar knows Mohammad likes Bitcoins. He also wants the 400$. Salar thought of this solution:

<ul>

 <li>Salar uses the <em>SHA</em>256 hash of the file to construct an address (using the algorithm that can generate an address based on public keys) and sends 1 satoshi to it</li>

</ul>

<h1>Part 1</h1>

Write a Python scripts (<strong>fileverify.py</strong>) who take an input file and implement the two ideas. Try your script with the file <strong>data.hex</strong>. Save the transaction hashes in <strong>transactions.py</strong>.

<h1>Part 2</h1>

Now, If there are 10 articles and Salar needs to prove he has written all of them beforehand, what should he do? Clearly he can do the same steps 10 times. Can you suggest an easier, better and cheaper solution?

Explain your idea and implement it in a script called <strong>multifileverify.py</strong>, which takes n, the number of files and then takes n files and using your idea, it achieves Parsa’s goal. You don’t need to test it, but make sure it works.

<h1>Problem 6 – Atomic Swap</h1>

Last but not least, you will create a transaction called a cross-chain atomic swap, allowing two entities to securely trade ownership over cryptocurrencies on different blockchains. In this case, Alice and Bob will swap coins between the Bitcoin testnet and BlockCypher testnet. As you recall from setup, Alice has bitcoin on BTC Testnet3, and Bob has bitcoin on BCY Testnet. They want to trade ownership of their respective coins securely, something that can’t be done with a simple transaction because they are on different blockchains. The idea here is to set up transactions around a secret x, that only one party (Alice) knows. In these transactions only H(x) will be published, leaving x secret. Transactions will be set up in such a way that once x is revealed, both parties can redeem the coins sent by the other party. If x is never revealed, both parties will be able to retrieve their original coins safely, without help from the other. Before you start, make sure to read swap.py, alice.py, and bob.py. Compare to the pseudocode in <a href="https://en.bitcoin.it/wiki/Atomic_cross-chain_trading">here</a>(open your vpn :D). This will be very helpful in understanding this assignment. Note that for this question, you will only be editing ex6.py and you can test your code by running python swap.py.

<ol>

 <li>Consider the ScriptPubKey required for creating a transaction necessary for a cross- chain atomic swap. This transaction must be redeemable by the recipient (if they have a secret x that corresponds to Hash(x)), or redeemable with signatures from both the sender and the recipient. Write this ScriptPubKey in coinExchangeScript in ex6.py.</li>

 <li>Write the accompanying ScriptSigs:

  <ul>

   <li>Write the ScriptSig necessary to redeem the transaction in the case where the re- cipient knows the secret x. Write this in coinExchangeScriptSig1 in ex6.py.</li>

   <li>Write the ScriptSig necessary to redeem the transaction in the case where both the sender and the recipient sign the transaction. Write this in coinExchangeScriptSig2 in ex6.py.</li>

  </ul></li>

 <li>Run your code using python swap.py. We aren’t requiring that the transactions be broadcasted, as that requires some waiting to validate transactions. Running with broad- cast transactions=False will validate that ScriptSig + ScriptPK return true. Try this for alice redeems=True as well as alice redeems=False.</li>

</ol>

<a href="#_ftnref1" name="_ftn1">[1]</a> The testnet is a network that functions similar to the mainnet of Bitcoin, but the bitcoins in it are free. It’s purpose is to help developers test their codes and play around with their tools before trying them out on the mainnet.

You can read more about it <a href="https://en.bitcoin.it/wiki/Testnet">here</a>

<a href="#_ftnref2" name="_ftn2">[2]</a> A faucet is a website that gives free testnet coins to developers.