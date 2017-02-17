# solr-dataimport-scheduler
此项目用于定时增量更新和定时全量更新solr中的数据，含有源码和jar文件，适用solr版本为solr-6.2.0。<br>

基于Apache Solr DataImportHandler Scheduler，感谢原作者。<br>
URL：https://code.google.com/archive/p/solr-data-import-scheduler/<br>

作为一个初学者，参考了liuqingyu的代码，在此表示感谢。<br>
URL：https://github.com/liuqingyu/solr-dataimport-scheduler<br><br>

#### 使用说明：
1.将solr-dataimportscheduler.jar放到solr项目的lib中，然后在solr项目的web.xml中增加listener：<br>
```xml
    <listener>    
    	<listener-class>    
            org.apache.solr.handler.dataimport.scheduler.ApplicationListener    
    	</listener-class>    
  	</listener>
```
2.把jar包中的dataimport.properties文件拷贝到solrhome/conf下(如果没有则创建，注意不是solrhome/core/conf)，然后重启服务即可。<br>

#### dataimport.properties配置项说明:<br>
\#  to sync or not to sync<br>
\#  1 - active; anything else - inactive<br>
syncEnabled=1<br>

\#  which cores to schedule<br>
\#  in a multi-core environment you can decide which cores you want syncronized<br>
\#  leave empty or comment it out if using single-core deployment<br>
syncCores=coretest<br>

\#  solr server name or IP address<br>
\#  [defaults to localhost if empty]<br>
server=localhost<br>

\#  solr server port<br>
\#  [defaults to 80 if empty]<br>
port=8080<br>

\#  application name/context<br>
\#  [defaults to current ServletContextListener's context (app) name]<br>
webapp=solr<br>

\#  URL params [mandatory]<br>
\#  remainder of URL<br>
params=/dataimport?command=delta-import&clean=false&commit=true<br>

\#  schedule interval<br>
\#  number of minutes between two runs<br>
\#  [defaults to 30 if empty]<br>
interval=1<br>

\#  全量更新索引的时间间隔，单位分钟，默认0；<br>
\#  为空,为0,或者注释掉:表示永不全量更新索引<br>
intervalFullImport=3<br>
  
\#  全量更新索引的参数<br> 
paramsFullImport=/dataimport?command=full-import&clean=true&commit=true<br>
  
\#  全量更新索引时间间隔的计时开始时间，第一次真正执行的时间=startTimeFullImport+intervalFullImport*60*1000；<br>
\#  两种格式：2012-04-11 03:10:00 或者  03:10:00，后一种会自动补全日期部分为服务启动时的日期<br>
startTimeFullImport=16:10:00
