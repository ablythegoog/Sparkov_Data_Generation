## Generate Fake Credit Card Transaction Data, Including Fraudulent Transactions

### General Usage
* Create customers data file (see generate_customers.bat for syntax)
* Create transactions, utilizing prior customer file (see various .sh/.bat for syntax)

This code is heavily modified, but based on original code by [Josh Plotkin](https://github.com/joshplotkin/data_generation). Change log of modifications to original code are below.


```
# git clone ...
cd Sparkov_Data_Generation
mkdir output
# Ensure running python 3
python --version
pip install -r requirements.txt
python datagen_customer.py 10000 4144 profiles/main_config.json >> output/customers.csv
python datagen_transaction.py output/customers.csv profiles/adults_2550_female_rural.json 1-1-2020 12-31-2020 >> output/adults_2550_female_rural.csv
# may take 15 minutes (or more) to complete
# if this works then run
rm -rf output/*
chmod +x create_all_transactions.sh
./create_all_transactions.sh
# this will thread many python processes in the background. it may take a lot of CPU and a while.
```

### Modifications:

#### Aaron Blythe Fork

* Add requirements.txt
* Update create_all_transactions.sh to run out of the box.

#### v 0.4
* Only surface-level changes done in scripts so that simulation can be done using Python3
* Corrected bat files to generate transactions files.

#### v 0.3
* Completely re-worked profiles / segementation of customers
* introduced fraudulent transactions
* introduced fraudulent profiles
* modification of transaction amount generation via Gamma distribution
* added 150k_ shell scripts for multi-threaded data generation (one python process for each segment launched in the background)

#### v 0.2
* Added unix time stamp for transactions for easier programamtic evaluation.
* Individual profiles modified so that there is more variation in the data.
* Modified random generation of age/gender. Original code did not appear to work correctly?
* Added batch files for windows users

#### v 0.1
* Transaction times are now included instead of just dates
* Profile specific spending windows (AM/PM with weighting of transaction times)
* Merchant names (specific to spending categories) are now included (along with code for generation)
* Travel probability is added, with profile specific options
* Travel max distances is added, per profile option
* Merchant location is randomized based on home location and profile travel probabilities
* Simulated transaction numbers via faker MD5 hash (replacing sequential 0..n numbering)
* Includes credit card number via faker
* improved cross-platform file path compatibility
