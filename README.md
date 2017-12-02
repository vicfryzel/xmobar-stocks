# xmobar-stocks
xmobar-stocks is a program to fetch stock quotes on-demand.

![Screenshot of xmobar-stocks](screenshot.png)

It is a replacement for the popular https://github.com/jacobtolar/xmobar-stocks,
which no longer functions because the Yahoo Finance API has been disabled. This updated version
(written in Python) fetches stock quotes from https://www.alphavantage.co.

xmobar-stocks is tested to run with Python 2.7.13 and 3.5.3. The specific version of xmobar or xmonad
you're using doesn't matter.

## Installation
The only dependencies of xmobar-stocks are Python and the
[Python Requests library](http://docs.python-requests.org/en/master/). You'll also need git to clone
this repository. To install these dependencies on an Ubuntu instance, run:

    aptitude install git python python-requests
    
Once the dependencies are installed, clone xmobar-stocks, make it executable, and add it to your PATH.

    cd
    git clone https://github.com/vicfryzel/xmobar-stocks.git
    chmod +x xmobar-stocks/xmobar-stocks
    echo "PATH=\${PATH}:~/xmobar-stocks" >> ~/.bashrc
    
## Configuration
Now that you've got xmobar-stocks and its dependencies installed, you must register an API key with
[Alpha Vantage](https://www.alphavantage.co), and then configure xmobar.

To configure an API key, go [here](https://www.alphavantage.co).

Now, edit your xmobar configuration as follows (likely located at `~/.xmonad/xmobarrc` or
`~/.xmonad/xmobar.hs`):

    Config {
      ...
      commands = [
        ...
        Run Com "xmobar-stocks" ["-s", "<list-of-symbols>", "-k", "<api-key>"] "stocks" 60,
        ...
      ],
      ...
      template = "...   %stocks%   ..."
    }

Replace `<list-of-symbols>` with a comma-separated list of stock symbols (e.g. `GOOG,AMZN,TSLA`).
Replace `<api-key>` with your Alpha Vantage API key.

That's it! Recompile/refresh xmonad and you should see stock quotes in xmobar.

## Usage information

    ./xmobar-stocks -h
    usage: xmobar-stocks [-h] -s SYMBOLS -k API_KEY [-d]
    
    optional arguments:
      -h, --help            show this help message and exit
      -s SYMBOLS, --symbols SYMBOLS
                            comma-separated list of stock symbols
      -k API_KEY, --api-key API_KEY
                            Alpha Vantage API key (see
                            https://www.alphavantage.co/)
      -d, --debug           show debug messages
