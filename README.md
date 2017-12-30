# Tweet Pump-and-Dump
### Description
Performs trades on Bittrex based on tweets of a user. Searches tweets for any
mentions of currencies available on Bittrex. Optionally searches for a key
term/phrase first before searching for currencies.

### Configuration
A file named `config.json`, located in `/res/`, is used as the configuration of
the bot. Below is the base configuration for the bot:

```json
{
    "twitter": {
        "api": {
            "key": "",
            "secret": "",
            "access_token": "",
            "access_secret": ""
        },
        "user": "",
        "search_term": "",
        "ignore_retweets": true
    },
    "exchanges": {
        "binance": {
            "priority": 0,
            "key": "",
            "secret": ""
        },
        "bittrex": {
            "priority": 1,
            "key": "",
            "secret": ""
        }
    },
    "order": {
        "quote_currencies": {
            "btc": 0,
            "eth": 0
        },
        "multiplier": 0
    },
    "tesseract_cmd": "",
    "verbose: false
}
```

> **Note**: All strings, with the exception of authentication credentials,
`user`, `search_term`, and `tesseract_cmd` must be completely lower case.

* `tesseract_cmd` - Path to the tesseract binary; ignored if empty. Unnecessary
if it is in the system's `PATH`.
* `verbose` - `true` if the logger should be more verbose e.g. show debug
messages; `false` otherwise.

#### Twitter
* `key` - Consumer key (API key)
* `secret` - Consumer secret (API secret)
* `access_token` - Access token; can be used to make API requests on your own
account's behalf.
* `access_secret` - Access secret
* `user` - The Twitter handle of the user whose tweets will be read.
* `search_term` - A search term to use to filter the user's tweets; ignored if
empty.
* `ignore_retweets` - Does not parse tweets which are retweets.

#### Exchanges
* `priority` - A positive integer representing the priority of the exchange.
Lower numbers have higher priority. Set to `0` to disable the exchange.
* `key` -  The exchange's API key.
* `secret` - The exchange's API secret.

#### Orders
* `quote_currencies` - A dictionary of currency ticker symbols for quote
currencies (currencies with which the tweeted currency can be bought) and the
amounts to spend on the order. The order determines the priority of the
currency; the first has the highest priority.
* `multiplier` - The price paid for the order is multiplied by `1 + multiplier`
to account for any price increases between the request for the price and request
for placing the order.

### Requirements
* [Python 3.6](https://www.python.org/downloads/) or higher
* [tweepy](http://www.tweepy.org/)
* [pytesseract](https://github.com/madmaze/pytesseract)
    * Requires
    [Google Tesseract OCR](https://github.com/tesseract-ocr/tesseract) to be
    installed on the system. See
    [this](https://github.com/tesseract-ocr/tesseract/wiki) page for more
    specific installation instructions.
* [coinmarketcap](https://github.com/mrsmn/coinmarketcap)
* [python-binance](https://github.com/sammchardy/python-binance)
* [python-bittrex](https://github.com/ericsomdahl/python-bittrex)

### Installation
[pipenv](https://docs.pipenv.org/) can be used to simply the installation
process. Once it is installed, `cd` into the root directory and install the
dependencies from the pipefile with

```bash
pipenv install
```

An error may occur while installing python-binance on Windows. More specifically

> Failed building wheel for Twisted

The error can be circumvented by downloading a pre-built wheel of Twisted from
[here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted). Download the
32-bit or 64-bit version depending on your OS and move the file into the root
directory of the program. To install Twisted and finish the installation of
python-binance run

```bash
pipenv install twisted-wheel-file-name.whl
pipenv install
```

### Running
Run `bot.py` to run the bot. If using pipenv:

```bash
pipenv shell
cd src
python bot.py
```

otherwise

```bash
python bot.py
```
