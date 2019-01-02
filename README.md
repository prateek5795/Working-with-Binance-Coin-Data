# Working-with-Binance-Coin-Data

Statistical Methods for Data Science  
Fall 2018  
Project: Working with Binance Coin Dataset  

Authors
- Prateek Sarna (pxs180012@utdallas.edu)
- Shivani Mankotia (sxm180018@utdallas.edu) (https://github.com/12ani)

Data Description
- Our data files contain two primary groups: token network edge files, and token price files. The Ethereum project is a         blockchain platform, and our data comes from there. Although Ethereum started in 2015, most tokens have been created since     2016. As such, tokens have different starting dates, and their data starts from that initial date.
- Token edge files have this row structure: fromNodeID\ttoNodeID\tunixTime\ttokenAmount\r\n
- This row implies that fromNodeID sold tokenAmount of the token to toNodeID at time unixTime. fromNodeID and toNodeID are       people who invest in the token in real life; each investor can also use multiple addresses. Two addresses can sell/buy         tokens multiple times with multiple amounts. For this reason, the network is considered a weighted, directed multi(edge)       graph. Each token has a maximum token count maxt; you can think of maxt as the total circulating token amount.
- Binance coin is among the many which run on the Ethereum blockchain and follows the ERC20 standard. These tokens have a       limited supply (i.e., token count, which can be found on coinmarketcap.com as circulating amount). Each token may have sub-   units. This is similar to dollar in the US. There are around 18 trillion dollars in the economy, and each dollar is divided   into 100 cents (subunits). Similarly, there is a token supply, and then there is a subunit for each token. This idea comes     from Bitcoin where subunits are called Satoshis, 1 Bitcoin =10^8 satoshis. Coin market cap gives the total supply, but not     sub-units, which differ from token to token. Some tokens have 1018 sub-units. That means there can be numbers as big as       totalAmount∗1018.
- Etherscan.io gives these sub-units as decimals, please see the Vechain here: It has 18 decimals, which means each Vechain     token has 1018 subunits. https://etherscan.io/token/0xd850942ef8811f2a866692a623011bde52a462c1
- Price files have no extensions, but they are text based. File can be opened with a text editor and have the following row     structure: Date\tOpen\tHigh\tLow\tClose\tVolume\tMarketCap\r
- The price data is taken from https://coinmarketcap.com/. Open and close are the prices of the specific token at the given     date. Volume and MarketCap give total bought/sold tokens and market valuation at the date.

Question 1
- Find the distribution of how many times a user 1 - buys, 2 - sells a token. Which discrete distribution type fits these       distributions best? Estimate distribution parameters.

Question 2
- How can we create layers of transactions with increasing amounts? This descriptive statistic is similar to bin selection in   histograms. For example, we could choose layer1 as those transactions that involve 0.01×maxt in amount. Find a good value     for the number of layers and justify your choice.
- Once you create layers, you can compute a feature in each layer. An example feature is the number of transactions, another     one is the number of unique buyers. 
- As each edge has a unix timestamp, it is easy to compute the edge time to a date. For     example, 1294226315 is equivalent   to 01/05/2011 @ 11:18am (UTC). See the website https://www.unixtimestamp.com/index.php for   unix time conversion. R has       functions to compute dates from unix time stamps as well. This way, for a given day you can find   all layer transactions in   that day. For example, you can say on 10/12/2018 there were 25 transactions in layer 1. The price of token on that date was   3.2$. For each day in a token’s history, you can then correlate price vs feature in time.
- Find an algorithm to compute the correlation of price data with each of the layers (hint: start by looking at Pearson         correlation).
