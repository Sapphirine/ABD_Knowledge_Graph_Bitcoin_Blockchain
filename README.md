# Advanced Big Data: Data Aquisition for Building Knowledge - Blockchain Graph for Bitcoin Transaction
Data Acquisition for Building Knowledge Graph: Blockchain 

## 1.	Overview:
Bitcoin (bitcoin.org) is a digital, cryptographically secure currency. Transactions between public-key "addresses" maintained in a distributed, verified public ledger form a transaction network that can be studied by network scientists. This code processes binary-format Bitcoin .dat files generated by the Bitcoin client (bitcoin.org, tested on v0.14) into human-readable flat-file formats, retaining all available information. 

## 2.	File output description:
The following files are generated, with their row specification:

bitcoin_pubkey_list.txt: [public_key_string]
bitcoin_transactionkey_list.txt: [transaction_key_string]

bitcoin_userkey_list.txt: [public_key1,public_key2,public_keyk]
bitcoin_user_edge_inputs.txt: [transaction_keyself,transaction_key1,transaction_keyk]
bitcoin_user_edge_inputs_public_keys.txt: [transaction_keyself,public_key1,public_keyk]
bitcoin_user_edges.txt: [transaction_keyself, user_keyfrom, user_keyto, date, value]
The first group of files, (bitcoin_pubkey_list.txt, bitcoin_transactionkey_list.txt) contains the lengthy text keys for public keys (i.e. 1EnHwdiKxvTE5AzcSnZqS52mMcHSLtCLwH) and transaction keys (i.e. 5dc77144dcf46a7f76e369d406481e857be9e95b21375935832a5bed4e23633b). Each key field is a line number (starting at 1) to index into the appropriate list file. 

The second group of files (bitcoin_userkey_list.txt, bitcoin_user_edge_inputs.txt, bitcoin_user_edge_inputs_public_keys.txt) organizes the user information, where a user is a grouping of public keys inferred from public keys combined as inputs into a single transaction (meaning the user owns the private key to each address).  We create a graph where two public keys have an edge if they have been used as inputs in a single transaction. The connected components of this graph are users. Each line in userkey_list.txt is one of these components (a grouping of public keys). The files user_edge_inputs.txt and user_edge_inputs_public_keys.txt record the transaction keys, and public keys used as input to this transaction.

The third group of files (bitcoin_user_edges.txt) is the primary network data file. The files bitcoin_user_edges.txt,  bitcoin_user_edge_inputs.txt, and bitcoin_user_edge_inputs_public_keys.txt share a transaction key field which allows them to be joined on. 

## 3.	Python code execution:
The included Python scripts use only core packages and have been tested on the latest version of Python, with Bitcoin .dat files generated by the official client, version v0.14. 
The main shell script process_bitcoin_network_runner.sh can be configured with your paths and desired output filenames. The two primary paths that need to be set by the user are the file output path (file_path), and lib_path the path to  the folder of bitcointools (https://github.com/harrigan/bitcointools), which handles the extraction of the binary files to raw text output (as of Mar 20 2017, about 122GB of transaction data).


