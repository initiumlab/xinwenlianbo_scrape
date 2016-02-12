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

### On and Before 20020927
Index pages of Xinwenlianbo seem in-accessible online.

### 20020908 - 20090626 (Period A)
The index pages of this period is accessible at a URL similar to
http://www.cctv.com/news/xwlb/20020908/index.shtml

### 20090627 - 20100505 (Period B)
The index pages of this period is accessible at a URL similar to
http://news.cctv.com/program/xwlb/20090627.shtml

### 20100506 - 20110405 (Period C)
The index pages of this period is accessible at a URL similar to
http://news.cntv.cn/program/xwlb/20100506.shtml

### 20110406 - now (Period D)
The index page of this period is accessible at a URL similar to
http://cctv.cntv.cn/lm/xinwenlianbo/20120406.shtml

Under this period, four sub-periods exist:

#### 20110406 - 20120226 (Period D1)
Under this period, the anchors linked to the individual reports are inserted by JavaScript, and the HTML page is encoded with GBK.

#### 20120227 - 20120329 (Period D2)
The title is dynamically inserted, but otherwise similar to B1.

#### 20120330 - 20130714 (Period D3)
Same pattern as B1.

#### 20130715 - now (Period D4; last update 20160212)
Under this period, the anchors are generated on the server side and the page is in UTF-8.

For reference, checkout the JavaScript implementation of the calendar date picker on any Xinwenlianbo page,
such as <http://news.cntv.cn/program/xwlb/20110105.shtml>. It's something like this:
```
var start = new Date(2009, 5, 25, 0, 0, 0);
//alert("start.getMonth()"+start.getMonth());
//alert("time="+time.getFullYear()+(time.getMonth()+1)+time.getDate() + "********start=" + start.getFullYear()+(start.getMonth()+1)+start.getDate() + "********now=" + now.getFullYear()+(now.getMonth()+1)+now.getDate());
if((time < now) && (time > start)){
var time_1 = year + mon + day;
if(time_1<20100506){
str = "http://news.cctv.com/program/xwlb/" + year + mon + day + ".shtml";
}
if(time_1>=20100506&&time_1<20110406){
str = "http://news.cntv.cn/program/xwlb/" + year + mon + day + ".shtml";
}
if(time_1>=20110406){
str = "http://cctv.cntv.cn/lm/xinwenlianbo/" + year + mon + day + ".shtml";
}
window.open(str);
}
```
(The above code is for research purpose only and is only distributed under Xinwenlianbo's terms.)

Note that although the code above implies Xinwenlianbo is available since 20090525, it seemsonly after 20090627 are the pages actually accessible.

LICENSE
--------
This document is released as CC-BY-3.0 as outlined in LICENSE.
