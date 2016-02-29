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

### 20020908 - 20090625 (Period A)
The index pages of this period is accessible at a URL similar to
http://www.cctv.com/news/xwlb/20020908/index.shtml

Under this period, there exist multiple sub-periods with similar URL scheme but different HTML layouts.

#### 20020908 - 20041230 (Period A1)

Titles are like `<font class='fs24'>Title</font>`

#### 20041231 - 20060131 (Period A2)

Titles are like `<font class='title_text'>Title</font>`

#### 20060201 - 20070830 (Period A3)

Titles are like `<span class='title'>Title</span>`

#### 20070831 - 20090625 (Period A4)

Title are like `<h1>Title</h1>`

### 20090626 - 20100505 (Period B)
The index pages of this period is accessible at a URL similar to
http://news.cctv.com/program/xwlb/20090626.shtml

### 20100506 - 20110405 (Period C)
The index pages of this period is accessible at a URL similar to
http://news.cntv.cn/program/xwlb/20100506.shtml

### 20110406 - 20160220 (Period D)
The index page of this period is accessible at a URL similar to
http://cctv.cntv.cn/lm/xinwenlianbo/20120406.shtml

Under this period, four sub-periods exist:

#### 20110406 - 20120226 (Period D1)
Under this period, the anchors linked to the individual reports are inserted by JavaScript, and the HTML page is encoded with GBK.

#### 20120227 - 20120329 (Period D2)
The title is dynamically inserted, but otherwise similar to B1.

#### 20120330 - 20130714 (Period D3)
Same pattern as B1.

#### 20130715 - 20160220 (Period D4)
Under this period, the anchors are generated on the server side and the page is in UTF-8.

### 20160202 - now (Period E; last check 20160226)
Under these period, the index is always at http://tv.cctv.com/lm/xwlb/index.shtml, while the anchors are asynchronoly loaded from a url in the form of http://tv.cctv.com/lm/xwlb/day/20160226.shtml

Note that this period overlaps with Period D4.

For reference, checkout the JavaScript implementation of the calendar date picker on the latest Xinwenlianbo page in 2016,
such as <http://tv.cctv.com/lm/xwlb/index.shtml>. It's something like this:
```
		if(time_1<20100506){
			str = "http://news.cctv.com/program/xwlb/" + year + mon + day + ".shtml";//这里的地址使用他之前的地址域名
			window.open(str);
		}
		if(time_1>=20100506&&time_1<20110406){
			str = "http://news.cntv.cn/program/xwlb/" + year + mon + day + ".shtml";//这里的地址使用他之前的地址域名，具体域名可参考相关栏目的旧时间表JS写法
			window.open(str);
		}
		if(time_1>=20110406&&time_1<20130709){
		    //alert("http://cctv.cntv.cn/program/C29201/" + year + mon + day + ".shtml");
			str = "http://cctv.cntv.cn/lm/xinwenlianbo/" + year + mon + day + ".shtml";//这里的地址使用他之前的新地址域名
			window.open(str);
		}
		if(time_1>=20130709&&time_1<20160203){
			str = "http://cctv.cntv.cn/lm/xinwenlianbo/" + year + mon + day + ".shtml";//这里的地址使用新地址域名例如http://news.cntv.cn/lm/xinwenlianbotest/20130515.shtml
			window.open(str);
		}
		
		if(time_1>=20160203){
		  //Code skipped
  	}
```
(The above code is for research purpose only and is only distributed under Xinwenlianbo's terms.)

Note that although the code above implies Xinwenlianbo is available since 20090525, it seemsonly after 20090627 are the pages actually accessible.

LICENSE
--------
This document is released as CC-BY-3.0 as outlined in LICENSE.
