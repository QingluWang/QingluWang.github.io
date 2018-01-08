---
layout	:	post
title	:	Intellij开发Spring常见问题
---

### 1.java.lang.ClassNotFoundException: org.springframework.web.context.ContextLoaderListener

原因：依赖问题

解决：右键单击你的项目->Open Module Settings->将缺少的依赖都添加上

### 2.The origin server did not find a current representation for the target resource or is not willing to

原因（部分）：WEB-INF目录受保护，无法访问该目录下页面

解决：将要访问的页面放在其他目录

### 3.java.lang.NoClassDefFoundError: javax/servlet/jsp/jstl/core/Config

原因：WEB-INF/lib目录下缺少jstl.jar和standard.jar

解决：http://archive.apache.org/dist/jakarta/taglibs/standard/binaries/下载jakarta-taglibs-standard-1.1.2.zip这个包，解压缩后将standard和jstl两个包放入lib下即可

### 4.Cannot resolve symbol

原因（部分）：缓存

解决： “File” -> “Invalidate Caches / Restart”，然后 “Invalidate and Restart”