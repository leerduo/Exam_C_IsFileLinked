题目的链接来自[这里](http://blog.csdn.net/simao234430/article/details/17189437)

C语言的某链接器有如下规则：

如果一个文件中至少有一个函数被主函数直接或间接调用，此文件会被Link进来；否则此文件不会被Link进来。

现有一组文件，给出文件与函数的关系、函数之间的调用关系，要求判断在上述链接规则下指定文件是否会被Link进来。

为了简化处理，文件和函数均用id来进行标识。

主函数的id固定为`11`

* 文件id，函数id都为正整数

* 1 <= 文件id <= 5000， 1 <=函数id <= 5000

* 文件个数<= 100，单文件中函数个数<=50

* 一个函数只能属于一个文件，一个文件中至少有一个函数

* 不存在直接或间接的函数递归调用

* 系统中有id为11的主函数（用例添加）

以上规格均由用例保证.

 
 ```C++
 int AddFile(unsigned int file_id, unsigned int func_id_array[],

  unsigned int  func_num)

功能：添加一个文件，以及这个文件内的所有函数

输入：

   file_id                   文件id

            func_id_array            函数id数组，用例保证数组内元素不重复

     func_num              函数个数

输出：无 

返回：

          执行成功返回0，失败返回-1。失败原因包括文件id已经存在，函数id已经存在，以及其他各种可能导致程序异常的非法参数

          返回-1时，本次输入全部无效

``` 

 


```C++
 int AddCallList(unsigned int caller_id, unsigned int callee_id_array[],        unsigned int  callee_num)

功能：添加一个函数的直接调用关系，可以多次增加

输入：

     caller_id           调用者函数id

     callee_id_array     被调用的函数id数组，用例保证数组内元素不重复，数组内    元素个数不为0

     callee_num                被调用的函数个数，用例保证函数个数不为0

输出：无 

返回：

      执行成功返回0，失败返回-1，失败包括函数id不存在，以及其他各种可能导致程序异常的非法参数

      返回-1时，本次输入全部无效
```
 

 
```C++
int IsFileLinked(unsigned int  file_id)

功能：判断一个文件是否会被Link进来

输入：

           file_id        文件id

输出：无 

返回：

           该文件会被Link进来返回0，不会被Link进来返回-1（包括文件id不存在等
```


提供cppunit的测试框架，VC测试工程中提供了测试样例，请大家参考具体工程：

Reference

Header File  : #include "CExampleTest.h"

Source File  : “CExampleTest.cpp”

Description  : 测试用例声明在“CExampleTest.h”中

测试用例实现在"CExampleTest.cpp"

1.测试框架只为方便员工自行测试而提供,不对测试代码评分
2.完备的测试不限于工程中的测试样例,请根据需求, 自行添加测试用例

 

1、考生完成答题后，把工程中的source目录直接

打包成source.rar，请自行保证完成的所有源文件

以及头文件都在source目录中。

2、再创建文件夹把source.rar放入，文件打包名称规定：部门_考试类别_姓名_工号。例如：OSS_c,c++_张三_12345。

附：部门列表：OSS、GUL、中射频、PS、LTE、平台、工具、CL、企业无线、天馈与室分、WTL

 

 

main.cpp


```C++
#include <cppunit/TextOutputter.h>
#include <cppunit/XmlOutputter.h>
#include <cppunit/BriefTestProgressListener.h>
#include <cppunit/extensions/TestFactoryRegistry.h>
#include <cppunit/TestResult.h>
#include <cppunit/TestResultCollector.h>
#include <cppunit/TestRunner.h>

int main(int argc, char* argv[])
{
    // Create the event manager and test controller
    CPPUNIT_NS::TestResult controller;

    // Add a listener that colllects test result
    CPPUNIT_NS::TestResultCollector result;
    controller.addListener( &result );

    // Add a listener that print dots as test run.
    CPPUNIT_NS::BriefTestProgressListener progress;
    controller.addListener( &progress );

    // Add the top suite to the test runner
    CPPUNIT_NS::TestRunner runner;
    runner.addTest( CPPUNIT_NS::TestFactoryRegistry::getRegistry("All Tests").makeTest() );
    runner.run( controller );

    // Print test in a text format.
    CPPUNIT_NS::TextOutputter outputter( &result, CPPUNIT_NS::stdCOut() );
    outputter.write();

    // This for XML output
    std::ofstream file( "TestResult.xml" );
    CPPUNIT_NS::XmlOutputter xml( &result, file );
    xml.setStyleSheet( "report.xsl" );
    xml.write();
    file.close();

    return result.wasSuccessful() ? 0 : 1;
}
```
 

Linker.h
```C++

#ifndef _LINKER_H_
#define _LINKER_H_

int AddFile(unsigned int file_id, unsigned int func_id_array[],unsigned int func_num);
int AddCallList(unsigned int caller_id, unsigned int callee_id_array[], unsigned int callee_num);
int IsFileLinked(unsigned int file_id);

#endif
```
 

Linker.cpp

```C++
#include "Linker.h"


/******************************************************************************
功能：添加一个文件，以及这个文件内的所有函数
输入：
    file_id                文件id
    func_id_array          函数id数组，用例保证数组内元素不重复
    func_num               函数个数
输出：
    无
返回：
    0：成功，-1：失败
******************************************************************************/
int AddFile(unsigned int file_id, unsigned int func_id_array[],unsigned int func_num)
{
 return 0;
}


/******************************************************************************
功能：添加一个函数的直接调用关系，可以多次增加
输入：
  caller_id        调用者函数id
  callee_id_array  被调用的函数id数组，用例保证数组内元素不重复，数组内元素个数不为0
  callee_num          被调用的函数个数，用例保证函数个数不为0

输出：
  无
返回：
  0：成功，-1：失败
******************************************************************************/
int AddCallList(unsigned int caller_id, unsigned int callee_id_array[], unsigned int callee_num)
{
 return 0;
}


/******************************************************************************
功能：判断一个文件是否会被Link进来
输入：
   file_id    文件id
输出：
   无
返回：
   该文件会被Link进来返回0，不会被Link进来返回-1（包括文件id不存在等）
******************************************************************************/
int IsFileLinked(unsigned int file_id)
{
 return 0;
}
```

 

CExampleTest.h
```C++
#ifndef _CEXAMPLE_TEST_H
#define _CEXAMPLE_TEST_H

#include <cppunit/extensions/HelperMacros.h>

class CExampleTest : public CPPUNIT_NS::TestFixture
{
    CPPUNIT_TEST_SUITE(CExampleTest);
 CPPUNIT_TEST(TestCase01);

    CPPUNIT_TEST_SUITE_END();

public:
    void setUp();
    void tearDown();

 void TestCase01();

};

#endif /*_CEXAMPLE_TEST_H*/
```
 

CExampleTest.cpp

```C++

#include "CExampleTest.h"

#include "Linker.h"


// 注册测试套到CppUnit
CPPUNIT_TEST_SUITE_REGISTRATION( CExampleTest );


// SetUp: 在每个用例前执行一次
void CExampleTest::setUp()
{

}

// tearDown: 在每个用例后执行一次
void CExampleTest::tearDown()
{
   
}


void CExampleTest::TestCase01()
{
 unsigned int file_1_func_array[] = {11,12};
 unsigned int file_2_func_array[] = {21,22};
 unsigned int file_3_func_array[] = {31,32,33};
 unsigned int file_4_func_array[] = {41,42,43};
 unsigned int file_5_func_array[] = {51,52};

 CPPUNIT_ASSERT(0 == AddFile(1,file_1_func_array,2));

 CPPUNIT_ASSERT(0 == AddFile(2,file_2_func_array,2));

 CPPUNIT_ASSERT(0 == AddFile(3,file_3_func_array,3));

 CPPUNIT_ASSERT(0 == AddFile(4,file_4_func_array,3));

 CPPUNIT_ASSERT(0 == AddFile(5,file_5_func_array,2));

 unsigned int callee_name_array_11[] = {12,21};
 unsigned int callee_name_array_21[] = {32,41};
 unsigned int callee_name_array_32[] = {33};
 unsigned int callee_name_array_41[] = {42,43};
 unsigned int callee_name_array_42[] = {22};
 unsigned int callee_name_array_51[] = {52};

 CPPUNIT_ASSERT(0 == AddCallList(11,callee_name_array_11,2));

 CPPUNIT_ASSERT(0 == AddCallList(21,callee_name_array_21,2));

 CPPUNIT_ASSERT(0 == AddCallList(32,callee_name_array_32,1));

 CPPUNIT_ASSERT(0 == AddCallList(41,callee_name_array_41,2));

 CPPUNIT_ASSERT(0 == AddCallList(42,callee_name_array_42,1));

 CPPUNIT_ASSERT(0 == AddCallList(51,callee_name_array_51,1));


 CPPUNIT_ASSERT(0 == IsFileLinked(1));

 CPPUNIT_ASSERT(0 == IsFileLinked(2));

 CPPUNIT_ASSERT(0 == IsFileLinked(3));

 CPPUNIT_ASSERT(0 == IsFileLinked(4));

 CPPUNIT_ASSERT(-1 == IsFileLinked(5));


 return;
}
```
