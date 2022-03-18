---
title: ServletContext
date: 2022-03-18 23:36:48 +0800
category: Java
tags: servlet
excerpt: 关于ServletContext（上下文对象）
---



## ServletContext

### ServletContext概述

- ServletContext：是一个全局对象，上下文对象。


- 服务器为每一个应用(项目)都创建了一个ServletContext对象。
- ServletContext是属于整个应用的，不局限于某个Servlet。

- ServletContext的作用：
  - 作为域对象存取数据，让Servlet共享
  - 获得文件MIME类型(文件下载)
  - 获得全局初始化参数
  - 获取web资源路径，可以将Web资源转换成字节输入流

---

### ServletContext的功能

#### 作为域对象存取值

![image-20191208154333086](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190009724.png)

- API

  - getAttribute(String name)：向ServletContext对象的map取数据

  + setAttribute(String name, Object object)：从ServletContext对象的map中添加数据
  + removeAttribute(String name)：根据name去移除数据

- 案例代码

  >需求：在ServletDemo02中获取servletDemo01中的一个变量的值

  - ServletDemo01

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/demo01")
  public class ServletDemo01 extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          String name = "周杰棍";
          //1.获取ServletContext对象
          ServletContext servletContext = getServletContext();
          //2.往容器ServletContext中存值
          servletContext.setAttribute("name",name);
      }
  }
  ```

  - ServletDemo02

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/demo02")
  public class ServletDemo02 extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 获取那个容器ServletContext
          ServletContext servletContext = getServletContext();
          //2. 从容器ServletContext中获取数据
          String name = (String) servletContext.getAttribute("name");
          System.out.println("在ServletDemo02中获取的name是:" + name);
      }
  }
  ```

  - 发布项目，浏览器跳转到welcome页面，此时我们访问/demo01路径，此时ServletDemo01往容器ServletContext中存值，再访问/demo02路径，可以看到控制台输出：`在ServletDemo02中获取的name是:周杰棍`

  ![image-20220319003022964](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190030021.png)

---

#### 获得文件mime-type

- API：getMimeType(String file)

- 案例代码

  >需求：根据文件名获得文件的mime类型

  - ServletDemo03

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/demo03")
  public class ServletDemo03 extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //根据文件名获得文件的mime类型
          // 1.获得ServletContext
          // 2.调用getMimeType()方法
          String file01 = "a.mp3";
          String file02 = "b.png";
          String mimeType01 = getServletContext().getMimeType(file01);
          String mimeType02 = getServletContext().getMimeType(file02);
          String value = getServletContext().getInitParameter("bkey");
          response.getWriter().print("ServletDemo03...:file01:"+mimeType01+";file02:"+mimeType02+";bkey:"+value+";");
      }
  }
  ```

  - 发布项目，浏览器跳转到welcome页面，此时我们访问/demo03路径，可以看到页面输出：`ServletDemo03...:file01:audio/mpeg;file02:image/png;bkey:null;`

  ![image-20220319005101336](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190051389.png)

---

#### 获得全局初始化参数

- API

  - String getInitParameter(String name)：根据配置文件中的key得到value

- 案例代码

  >需求：通过ServletContext来获得全局的初始化参数

  - web.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
           version="3.1">
      <context-param>
          <param-name>bkey</param-name>
          <param-value>bbb</param-value>
      </context-param>
  </web-app>
  ```

  - ServletDemo04

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/demo04")
  public class ServletDemo04 extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          String value = getServletContext().getInitParameter("bkey");
          System.out.println("value=" + value);
      }
  }
  ```

  - 发布项目，浏览器跳转到welcome页面，此时我们访问/demo04路径，可以看到控制台输出：`value=bbb`

  ![image-20220319010417942](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190104085.png)

---

#### 获取web资源路径

- API

  - String  getRealPath(String path)：根据资源名称得到资源的绝对路径
  - getResourceAsStream(String path)：返回制定路径文件的流

  >注意：filepath直接从项目的根目录开始写

- 案例代码

  >需求：使用ServletContext获取web里面的资源的真实路径

  - ServletDemo05

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  import java.io.InputStream;
  
  /**
   * 使用ServletContext获取web里面的资源文件的真实路径
   * 目标: 使用字节输入流，读取test.jpg这张图片
   * 在web项目中，将文件转换成流，有两种方式
   * 	1.如果文件在resources里面，使用类加载器
   *  2.如果文件在web里面，使用ServletContext
   */
  @WebServlet("/demo05")
  public class ServletDemo05 extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //使用ServletContext可以获取web里面的资源的真实路径
          ServletContext servletContext = getServletContext();
          InputStream is = servletContext.getResourceAsStream("test.jpg");
          System.out.println(is);
      }
  }
  ```

  - 发布项目，浏览器跳转到welcome页面，此时我们访问/demo05路径，可以看到控制台输出：`java.io.ByteArrayInputStream@7ce7f87d`

  ![image-20220319014827939](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190148016.png)

---

### 案例：统计网站被访问的总次数

> 需求：在页面中显示网站被访问的总次数

- 思路分析

  ![count](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190119940.jpg)

- 代码实现

  - CountServlet

  ```java
  package servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/count")
  public class CountServlet extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 获取容器中计数器原本的次数
          ServletContext servletContext = getServletContext();
          Object count = servletContext.getAttribute("count");
          //判断ServletContext中是否有计数器
          if (count == null) {
              //说明当前是第一次访问
              //就往ServletContext中添加一个计数器
              servletContext.setAttribute("count",1);
          }else {
              //说明我不是第一次访问，那么就要对原来的计数器+1，再存进去
              int number = ((int) count) + 1;
              servletContext.setAttribute("count",number);
          }
          //2. 向客户端响应WelCome
          response.getWriter().write("WelCome!!!");
      }
  }
  ```

  - ShowServlet

  ```java
  package com.itheima.servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/show")
  public class ShowServlet extends HttpServlet {
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doGet(request, response);
      }
  
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //从容器中获取计数器的值
          ServletContext servletContext = getServletContext();
          int count = (int) servletContext.getAttribute("count");
          //将count响应给客户端
          response.getWriter().print("access count is:"+count);
      }
  }
  ```

  - 发布项目，浏览器跳转到welcome页面，此时我们访问/count路径五次，然后访问/show路径，可以看到页面输出：`access count is:5`

  ![image-20220319012800377](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190128426.png)

  ![image-20220319012859646](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203190128691.png)

---

