## Working with Scrapy

To initialize scarpy (in cmd)
```
scrapy startproject
```

To create a spider (in cmd)
```
scrapy genspider -t basic <spider-name> <link of the website>
```

To scrape the web code in <spider-name>.py file inside the spiders folder
```py
import scrapy


class MobileSpiderSpider(scrapy.Spider):
    name = 'mobile_spider'
    allowed_domains = ['www.newegg.com']
    start_urls = ['https://www.newegg.com/p/pl?d=mobile/']

    def parse(self, response):
        for mobile in response.xpath("//div[@class='item-container']"):
            yield {
                'Product Name': mobile.xpath(".//div[@class='item-title']/p").extract_first(),
                'Price': mobile.xpath(".//div[@class='price-current']/p").extract_first(),
                'Discount': mobile.xpath(".//div[@class='price-save']/p").extract_first()
            }
```

To retreive the scraped data (in cmd)
```
scrapy crawl mobile_spider -o  crawl.json
```