scrapy项目文件目录：

```
tutorial/
    scrapy.cfg            # deploy configuration file

    tutorial/             # project's Python module, you'll import your code from here
        __init__.py

        items.py          # project items definition file

        middlewares.py    # project middlewares file

        pipelines.py      # project pipelines file

        settings.py       # project settings file

        spiders/          # a directory where you'll later put your spiders
            __init__.py
```

Spiders are classes that you define and that Scrapy uses to scrape information from a website (or a group of websites). They must subclass `scrapy.Spider` and define the initial requests to make, optionally how to follow links in the pages, and how to parse the downloaded page content to extract data.

This is the code for our first Spider. Save it in a file named `quotes_spider.py` under the `tutorial/spiders` directory in your project:

```
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = 'quotes-%s.html' % page
        with open(filename, 'wb') as f:
            f.write(response.body)
        self.log('Saved file %s' % filename)
```

As you can see, our Spider subclasses [`scrapy.Spider`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/spiders.html#scrapy.spiders.Spider) and defines some attributes and methods:

- [`name`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/spiders.html#scrapy.spiders.Spider.name): identifies the Spider. It must be unique within a project, that is, you can’t set the same name for different Spiders.

- [`start_requests()`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/spiders.html#scrapy.spiders.Spider.start_requests): must return an iterable of Requests (you can return a list of requests or write a generator function) which the Spider will begin to crawl from. Subsequent requests will be generated successively from these initial requests.

- [`parse()`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/spiders.html#scrapy.spiders.Spider.parse): a method that will be called to handle处理 the response downloaded for each of the requests made. The response parameter is an instance实力，例子 of [`TextResponse`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/request-response.html#scrapy.http.TextResponse) that holds the page content and has further helpful methods to handle it.

  The [`parse()`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/spiders.html#scrapy.spiders.Spider.parse) method usually parses the response, extracting the scraped收集 data as dicts and also finding new URLs to follow and creating new requests ([`Request`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/request-response.html#scrapy.http.Request)) from them.

### How to run our spider

To put our spider to work, go to the project’s top level directory and run:

```
scrapy crawl quotes
```

This command runs the spider with name `quotes` that we’ve just added, that will send some requests for the `quotes.toscrape.com` domain.

Now, check the files in the current directory. You should notice that two new files have been created: *quotes-1.html* and *quotes-2.html*, with the content for the respective URLs, as our `parse` method instructs.

注解

If you are wondering why we haven’t parsed the HTML yet, hold on, we will cover that soon.

#### What just happened under the hood?

Scrapy schedules处理 the [`scrapy.Request`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/request-response.html#scrapy.http.Request) objects returned by the `start_requests` method of the Spider. Upon receiving a response for each one, it instantiates实例化 [`Response`](https://scrapy-16.readthedocs.io/zh-cn/1.6/topics/request-response.html#scrapy.http.Response) objects and calls the callback method associated with与。。联系 the request (in this case, the `parse` method) passing the response as argument.



































