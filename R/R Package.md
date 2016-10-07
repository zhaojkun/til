# R Package

* 使用 `R studio`创建R的包框架

* 使用`R studio`右上方的`check`按钮进行包的功能性检查，包括依赖，导出等。这个过程实际调用的函数为`devtools:check(document=FALSE)`

  可在命令行使用使用`devtools::check()`，进行包检查。这个过程同时更新文档及`namespace`文件

  这个过程主要检查包是否符合`CRAN`的要求。目前来看一般来说，需要添加足够的文档。如函数的作用，函数的参数及返回值，依赖了那些包（这个跟下边讲的依赖貌似关系不大），是否导出某些函数等。

* 如果新建包中的某个函数依赖其他库（如：`ggplot2`）中的函数有如下三种解决方案：

  * 在函数中使用`library`，如`library(ggplot2)`

  * 调用依赖库函数时使用`::`，如`ggplot2::qplot`

  * 在`DESCRIPTION`文件中添加`Imports:`，并在该列表中添加需要的包，如：

    ```ini
    Imports:
    	ggplot2
    ```

    可使用`devtools::usepackage()`函数来自动添加

* 使用`devtools::usetestthat()`添加`testthat`，并生成测试文件框架

  然后在`./tests/testthat`文件夹下创建`test-`开头的R测试脚本文件，如下是一个示例测试文件：

  ```R
  expect_identical(jkadd(1,1),2)
  ```



  ​
