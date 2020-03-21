Question 1.1
    createGenesisBlock(){
        return new Block(0, "03/21/2020", "Bloco inicial da koreCoin", "0");
    }

Question 1.2

koreCoin.addBlock(new Block (1, "01/01/2018", {amount: 20}));
koreCoin.addBlock(new Block (2, "02/01/2018", {amount: 40}));
koreCoin.addBlock(new Block (3, "02/01/2018", {amount: 40}));
koreCoin.addBlock(new Block (4, "02/01/2018", {amount: 20}));
koreCoin.addBlock(new Block (5, "03/21/2020", {amount: 40}));

var i;
for (i = 0; i < koreCoin.chain.length; i++) {
  koreCoin.chain[i].data = { amount: 100 };
console.log("tampering with data...");
koreCoin.chain[i].hash = koreCoin.chain[i].calculateHash();

console.log('Is Blockchain valid? ' + koreCoin.isChainValid());
} 

Question 2.1

difficulty=2
		real	0m0.082s
		user	0m0.072s
		sys	0m0.012s
difficulty=3
		real	0m0.638s
		user	0m0.628s
		sys	0m0.040s

difficulty=4
		real	0m3.151s
		user	0m3.052s
		sys	0m0.100s

difficulty=5
		real	0m42.915s
		user	0m42.148s
		sys	0m0.652s

Question 2.2
1.Publish new blocks by mining and the reward is bitcoin that is: To create new coins, people have to mine new blocks of SnakeCoin. When they successfully mine new blocks, a new SnakeCoin is created
 and rewarded to the person who mined the block. The coin then gets circulated once the miner sends the SnakeCoin to another person.
2.Yes, because we need a shared consistent data store,more than one entity need to contribute data,records once written are never updated or deleted, sensitive identifiers will not be written to the data store,
the entities with write access are having a hard time deciding who should be in control of the data store and we want a tamperproof log of all writes to the data store.