# Scrapy-Tutorial
Just following along with the Scrapy tutorial on their website. 

Commands to know are as follows:
1. Run in the CLI ``scrapy crawl quotes``

This generates the html for the pages in the quotes.spider file.

2. Run in the CLI `scrapy shell "https://quotes.toscrape.com/page/1/"` for WSL or `scrapy shell 'https://quotes.toscrape.com/page/1/'` for linux based platforms.
3. From there, you can use the following commands
- ``response.css("title::text").getall() `` or `` response.css("title::text")[0].get()``
- You can also  create variables in the CLI such as `` quote = response.css("div.quote")[0]  `` This creates an psuedo object class from the response array of data for the first array.
- You can also create other variables like  ``author = quote.css("span.author::text").get()`` or ``text = quote.css("span.text::text").get() ``This tells the CLI to check the quote object created above, and then createse variables from the text under the spans of author and text from the HTML originally scrapped from the scrapy shell.
- If you would prefer you can copy the following into the CLI:
```python
for quote in response.css("div.quote"):
     text = quote.css("span.text::text").get()
     author = quote.css("small.author::text").get()
     tags = quote.css("div.tags a.tag::text").getall()
     print(dict(text=text, author=author, tags=tags))
```

Now that there's a basic understaning of commands, you can use the folliwng command to get workable JSON's for what was scrapped.

```python
scrapy crawl quotes -o quotes.jsonl

```
The command tells it to scrape and show the the quotes function class, with the -o overwriting the files, and telling it to print to a quotes.json files.