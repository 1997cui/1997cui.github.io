---
layout: post
title:  "告别Certified Mail: 让USPS贴邮票的平信(First-Class Mail)可追踪"
date: 2021-06-03
categories: 生活
tags:
 - USPS
 - IMb
 - Barcode
 - IV-MTR
 - Certified Mail
 - Tracking
 - Stamp
 - First class Mail
 - 平信
 - 追踪
 - 邮票
---
**Disclaimer: 对于按本文寄信给IRS却寄丢了的，本人概不负责**

邮局和平信作为一种在中国已经消声觅迹淘汰多年的产物，在美国不但普遍却还历久弥新。在美国的大家一定对USPS非常熟悉，每天一打开信箱里面就充满了各种各样花花绿绿的广告信件，甚至还有麦当劳的优惠券。同时，我们时不时的总是无法逃离USPS的股掌——时不时的我们需要用邮局向外寄一些信，比如给IRS的退税。甚至可能有时还需要寄表格，SSN复印件等内容。

对于这类文件，之前每次小崔我搞起来都十分头大：需要跑一趟邮局买信封邮票。我还不太敢放到信封里，像IRS这种机构很容易石沉大海，根本不知道是不是路上寄丢了。为此，还得在邮局排队买一个叫[Certifed Mail](https://www.usps.com/ship/insurance-extra-services.htm)的额外服务（截至2021年6月3日，收费3.6美元）。后来，因为COVID-19在家工作，先添置了打印机，接着我又屯了些邮票和信封，鼓捣了一下如何用打印机打印信封。这下我终于可以在家打印好材料贴好邮票直接塞到邮筒里了，但邮件可能石沉大海无法追踪的问题并没有解决。最近我摸鱼时鼓捣了一下，终于做到了可以让直接丢进邮筒贴1oz邮资的普通信封可以追踪了。终于做到了*足不出楼用一张邮票钱搞定可追踪平信*。

## 前提条件
 - 打印机一台（可以打印信封）
 - 信封（可以被打印）
 - 邮票
 - Office全家桶

## 工作原理
{:refdef: style="text-align: center;"}
{% include image.htm url="/wp-content/uploads/2021/USPSIVMTR/samplemail.png" description="带IMb的信封示例, 来自网络" %}
{: refdef}
上图是一个我从网上找到的信封示例图。不知大家仔细观察过收到的信没有，每封信右下角或者收件人地址区域里面都有一个这样奇形怪状的条码。USPS在处理信件的时候，每一封信都会通过各式各样的机器，每一台机器通过扫描这个条码来判断出这封信的目的地在哪里并进行自动分拣。我们在邮局寄的信第一次过的机器就是把邮票上盖邮戳(postage cancellation)和打印条码了。当然，这个条码也可以用来追踪信件，只要条码在45天内在系统里唯一。

不过需要注意的是，因为USPS贴邮票的平信并不是每一条都会过机器扫描的（运输时成盒(Container)的直接送到目的地），同时最后邮差送信时也是不扫描的，所以一般能拿到的tracking只有刚刚进入系统和接近投递前的最后一次分拣，详细程度远远比不上Certified Mail。

此外，不知道大家有没有用过USPS的[Informed Delivery](https://informeddelivery.usps.com/box/pages/intro/start.action)功能，它就是利用条形码确定哪封信是寄给你家的，然后每天发邮件给你。

我们需要做的事情就是自己把条形码（这个条码称之为[IMb (Intelligent Mail Barcode)](https://postalpro.usps.com/mailing/intelligent-mail-barcode)）打印到信封上，然后用某种方式追踪到就可以了。

## TL;DR
偷懒的同学建议注册并交钱使用[Letter Track Pro](https://www.lettertrackpro.com/) (并没有人给我广告费，自己也没有用过)

## 完整版教程

### 下载安装条形码对应的字体以及Word信封模板

所有的文件都在[USPS IMb Fonts and Encoders Download](https://postalpro.usps.com/onecodesolution)能够下载到。其中我们最需要的是``uspsEncoderMsOffice64-1.3.1.zip``和``uspsFontsNonAFP-1.4.0.zip``。第一个是office的模板，第二个是字体，在``fonts\scalable\trueType``有TrueType字体可以使用。

接着大家到安装目录下找到``Excel\IM Barcode Envelope Size 10.doc``打开使用就好啦，具体使用自己看教程即可。

### 注册并使用tracking服务

这个追踪IMb平信的服务叫做[Informed Visibility](https://iv.usps.com)，虽然只面向商业用户开放，但注册起来其实并没什么问题，个人完全可以注册。注册入口不是很好找，分为以下几步：
1. 在[USPS Business Customer Gateway](https://gateway.usps.com)根据提示注册一个账户，注册好之后不要被眼花撩乱的东西吓到，接着往下看。
2. 按如图点击。
   ![步骤2](/wp-content/uploads/2021/USPSIVMTR/reg_getaccess.png)
3. 点击``Get Access``，然后等一会等USPS审核。
4. 接下来[Informed Visibility](https://iv.usps.com)应该就可以可以进去了

### 打印信件，寄信

使用上面下载的excel和word模板文件即可。zipcode可以5位，9位，11位都可以，但要填对。Zipcode可以用[USPS Lookup a ZIP Code](https://tools.usps.com/zip-code-lookup.htm)查到。11位的最后两位是delivery point。

Barcode identifier参考[这个](https://postalpro.usps.com/node/3528)文档，Service Type identifier (STID)参考[这个](https://postalpro.usps.com/service-type-identifiers/stidtable)文档。截至2021年6月3日，我自己Barcode identifer填写``00``, STID填写``040``可以让信被追踪到。

[Intelligent Mail® Barcode Technical Resource Guide](https://postalpro.usps.com/node/221)里详细讲了条码的每一个字段怎么填。我序列号(Serial Number)从``000001``开始进行的编号。

Mailer ID (MID)在[这里](https://mid.usps.com)可以查询到。

最后使用一下Office Word的邮件合并和信封打印功能，再折腾一下打印机即可把发件人和收件人以及条码打印到信封上了。USPS提供了一个[条码编解码工具(encoder decoder)](https://postalpro.usps.com/ppro-tools/encoder-decoder), 不会使用Word的同学也可以用这个工具按上文所述把字段填好，然后把条码画到信封上。*注意，对画在哪里有[位置要求](https://pe.usps.com/text/dmm300/202.htm#ep1047220)*:dog:

最后，把信封贴上邮票，把内容放进去，丢到楼下的~~垃圾桶~~邮筒里即可。

### 查看追踪信息

进入[Informed Visibility](https://iv.usps.com)，创建一个query，注意Step 2要选Download而非Online View, Step 3``Object Type``选择Piece.
{:refdef: style="text-align: center;"}
{% include image.htm url="/wp-content/uploads/2021/USPSIVMTR/query.png" description="IV query 设置filter" %}
{: refdef}

铛铛铛，我们得到了如下结果。
{:refdef: style="text-align: center;"}
{% include image.htm url="/wp-content/uploads/2021/USPSIVMTR/result.png" description="IV query result" %}
{: refdef}

至于每个字段是什么含义，请参考[IV®-MTR Operation Codes List](https://postalpro.usps.com/informedvisibility/OperationCodesList)和[IV-MTR Data Directory](https://postalpro.usps.com/informedvisibility/DataDictionary)。

