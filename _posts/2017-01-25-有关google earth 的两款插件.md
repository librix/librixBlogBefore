# 2017-01-25-有关google earth 的两款插件

问题起源于：如何使用google earth pro版导出高程？

通过查找，似乎有两款插件可以满足基本需求：

- TCX Converter

  With TCX Converter you can:

  1. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Import TCX, GPX, FITLOG, KML, TRK (and more to come...) files
  2. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Join multiple GPX files into one big course
  3. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Import directly from Garmin GPS via Garmin Communicator Plugin or GPSBabel plugin
  4. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Add or remove Waypoints with a simple mouse click
  5. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Truncate the track at any point you like
  6. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Update altitude data (internet connection needed)
  7. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Change average speed of the course
  8. ![Punti elenco](http://www.tcxconverter.com/TCX_Converter/TCX_Converter_ENG_files/Graphpaper_bullet_default.png)Import/Export Waypoints with smart repositioning function

- QuikGrid

  ​

  因为Google地球里面是有数据的，所以只要有插件就可以将它导出。两个都是免费软件。

导出数据：.格式用Kml格式。

使用TCX Converter，加载进来。加载之后选择Update Altitude，这时会联网下载Google的海拔数据，下载之后，ALT这一栏就有数据了，这就是海拔高度。

可以导出为CSV格式。

​	视频教程：https://www.youtube.com/watch?v=pbs7bhv7HgQ

仅保留LAT 、LONG、ALT三列数据，导入QuikGrid,即为等高线。之后，可以导出至CAD.

> 细节：
>
> - Distance between Labeledbold Lines就是指间隔多少加粗写出高差。
> - polylines选起来，会把等高线变为连接的线段。

# SRTM数据

除了以上解决方案以外，还有知道了SRTM数据，配合Global Mapper 使用。

## xSRTM数据是什么？

由美国太空总署(NASA)和国防部国家测绘局(NIMA)联合测量的，全称Shuttle Radar Topography Mission。

SRTM数据每经纬度方格提供一个文件，精度有1 arc-second和3 arc-seconds两种，称作SRTM1和SRTM3,或者称作30M和90M数据(每个90米的数据点是由9个30米的数据点算术平均得来的)，SRTM1的文件里面包含3601*3601个采样点的高度数据，SRTM3的文件里面包含1201*1201个采样点的高度数据。

## SRTM数据下载

        SRTM数据下载地址：http://srtm.csi.cgiar.org/SELECTION/inputCoord.asp。

- ​	我国境内的数据在Eurasia目录下

  - 每经纬度方格一个文件，文件命名方法是X1X2X3X4.hgt.zip，
  - X1是N或 S表示南北，X2是下方纬度数，X3是E或W表示东西，X4是左方经度数。 

- Documentation目录下有这些数据的介绍。 

  ​

  ## GeoCover是什么？ 

          GeoCover是使用LANDSAT5卫星（美NASA于1984年3月1日发射的地球观测卫星）在1990年左右采集的数据合成的，公开的三波段遥感合成图像。LANDSAT5 TM(Thematic Mapper)有7个波段： 
  波段1:0.45–0.52um蓝绿波段

  波段2:0.52- 0.60绿色波段 

  波段3:0.63 - 0.69红色波段 

  波段4:0.76-0.90um近红外波段 
  波段7:2.08-2.35um短红外波段 
           其中波段1-5和7为可见光及近红外波段，分辨率为30米，波段6为热红外光分辨率为120 米。

LANSAT5每景扫描耗时约26.31秒，覆盖185公里×170公里 ，扫描影像重叠率超过10%。

 GeoCover使用了742波段分别作为红色、绿色和蓝色进行了假彩色合成，也许如果使用1、 2、3三种可见光波段合成的话会使我们看起来更舒服一些，不过我们现在能拿到的只能是这种742的合成假彩，通过观察发现其中的绿色通道对地形有较好的反应，实际操作中可以将这种假彩图像反相取其中的绿色通道来作为地形底图。

## GeoCover的下载

 GeoCover的下载地址是：https://zulu.ssc.nasa.gov/mrsid。可从全球地图页面上选择需要的区域下载。

- GeoCover图像文件使用WGS84 UTM坐标，采用TIFF或MrSID格式分发，图像中每个像素28.5M-30M,一般以28.5M计算。

- GeoCover文件每个在东西方向跨越一个UTM分区，在南北方向跨越5个纬度，东西提供50KM的富裕，南北提供1KM的富裕。文件命名方法是X1-X2-X3.tar，X1是N或S表示南北，X2是UTM带数，X3下方经度数。 

  ## 其他地理信息数据库

          NIMA地名数据库:可以提供大多数国家的地名英文拼写及坐标,包含中国境内大约6万个地方, 可以在以下地址下载中国地名库 ftp://ftp.nga.mil/pub/gns ;data/cn.zip。 
          SPACEIMAGING 1M分辨率卫星图像预览:虽然只能免费得到预览图像，但其分辨率也已经不算太低了，并且可以随预览图提供图像的一些数据信息，非常方便将图像用工具软件进行较正，下载地址: http://www.spaceimaging.com/default.htm ; 
         国家基础地理信息系统:国家基础地理信息系统全国1:400万数据库全部数据均可浏览。其中，中国国界、省界、地市级以上居民地、三级以上河流、主要公路和主要铁路等数据可以自由下载。 地址为：http://nfgis.nsdi.gov.cn/nfgis/chinese/cxz.htm

         从公开发行的地图上获取数据信息:可以直接从某些电子地图提取到不错的数据；也可以从纸介地图上测量或数字化某些信息，目前正在进行这方面的试验，已取得一定量数据。  

# 其他

### Goody Geographic Information System

##### 英文简称： GoodyGIS

谷地是一款基于谷歌地球API开发的应用软件，旨在扩展谷歌地球的应用，辅助获取数据，提高工作效率。可应用于学术科研、工程、规划、设计等工作，在测绘、地质、交通、电力、水利、农业、林业、能源和旅游等领域，应用广泛。

[朴自然](http://www.puziran.com/index.html)的教程：www.puziran.com/tovideo.html?courseUrlId=83

利用**OGC协议**打开地图资源：http://blog.3snews.net/space.php?uid=6955280&do=blog&id=67981