## Unit 19 Homework: Cryptocurrency Wallet

### Background

This code is for building a new and disruptive platform called KryptoJobs2Go. KryptoJobs2Go is an application that its customers can use to find fintech professionals from among a list of candidates, hire them, and pay them. As KryptoJobs2Go’s lead developer, you have been tasked with integrating the Ethereum blockchain network into the application in order to enable your customers to instantly pay the fintech professionals whom they hire with cryptocurrency.

In this Challenge, I have completed building the code that enables your customers to send cryptocurrency payments to fintech professionals.

### What was done ? 

Following was done to successfully build an application which will help the customers of KryptoJobs2Go to hire fintech professionals and pay them in cryptocurrency :

* Generate a new Ethereum account instance by using the mnemonic seed phrase provided by Ganache.

* Fetch and display the account balance associated with your Ethereum account address.

* Calculate the total value of an Ethereum transaction, including the gas estimate, that pays a KryptoJobs2Go candidate for their work.

* Digitally sign a transaction that pays a KryptoJobs2Go candidate, and send this transaction to the Ganache blockchain.

* Review the transaction hash code associated with the validated blockchain transaction.

Once the transaction’s hash code is generated, the application can navigate to the Transactions section of Ganache to review the blockchain transaction details. 

### High Level steps for this challenge 

The steps for this challenge are broken out into the following sections:

* Import Ethereum Transaction Functions into the KryptoJobs2Go Application
* Sign and Execute a Payment Transaction
* Inspect the Transaction on Ganache

#### Step 1: Import Ethereum Transaction Functions into the KryptoJobs2Go Application

Imported several functions from the `crypto_wallet.py` script into the file `krypto_jobs.py`, which contains code for KryptoJobs2Go’s customer interface, in order to add wallet operations to the application. For this section, you will assume the perspective of a KryptoJobs2Go customer (i.e., you’ll provide your Ethereum wallet and account information to the application).

Completed the following steps:

1. Reviewed the code contained in the `crypto_wallet.py` script file. Note that the Ethereum transaction functions that you have built throughout this module&mdash;including `wallet`, `wallet.derive_acount`, `get_balance`, `fromWei`, `estimateGas`, `sendRawTransaction`, and others&mdash;have now been incorporated into Python functions that allow you to automate the process of accessing them.

2. Add your mnemonic seed phrase (provided by Ganache) to the starter code’s `SAMPLE.env` file. When the information has been added, rename the file `.env`.

Generated a new mnemonic seed phrase in my local Ganache interface and add the same to SAMPLE.env and renamed it to ".env".

3. In the `krypto_jobs.py` file imported the following functions from the `crypto_wallet.py` file:

    * `generate_account`

    * `get_balance`

    * `send_transaction`

	Added the following code block :

	`from crypto_wallet import generate_account, get_balance, send_transaction`	
	
4. Within the Streamlit sidebar section of code, created a variable named `account`. Set this variable equal to a call on the `generate_account` function. This function will create the KryptoJobs2Go customer’s (in this case, your) HD wallet and Ethereum account.

	Added the following code block :

	`account = generate_account()`

5. Within this same section of the `krypto_jobs.py` file, define a new `st.sidebar.write` function that will display the balance of the customer’s account. Inside this function, call the `get_balance` function and pass it your Ethereum `account.address`.

	Added the following code block :

	`st.sidebar.write(account.address)`
	
#### Step 2: Sign and Execute a Payment Transaction

The code will calculate a fintech professional’s wage, in ether, based on the worker’s hourly rate and the number of hours that they work for a customer. (The fintech professionals’ hourly rates are provided in the `candidate_database` that is found in `krypto_jobs.py`.)

Then the code uses the calculated wage value to send a transaction that pays the worker. This code will allow the KryptoJobs2Go customer to authorize the transaction with their digital signature. For the purpose of testing out this application, i have used my own Ethereum account (from Ganache) information as the customer account information.

To accomplish all of this, completed the following steps:

1. KryptoJobs2Go customers will select a fintech professional from the application interface’s drop-down menu, and then input the amount of time for which they’ll hire the worker. Code the application so that once a customer completes these steps, the application will calculate the amount that the worker will be paid in ether. To do so, complete the following steps:

    * Write the equation that calculates the candidate’s wage. This equation should assess the candidate’s hourly rate from the candidate database (`candidate_database[person][3]`) and then multiply this hourly rate by the value of the `hours` variable. Save this calculation’s output as a variable named `wage`.

    * Write the `wage` variable to the Streamlit sidebar by using `st.sidebar.write`.

2. Now that the application can calculate a candidate’s wage, write the code that will allow a customer (you, in this case) to send an Ethereum blockchain transaction that pays the hired candidate. To accomplish this, locate the code that reads `if st.sidebar.button("Send Transaction")`. You’ll need to add logic to this `if` statement that sends the appropriate information to the `send_transaction` function (which you imported from the `crypto_wallet` script file). Inside the `if` statement, add the following functionality:

    * Call the `send_transaction` function and pass it three parameters:

    * Your Ethereum `account` information. (Remember that this `account` instance was created when the `generate_account` function was called.) From the `account` instance, the application will be able to access the `account.address` information that is needed to populate the `from` data attribute in the raw transaction.

    * The `candidate_address` (which will be created and identified in the sidebar when a customer selects a candidate). This will populate the `to` data attribute in the raw transaction.

    * The `wage` value. This will be passed to the `toWei` function to determine the wei value of the payment in the raw transaction.

    * Save the transaction hash that the `send_transaction` function returns as a variable named `transaction_hash`, and have it display on the application’s web interface.

#### Step 3: Inspected the Transaction

Tested the KryptoJobs2Go application with my newly integrated Ethereum wallet from Ganache. You will send a test transaction by using the application’s web interface, and then look up the resulting transaction in Ganache. To do so, complete the following steps:

1. From my terminal, navigated to the project folder that contains the `.env` file and the `krypto_jobs.py` and `crypto_wallet.py` files in an activated conda environment with all the depndencies installed.

2. Launched the Streamlit application by executing `streamlit run krypto_jobs.py`.

3. On the resulting webpage, selected a candidate that i would like to hire from the appropriate drop-down menu. Then, entered the number of hours that i would like to hire them for and clicked the "Send Transaction" button to sign and send the transaction with my Ethereum account information.

	- Below is the screen-shot of my local Ganache application which displays the Ethereum accounts with their addresses, balances and also the seed phrase 

	<img width="1280" alt="Ganache" src="https://user-images.githubusercontent.com/112692272/216811633-a21d0c2e-bbc7-4997-947d-a8c3934342d7.png">


	- Below is the screen-recording video of KryptoJobs2Go's customer web interface which shows the transaction of a successful hire of a candidate with available ether.
	
	

	- Below is the scree-recording video which shows that the transaction fails if i do not have enough ether to hire a candidate
 
