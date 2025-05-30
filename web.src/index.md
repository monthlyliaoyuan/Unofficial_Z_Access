# 本版本发行宣言

本版本是Zlibrary的非官方中国客户端，由某个初中生（现高一）编写，其实十分简单。

#### 网页加载可能比较慢（国外服务器）。当前页面也是一个初始加载较慢时的默认页面。

请向下看。

## 使用指南

* 欢迎访问Zlibrary，充满**知识**的地方！
* **鉴于Zlibrary目前遭到FBI和GFW的双重封锁，如果失效请自行进行新配置。或者到github的release界面查看是否有更新。**

请翻到本文结尾，查看使用指南。

我强烈建议你慢慢往下看，以了解我为什么打算写这个，这个安不安全等。

## 安卓使用指南

提示：极其折腾！（对于有安卓ADB经验的除外）

[指南](./help.html#安卓配置指南)

## 发行缘由

Zlibrary遭GFW封锁，Zlibrary官方中国区向中国政府低头。

我们第一反应往往是支持国家的行为的，但是，等等，国家是什么？

按照“中国共产党”的伟大导师（至少表面上）列宁同志在《国际与革命》里所总结马克思恩格斯同志所说：

> 国家是阶级矛盾不可调和的产物，是一个阶级压迫另一个阶级（或多个）的暴力机器。

我们看看中国（名义上的）最高权利机关人民代表大会吧（注意，人民代表是一个完整的名词，不能拆分）。

这是十四届上海的情况（见本文末尾）：

怎么就没有一个一线工农呢？这恐怕是官商大会吧。

所以，GFW？

再次回望历史。

可能上面有一些不知所云，我强烈推荐你阅读以下书籍（都是Zlibrary上的，也帮你验证以下直连效果）：

+ [共和国的历程](https://z-library.rs/book/17447552/cf6795/%E5%85%B1%E5%92%8C%E5%9B%BD%E7%9A%84%E5%8E%86%E7%A8%8B.html)
+ [文革与改开](https://z-library.rs/book/17567345/2280e3/%E6%96%87%E9%9D%A9%E4%B8%8E%E6%94%B9%E5%BC%80.html)

（我并不是说这些书上的内容都是完全对的，但是，这些书的作者的立场我是认同的。也许会出现一些逻辑错误，乃至事实错误，但是立场我是认同的，观点大部分是认同的）

***相信我，这不会浪费你的时间！***

上面你也许能找到关于版权法的论述，看看知网，看看天下霸唱侵权自己的作品鬼吹灯。

人家百度网盘Doc88这种收费的文件网站上有多少没有得到许可的内容？为什么这些大资本没管呢？

### 关于犯罪

或许你可能会说，GFW阻止了电信诈骗与卖淫等，但是，到底是什么导致了电诈和黄色呢？

## 实现原理

Zlib目前遭到GFW的DNS污染与SNI阻断，其挂靠在CloudFlare后面。

我们通过浏览器内改Host来过DNS污染，通过HTTP3QUIC来过SNI阻断。

理论上走CF的都可以这么干。

我再做了一个丢弃sni的功能适配，测试解开了`wikipedia.org`，`torproject.org`, `imgur.com`（主域名，底下一堆cdn和js文件也被墙了，没空一个一个测试）。

接下来看看ECH能不能普及海外。

## 稳定性

**这部分是写给技术人员看的。**

首先无法IP黑洞，因为CloudFlareCDN处理全切30%的流量。

DNS污染无法处理，有很多安全DNS。QUIC可能被处理，有一定漏洞，我们也许应该等待ECH在国外基本普及。

目前QUIC过了3年没被封。（UDP有QoS，但是能用）。

## 安全性

我是没放什么小玩意。

如果你看过上面的参考资料，也会知道我没有理由放。

## 关于更新

本项目完全免费。项目地址：[Github](https://github.com/louiesun/Unofficial_Z_Access)

不会主动推送，请关注[Github Release](https://github.com/louiesun/Unofficial_Z_Access/releases)界面。

[项目主页](https://louiesun.github.io/Unofficial_Z_Access/)

**注意：更新不一定发新版本号，请关注dist文件时间上传时间。**

## 使用指南

好的，到了这里。

#### 请访问[Zlibrary](https://zh.z-library.sk)

#### Zlibrary[线路二](https://zh.singlelogin.re) （会被zlib重定向到线路一）

或者自己去[搜](https://cn.bing.com)个网站玩玩

由于zlib好像最近树敌（FBI，GFW，可能还有其他什么东西）有点多，我也给出另外两个电子图书馆的访问方式。（没错，使用了一些科技）

**请注意！！！！！！由于Zlib的在线阅读莫名奇妙会跳到http，导致quic失效。当你点击在线阅读后会出现连接已重置，此时请复制那个链接，进入下方的[跳转](./jumper.html)，然后改成https协议访问。**

**或者请点击3个点直接下载！！！！！！**

#### 请访问[Anna'sArchive](https://annas-archive.se/)

#### 请访问[LibGen](https://libgen.rs/)

#### 或者使用[跳转](./jumper.html)

#### 想访问Google/Youtube? 一个[网络代理](https://www.croxy.network/)（*与我没有任何关系，且我看下来有大量广告（甚至不少VPN广告，请自行鉴别）。隐私或安全以及可用性问题请自负*）。

软件根据[GPLv3](https://www.gnu.org/licenses/gpl-3.0.html#license-text)提供，源码位于github上。

包括但不限于`index`，`help`，`android`的帮助文档按照[GFDL](https://www.gnu.org/licenses/fdl-1.3.html#license-text)提供。

## [尝试](./download.html)找到下载内容

## 高级使用指南

[help.html](./help.html)（想要[更好的渲染](https://louiesun.github.io/AppsHelp/UZA.html)？）

源码托管于github上。

## 欠你的表


| 姓名   | 职位 | 官职                                                                                                                                         | 党派       |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| 丁奎岭 | 男   | 上海交通大学党委副书记、校长（副部长级），中国科学院院士，中国化学会常务理事，中国产学研合作促进会副会长，上海市科学技术协会常务委员会副主席 | 中共       |
| 王瑞贺 | 男   | 全国人大常委会委员，全国人大宪法和法律委员会委员，全国人大常委会法制工作委员会副主任                                                         | 中共       |
| 水庆霞 | 女   | 上海市体育运动学校女足教练                                                                                                                   | 中共       |
| 田  轩 | 男   | 清华大学五道口金融学院副院长、金融学讲席教授                                                                                                 | 无党派     |
| 史耀斌 | 男   | 全国人大常委会委员，全国人大财政经济委员会副主任委员                                                                                         | 中共       |
| 印  杰 | 男   | 上海科技大学常务副校长（正局长级）                                                                                                           |            |
| 印海蓉 | 女   | 上海广播电视台、上海文化广播影视集团有限公司融媒体中心主持人（首席）                                                                         | 中共       |
| 权  衡 | 男   | 上海社会科学院党委书记                                                                                                                       | 中共       |
| 师延财 | 男   | 中国核工业建设股份有限公司高级技能大师，中核检修有限公司首席技能专家、中核检修焊接虚拟队队长、福清分公司一厂项目副经理                       | 中共       |
| 朱丽平 | 女   | 中国铁路上海局集团有限公司财务部会计科科长                                                                                                   | 民盟       |
| 朱建弟 | 男   | 上海市工商联副主席，市注册会计师协会会长，立信会计师事务所（特殊普通合伙）首席合伙人、董事长，BDO 德豪国际会计师事务所全球董事会董事         | 中共       |
| 刘  多 | 女   | 上海市副市长，上海国际旅游度假区管委会主任                                                                                                   | 中共       |
| 刘云志 | 男   | 中央歌剧院院长、艺术总监，中国音乐家协会弦乐学会会长                                                                                         |            |
| 刘懿艳 | 女   | 上汽集团零束科技有限公司党委副书记、纪委书记、工会主席                                                                                       | 中共       |
| 汤  亮 | 男   | 全国工商联副主席，上海市普陀区人大常委会副主任（不驻会），奥盛集团有限公司董事长                                                             |            |
| 许  忠 | 男   | 上海歌剧院院长                                                                                                                               | 农工       |
| 许保云 | 女   | 上海化工研究院有限公司总工程师                                                                                                               | 中共       |
| 李  丰 | 男   | 上海熊猫机械（集团）有限公司采购经理                                                                                                         | 无党派     |
| 李  峻 | 男   | 上海市崇明区委副书记、区长                                                                                                                   | 中共       |
| 李仰哲 | 男   | 中共中央纪委委员，上海市委常委、市纪委书记，市监察委主任                                                                                     | 中共       |
| 李海泳 | 男   | 上海市政协常务委员、兼职副秘书长，台盟上海市委专职副主委                                                                                     | 中共、台盟 |
| 吴一戎 | 男   | 全国人大常委会委员，全国人大教育科学文化卫生委员会委员，中国科学院空天信息创新研究院院长，中国科学院院士                                     | 中共       |
| 吴焕淦 | 男   | 上海中医药大学市针灸经络研究所所长                                                                                                           | 民进       |
| 张  为 | 男   | 中共上海市委常委、市委组织部部长                                                                                                             | 中共       |
| 张  帆 | 男   | 中国电气装备集团有限公司科技创新部部长                                                                                                       | 中共       |
| 张义民 | 男   | 上海市闵行区浦锦路街道芦胜村党总支书记、村委会主任                                                                                           | 中共       |
| 张素心 | 男   | 上海华虹（集团）有限公司党委书记、董事长                                                                                                     | 中共       |
| 陈  达 | 女   | 东浩兰生集团上海工业商务展览有限公司能源展部经理、工会副主席                                                                                 |            |
| 陈  勇 | 男   | 上海市人民检察院检察长、党组书记                                                                                                             | 中共       |
| 陈吉宁 | 男   | 中共中央政治局委员，上海市委书记                                                                                                             | 中共       |
| 陈众议 | 男   | 全国人大教育科学文化卫生委员会委员，中国社会科学院学部委员，国家文科一级教授                                                                 | 中共       |
| 其  实 | 男   | 民建上海市委副主委，东方财富信息股份有限公司董事长                                                                                           | 民建       |
| 范先群 | 男   | 上海交通大学副校长，上海交通大学医学院党委副书记、院长，中国工程院院士                                                                       | 中共       |
| 杭迎伟 | 男   | 上海建工集团股份有限公司党委书记、董事长                                                                                                     | 中共       |
| 金  力 | 男   | 复旦大学党委副书记、校长（副部长级），复旦大学上海医学院党委副书记、院长，中国科学院院士                                                     | 中共       |
| 金鹏辉 | 男   | 中国人民银行上海总部党委副书记、副主任，上海市分行行长兼国家外汇管理局上海市分局局长                                                         | 中共       |
| 周桐宇 | 女   | 上海市工商联副主席，威达高科技控股有限公司董事长                                                                                             | 民革       |
| 周新民 | 男   | 中国商用飞机有限责任公司副董事长、总经理、党委副书记                                                                                         | 中共       |
| 周燕芳 | 女   | 太平洋医疗健康管理有限公司总经理                                                                                                             | 中共       |
| 单渭祥 | 男   | 中国基督教三自爱国运动委员会驻会副主席                                                                                                       |            |
| 赵进才 | 男   | 农工党中央常委，中国科学院化学研究所研究员，中国科学院院士                                                                                   | 农工       |
| 姚卓匀 | 女   | 上海市政协副秘书长，民盟上海市委专职副主委（正局长级）                                                                                       | 民盟       |
| 袁国华 | 男   | 上海临港经济发展（集团）有限公司党委书记、董事长，中国（上海）自由贸易试验区临港新片区党工委副书记                                           | 中共       |
| 贾  宇 | 男   | 上海市高级人民法院院长、党组书记                                                                                                             | 中共       |
| 顾  军 | 男   | 上海市政府副秘书长，市发展改革委主任、党组书记                                                                                               | 中共       |
| 顾祥林 | 男   | 民盟上海市委副主委，同济大学特聘教授，工程结构性能演化与控制教育部重点实验室主任                                                             | 民盟       |
| 倪  迪 | 男   | 中远海运船员管理有限公司上海分公司油运库船长                                                                                                 | 中共       |
| 黄莉新 | 女   | 上海市人大常委会主任、党组书记                                                                                                               | 中共       |
| 黄勇平 | 男   | 上海交通大学环境科学与工程学院特聘教授                                                                                                       | 九三学社   |
| 梅  兵 | 女   | 华东师范大学党委书记                                                                                                                         | 中共       |
| 龚  正 | 男   | 中共中央委员，上海市委副书记、市长、市政府党组书记                                                                                           | 中共       |
| 龚新高 | 男   | 复旦大学物理学系教授、计算物质科学教育部重点实验室主任、计算物质科学研究所所长，中国科学院院士                                               | 致公       |
| 盛  弘 | 女   | 上海市长宁区虹桥街道古北荣华第四居民区党总支书记                                                                                             | 中共       |
| 蒋卓庆 | 男   | 全国人大常委会委员，全国人大监察和司法委员会副主任委员                                                                                       | 中共       |
| 程学源 | 男   | 全国人大常委会委员，全国人大华侨委员会委员，中国侨联党组成员、副主席                                                                         | 中共       |
| 谢坚钢 | 男   | 上海市人大常委会党组成员、秘书长，机关党组书记                                                                                               | 中共       |
| 樊  芸 | 女   | 上海市商标品牌协会会长、市房地产估价师协会会长，中国房地产估价师与经纪人学会副会长，上海富申评估咨询集团董事长                               |            |

来源：上海发布（他们小编竟然敢发这种东西，要知道其他省都是不发的）
