---
layout: post
category: "python"
title: "python 爬虫 + PDF"
tags: ["爬虫","PDF"]
---


###爬虫 + PDF  (无图片)

<a name="top"></a>

好久，前阵子跟着  `伯乐在线` 的教程自学了python爬虫，觉得实践还是比较少，对于爬虫也好，python的语法也是，还不是很精通。  

加上最近在网页上看文章，就想着能不能把网页上的`文字`和`图片`扒下来在kindle上看。 （在chrome上有`push to kindle` 能把网页直接推送到kindle 但是对于连载的网页比较不方便，因为连载的网页比较多，而且一个网页推送一次都是一个个小文件。）  
对于文件格式，第一个想到的就是PDF，既能包括文字，也有图片，几乎能在所有移动设备上查看。  
于是上Google搜索 `python pdf` 第一个看见的就是`PyPDF` （已出`PyPDF2`），继续查发现使用的例子比较少，而且好像入门也比较难。  
然后在Baidu上找，发现了几篇文章。发现另一个库`reportlab`。[参考1](#cankao) 给出的就是以reportlab为例子的。细看是用的`beautifulsoup`之前也学过一点，但是用的没那么熟悉。  

下面就贴出我的代码，是基于之前扒百度贴吧的帖子改的， 各种注释比较乱，还请见谅。  
####爬取github上的文章保存为PDF，图片的问题暂时还没找到好的解决办法。有大神看到的话，欢迎指教。

```python

# -*- coding:utf-8 -*-
import urllib
import urllib2
import re

import reportlab.rl_config
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont
from reportlab.lib import fonts
import copy
from reportlab.platypus import Paragraph, SimpleDocTemplate,flowables
from reportlab.lib.styles import getSampleStyleSheet

from reportlab.pdfgen import canvas

#处理页面标签类
class Tool:
    #去除img标签,7位长空格
    removeImg = re.compile('<img.*?>| {7}|')
    #删除超链接标签
    removeAddr = re.compile('<a.*?>|</a>')
    #把换行的标签换为\n
    replaceLine = re.compile('<tr>|<div>|</div>|</p>')
    # replaceLine = re.compile('<tr>|<div>|</div>|</p>|<blockquote>|</blockquote>')
    #将表格制表<td>替换为\t
    replaceTD= re.compile('<td>')
    #把段落开头换为\n加空两格
    replacePara = re.compile('<p.*?>|<p>')
    #将换行符或双换行符替换为\n
    replaceBR = re.compile('<br>')
    #将其余标签剔除
    removeExtraTag = re.compile('<.*?>')
    def replace(self,x):
        x = re.sub(self.removeImg,"",x)
        x = re.sub(self.removeAddr,"",x)
        x = re.sub(self.replaceLine,"\n",x)
        x = re.sub(self.replaceTD,"\t",x)
        x = re.sub(self.replacePara,"\n     ",x)
        x = re.sub(self.replaceBR,"\n",x)
        x = re.sub(self.removeExtraTag,"",x)
        #strip()将前后多余内容删除
        return x.strip()

#爬虫+pdf类
class BDTB:

    def __init__(self,baseUrl):
        #base链接地址
        self.baseURL = baseUrl
        #是否只看楼主
        #self.seeLZ = '?see_lz='+str(seeLZ)
        #HTML标签剔除工具类对象
        self.tool = Tool()
        #全局file变量，文件写入操作对象
        self.file = None
        #楼层标号，初始为1
        #self.floor = 1
        #默认的标题，如果没有成功获取到标题的话则会用这个标题
        self.defaultTitle = u"yufei"
        #是否写入楼分隔符的标记
        #self.floorTag = floorTag

    #传入页码，获取该页帖子的代码
    def getPage(self,baseURL):
        try:
            #构建URL
            #url = self.baseURL+ self.seeLZ + '&pn=' + str(pageNum)
            url = baseURL
            request = urllib2.Request(url)
            response = urllib2.urlopen(request)
            #返回UTF-8格式编码内容
            return response.read().decode('utf-8')
        #无法连接，报错
        except urllib2.URLError, e:
            if hasattr(e,"reason"):
                print u"连接失败,错误原因",e.reason
                return None

    #获取帖子标题
    def getTitle(self,page):
        #得到标题的正则表达式
        pattern = re.compile('<h1 class="headline".*?>(.*?)</h1>',re.S)
        result = re.search(pattern,page)
        if result:
            #如果存在，则返回标题
            # print result
            # return result
            return result.group(1).strip()
        else:
            return None


    #获取内容,传入页面内容
    def getContent(self,page):
        # pattern = re.compile('<div class="article-body.*?>(.*?)</p>.*?<p><u><strong><a.*?</div>',re.S)
        # pattern = re.compile('<div class="article-body.*?>(.*?)</div>',re.S)
        # pattern = re.compile('<h1 class="headline".*?>(.*?)</h1>',re.S)
        # pattern = re.compile('<h1 class="headline".*?>(.*?)</h1>.*?<p>(.*?)</p>',re.S)
        pattern = re.compile('<article class.*?mainContentOfPage">(.*?)</article>',re.S)
        items = re.findall(pattern,page)
        # print items
        contents = []
        for item in items:
            #将文本进行去除标签处理，同时在前后加入换行符
            content = "\n"+self.tool.replace(item)+"\n"
            contents.append(content.encode('utf-8'))
            # contents.append(content.decode('utf-8','ignore').encode('gb2312','ignore') )
        # print contents
        return contents

    def getAllContents(self,links):
        allarticleTitle=list()
        allcontent = list()
        i=0
        for a in links:
            allPage = self.getPage(a)
            allarticleTitle.extend(self.getArticleTitle(allPage))
            allcontent.extend(self.getContent(allPage))
            print i
            i=i+1
        # allPage = self.getPage(links[0])
        # allarticleTitle.extend(self.getArticleTitle(allPage))
        # allcontent.extend(self.getContent(allPage))
        # allPage = self.getPage(links[1])
        # allarticleTitle.extend(self.getArticleTitle(allPage))
        # allcontent.extend(self.getContent(allPage))   
        # print allarticleTitle[0]
        # for s in range(len(allarticleTitle)):
        #     print allarticleTitle[s]
        #     print allcontent[s]
        print len(links)
        self.write2pdf(allcontent,allarticleTitle)


    def getArticleTitle(self,page):
        pattern = re.compile('<h1><a id=.*?</a>(.*?)</h1>',re.S)
        items = re.findall(pattern,page)
        contents = []
        for item in items:
            #将文本进行去除标签处理，同时在前后加入换行符
            content = "\n"+self.tool.replace(item)+"\n"
            contents.append(content.encode('utf-8'))
            # contents.append(content.decode('utf-8','ignore').encode('gb2312','ignore') )
        # print contents
        return contents


    def getlinks(self,page):
        pattern = re.compile('<li><a href="/qiwsir/StarterLearningPython/blob/master/(.*?).md">.*?</a>.*?</li>',re.S)
        # pattern = re.compile('<li><a href="/wdyggh/StarterLearningPython/blob/master/(.*?).md">.*?</a>.*?</li>',re.S)
        # pattern = re.compile('<li><a href="/wdyggh/(.*?)">.*?</a>.*?</li>',re.S)
        # pattern = re.compile('<p><u><strong><a href="(.*?)" target=.*?</a></strong></u></p>',re.S)
        links = list()
        # links = None
        # links.append(self.baseURL)
        links.extend(re.findall(pattern,page))
        # print links[0]
        for a in range(0,len(links)):
            
            links[a] = 'https://github.com/qiwsir/StarterLearningPython/blob/master/'+links[a]+'.md'
            # links[a] = 'https://github.com/wdyggh/StarterLearningPython/blob/master/'+links[a]+'.md'
            # print links[a]
            # links[a] = 'http://www.eefocus.com/fpga/'+links[a]+'/r0'
        # print links[1]
        # print links[2]
        print "links:  "+str(len(links))
        return links

    def setFileTitle(self,title):
        #如果标题不是为None，即成功获取到标题
        if title is not None:
            self.file = open(title + ".txt","w+")
        else:
            self.file = open(self.defaultTitle + ".txt","w+")

    def writeData(self,contents):
        for item in contents:
            self.file.write(item)
            
    def write2pdf(self,contents,articleTitle):
        reportlab.rl_config.warnOnMissingFontGlyphs = 0
        pdfmetrics.registerFont(TTFont('song',"simsun.ttc"))
        #字体文件  找到下载在代码的文件夹下即可
        pdfmetrics.registerFont(TTFont('hei',"msyh.ttc"))
        #字体文件  找到下载在代码的文件夹下即可
        fonts.addMapping('song', 0, 0, 'song')
        fonts.addMapping('song', 0, 1, 'song')
        fonts.addMapping('song', 1, 0, 'hei')
        fonts.addMapping('song', 1, 1, 'hei')
        stylesheet=getSampleStyleSheet()
        normalStyle = copy.deepcopy(stylesheet['Normal'])
        normalStyle.fontName ='song'
        normalStyle.fontSize = 15
        normalStyle.leading = 25
        normalStyle.firstLineIndent = 20
        titleStyle = copy.deepcopy(stylesheet['Normal'])
        titleStyle.fontName ='song'
        titleStyle.fontSize = 15
        titleStyle.leading = 20
        firstTitleStyle = copy.deepcopy(stylesheet['Normal'])
        firstTitleStyle.fontName ='song'
        firstTitleStyle.fontSize = 20
        firstTitleStyle.leading = 20
        firstTitleStyle.firstLineIndent = 50
        smallStyle = copy.deepcopy(stylesheet['Normal'])
        smallStyle.fontName ='song'
        smallStyle.fontSize = 8
        smallStyle.leading = 8
        story = []
        #enter article title
        # for b in articleTitle:    
        #     story.append(Paragraph(b, firstTitleStyle))
        #     for item in contents:
        #         story.append(Paragraph(item,normalStyle))

        for b in range(len(articleTitle)):    
            story.append(Paragraph(articleTitle[b], firstTitleStyle))
            # for item in contents:
            story.append(Paragraph(contents[b],normalStyle))
        # story.append(Paragraph("<b>test</b>".format(issue), firstTitleStyle))

        # for eachColumn in duzhe:
        #     story.append(Paragraph('__'*28, titleStyle))
        #     story.append(Paragraph('<b>{0}</b>'.format(eachColumn), titleStyle))
        #     for eachArticle in duzhe[eachColumn]:
        #         story.append(Paragraph(eachArticle["title"],normalStyle))

        # story.append(flowables.PageBreak())

        # for eachColumn in duzhe:
        #     for eachArticle in duzhe[eachColumn]:
        #         story.append(Paragraph("<b>{0}</b>".format(eachArticle["title"]),titleStyle))
        #         story.append(Paragraph(" {0}  {1}".format(eachArticle["writer"],eachArticle["from"]),smallStyle))
        #         para=eachArticle["context"].split("　　")
        #         for eachPara in para:
        #             story.append(Paragraph(eachPara,normalStyle))
        #         story.append(flowables.PageBreak())
        # for item in contents:
        #     story.append(Paragraph(item,normalStyle))

        # story.append(Paragraph(contents,normalStyle))
        story.append(Paragraph("END",firstTitleStyle))

        doc = SimpleDocTemplate("StarterLearningPython.pdf")
        print "Writing PDF..."
        doc.build(story)

    def start(self):
        indexPage = self.getPage(baseURL)
        title = self.getTitle(indexPage)
        self.setFileTitle(title)

        try:                
                #page = self.getPage(i)
                page = self.getPage(baseURL)
                links = self.getlinks(page)
                # print page
                # articleTitle = self.getArticleTitle(page)
                # contents = self.getContent(page)
                self.getAllContents(links)

                print "正在写入..."
                # self.writeData(contents)
                # self.write2pdf(contents,articleTitle)
        #出现写入异常
        except IOError,e:
            print "写入异常，原因" + e.message
        finally:
            print "写入任务完成"

#baseURL = 'http://tieba.baidu.com/p/' + str(raw_input(u'http://tieba.baidu.com/p/'))
baseURL = 'https://github.com/qiwsir/StarterLearningPython/blob/master/index.md'

bdtb = BDTB(baseURL)
bdtb.start()

```

最后找到一片将图片转换成pdf的[文章](http://www.jb51.net/article/66595.htm)

<a name="cankao"></a> 



参考1：[Python爬取读者并制作成PDF](http://www.jb51.net/article/61975.htm)

- - - 

###[TOP](#top)
