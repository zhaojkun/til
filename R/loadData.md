##### 从带分隔符的文本文件中导入数据

* mydataFrame<-read.table(file,header=logical_value,sep="delimiter",row.names="name")
* read.csv,read.csv2,read.delim,read.delim2等都是read.table的特例
* 默认情况下，字符型变量将转换为因子，有很多方法可以禁止这种转换行为，其中包括设置选项`stringsAsFactors=FALSE`

##### 导入`Excel`数据

* 读取一个Excel文件的最好方式，就是在Excel中将其导出为一个逗号分隔文件`(csv)`，并使用前文描述的方式将其导入R中。在`Windows`中，你也可以使用`RODBC`包来访问Excel文件。

* ```R
  install.packages("RODBC")
  library(RODBC)
  channel<-odbcConnectExcel("myfile.xls")
  mydataFrame<-sqlFetch(channel,"mysheet")
  odbcClose(channel)
  # 这里myfile.xls是excel文件，mysheet是要从整个工作簿中读取工作表的名称
  ```
  
 ```
  library(xls) # Excel2007读取方式
  workbook<-"c:/myworkbook.xlsx"
  mydataframe<-read.xlsx(workbook,1)
  ```

#####数据库

* DBI
* R中有一个库为`sqldf`，能够在R中使用`sql`语句对`dataframe`进行处理。不过这里写的是R中与sql相关语法的对应关系。

| `sqldf` |  `normal R`  |
| ---------------------------------------- | ---------------------------------------- |
| `s01<-sqldf("select Type,conc from myCO2")` | `ro1<-myCo2[,c("Type","conc")]`          |
| `s01<-sqldf("select * from myCO2")`      | `r01<-myCO2[，]`                          |
| `s05<-sqldf("select * from myCO2 where uptake<20")` | `r05<-myCO2[myCO2[,"uptake"]<20,]`       |
|                                          | `r05w<-with(myCO2,myCO2[update<20,])`    |
| `s06<-sqldf(select * from myCO2 where uptake<20 and Type='Quebec')` | `r06<-with(myCO2,myCO2[uptake<20 & Type=='Quebec',])` |
| `s09<-sqldf("select * from r08 where plant is not null")` | `r09<-with(r08,r08[!is.na(Plant),])`     |

