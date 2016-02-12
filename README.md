Xinwenlianbo Scraping
=====================

This is the scripts capable of downloading from Xinwenlianbo, or News Simulcast, of China Central Television.

Requirements
----------
```
pip install -r requirements.txt
```

How to use
----------
This repo does not contain actual data from Xinwenlianbo.

To download the data, run all cells of the following iPython notebooks, in order:
- Initial_Collect
- Initial_Collect-fix-march-2012

Expected output:
- Index pages in 'index_pages'
- Detail pages in 'posts'
- Text exacted from detail pages, in 'texts'

This would usually take several hours.

To consolidate all texts into one json, please run:
- make_json

To update the documents after the initial collection, run:
- update_db.ipynb
(to optimize performance, you can manually specify the starting date in the code)

Key periods
-----------

### Before 20090627
Index pages of Xinwenlianbo seem in-accessible online.

### 20090627 - 20110405 (Period A)
The index pages of this period is accessible at a URL similar to
http://news.cctv.com/program/xwlb/20090627.shtml

### 20100506 - 20110405 (Period B)
The index pages of this period is accessible at a URL similar to
http://news.cntv.cn/program/xwlb/20100506.shtml

### 20110406 - now (Period C)
The index page of this period is accessible at a URL similar to
http://cctv.cntv.cn/lm/xinwenlianbo/20120406.shtml

Under this period, four sub-periods exist:

#### 20110406 - 20120226 (Period B1)
Under this period, the anchors linked to the individual reports are inserted by JavaScript, and the HTML page is encoded with GBK.

##### 20120227 - 20120329 (Period B2)
The title is dynamically inserted, but otherwise similar to B1.

##### 20120330 - 20130714 (Period B3)
Same pattern as B1.

#### 20130715 - now (Period B4; last update 20160212)
Under this period, the anchors are generated on the server side and the page is in UTF-8.

LICENSE
--------
This document is released as CC-BY-3.0 as outlined in LICENSE.
