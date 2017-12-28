# yahoo-dividends-splits
These Racket programs will download the Yahoo dividends and splits CSV files and insert the data into a PostgreSQL database. The intended usage is:

```
$ Racket extract.rkt
$ Racket transform-load.rkt
```

The provided schema.sql file shows the expected schema within the target PostgreSQL instance. This process assumes you can write to a 
/var/tmp/yahoo/dividends-splits folder. This process also assumes you have loaded your database with the NASDAQ symbol file information.
This data is provided by the [nasdaq-symbols](https://github.com/evdubs/nasdaq-symbols) project.

Finally, there are two parameters required to extract data correctly from Yahoo: cookie and crumb. You can find these values by doing the following:

1. Go to http://finance.yahoo.com in your web browser
2. Load a stock (AAPL will work)
3. Click on the "Historical Data" tab
4. Right-click the "Download Data" link and select "Copy Link Location". This URL will have a query string that includes the crumb field and its value. The value may look something like `aAbBcCdDeE123` and will be what you need to extract.
5. Find the cookies set for this page (in Firefox, right-click, View Page Info, Security, View Cookies). A cookie named "B" will be set. The content of this cookie may look something like `abcdefghi123&b=3&s=ua` and will be what you need to extract.

This cookie and crumb combination should both be valid for a year, so you do not need to do this every time.