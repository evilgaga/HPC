#### cmake 使用

1. 先创建CMakeLists.txt,在里面定义文件的编译过程，包括语音和顺序

2. cmake .
3. make

#### CMakeLists.txt 中指令

1. PROJECT (projectname [CXX] [C] [Java])

​	用这个指令定义工程名称，并且可以指定工程支持的语言，支持的语言列表是可以忽略的，默认情况表示支持所有语言。

​	这个指令隐式的定义了两个cmake的变量：

​				 <projectname>_BINARY_DIR
​				<projectname>_SOURCE_DIR

​	这两个变量可以用下面方式表示（这样不用担心写错工程名称）

​				PROJECT_BINARY_DIR
​				PROJECT_SOURCE_DIR

2. SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]])

    SET指令可以用来显式地定义变量。如：

   ​	`SET(SRC_LIST main.c)`

​        如果有多个源文件，也可以定义为：

​		`SET(SRC_LIST main.c t1.c t2.c)`

3. MESSAGE([SEND_ERROR | STATUS | FATAL_ERROR] "message")

   这个指令是向终端输出用户定义的信息，包含三种类型：

```Bash
		SEND_ERROR     #产生错误，生成过程被跳过。
		STATUS     #输出前缀为--d的信息。
		FATAL_ERROR    #立即终止所有的cmake过程。
```



4. ADD_EXECUTABLE(hello ${SRC_LIST})

   定义了一个为hello的可执行文件，相关的源文件是SRC_LIST中定义的源文件列表。

5. 参数之间使用空格或者分号分隔开。

   如果加入一个 fun.c

   ```bash
   ADD_EXETABLE(hello main.c;fun.c)
   ```

   指令是大小写无关的，参数和变量是大小写相关的。但是推荐你全部使用大写指令。

6. 关于语法的困惑

   可以使用双引号“”将源文件包含起来。

   处理特别难处理的名字比如fun c.c，则使用SET(SRC_LIST "fun c.c")可以防止报错。

7. 清理工程
   可以使用   `make clean`  清理makefile产生的中间的文件，但是，不能使用`make distclean`清除cmake产生的中间件。如果需要删除cmake的中间件，可以采用`rm -rf ***`来删除中间件。

8. 外部构建
   在目录下建立一个build文件用来存储cmake产生的中间件，不过需要使用`cmake ..`来运行。

   其中外部编译，**PROJECT_SOURCE_DIR** 仍然指代工程路径，即**/backup/cmake/t1**，而**PROJECT_BINARY_DIR**指代编译路径，即**/backup/cmake/t1/build**。
   

9. `ADD_SUBDIRECTORY(source_dir [binary_dir] [EXCLUDE_FROM_ALL] )`

   这个指令用于向当前工程添加存放源文件的子目录,并可以指定中间二进制和目标二进制存放的位置。EXCLUDE_FROM_ALL参数的含义是将这个目录从编译过程中排除，比如，工程中的example，可能就需要工程构建完成后，再进入example目录单独进行构建（当然，你可以通过定义依赖来解决此类问题）。

​						`add_subdirectory(src bin)`

​	定义了将src子目录加入工程，并指定编译输出（包含编译中间结果）路径为bin目录。如果不进行bin目录的指定，那么编译结果（包括中间结果）都将存放在build/src目录（这个目录跟原来的src目录对应），指定bin目录后，相当于在编译时将src重命名为bin，所有的中间结果和目标二进制都贱存放在bin目录中。

​	如果在上面的例子中将ADD_SUBDIRECTORY(src bin)改成SUBDIRS(src)。那么在build目录中将出现一个src目录，生成的目标代码hello将存在在src目录中。

