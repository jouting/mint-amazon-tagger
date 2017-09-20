# Mint tagger for Amazon Transactions

Do you order a lot from Amazon? Tired of everything showing up as "Amazon.com"
w/ category "Shopping"? Then this tool is for you!

This tool DOES NOT require an Amazon store card/Visa. Any account that pays for
your orders and is sync with Mint will do!

This tool takes Amazon order reports and merges it with your existing Mint
transactions. If it finds exact matches, it will either:

- Update the transaction description/category if there was only 1 item

- Split the transaction, one line-item per item in the order

The tagger will try to guess the best Mint category for you. It does this by
looking at each item's category from the Amazon Items report. Look at
`category.py` to see which Amazon categories map to which Mint categories.

The tagger will _NOT_ retag or touch transactions that have already been
tagged. So feel free to adjust categories after the fact without fear that the
next run will wipe everything out.

## Getting started

0. Clone this repository: `git clone git@github.com:jprouty/mint-amazon-tagger.git; cd mint-amazon-tagger`

1. Install the dependencies: `pip install -r requirements.txt`

2. Install selenium and chromedriver. These tools help you acquire the
appropriate Mint login credentials:

```
pip install selenium

# Mac:
brew install chromedriver

# Ubuntu/Debian:
# Also check out: https://askubuntu.com/questions/539498/where-does-chromedriver-install-to
sudo apt-get install chromium-chromedriver
```

3. Generate and download your Amazon Order History Reports.

a. Login and visit [Amazon Order History
Reports](https://www.amazon.com/gp/b2b/reports)

b. "Request Report" for both "Items" and "Orders and shipments". Make sure the
date ranges are the same.

c. Download the completed reports. Let's called them `Items.csv` and
`Orders.csv` for this walk-through.

4. Run the tagger:
`./tagger.py Items.csv Orders.csv --mint_email yourEmail@here.com`

5. Sit back and relax! The runtime depends on the speed of your machine,
quality of internet connection, and total number of transactions. For
reference, my machine did about 14k Mint transactions, finding 2k Amazon
matches in under 10 minutes.