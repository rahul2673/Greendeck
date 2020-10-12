# Greendeck
import scrapy
from ..items import MatchesfashionItem


class MatchesfashionSpiderSpider(scrapy.Spider):
    name = 'matchesfashion_spider'

    start_urls = [
        'https://www.matchesfashion.com/intl/mens/shop/shoes']

    def parse(self, response):
        items = MatchesfashionItem()

        product_Name = response.css('.lister__item__details::text').extract()
        product_Brand = response.css('.lister__item__title::text').extract()
        product_Price = response.css('.lister__item__price-full::text').extract()
        product_Image_Url = response.css('.lazy::attr(src)').extract()

        items['Name'] = product_Name
        items['Brand'] = product_Brand
        items['Price'] = product_Price
        items['Image_Url'] = product_Image_Url

        yield items

.................................................................................+...........................................



#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/items.html

import scrapy


class MatchesfashionItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    Name = scrapy.Field()
    Brand = scrapy.Field()
    Price = scrapy.Field()
    Image_Url = scrapy.Field()



