title: MyBatis 源码解读（零）导语
author: Kenny Tang
date: 2019-07-12 14:49:14
tags:
---
简单介绍下我使用最多的持久层框架 `Hibernate` `valuelist` `MyBatis` 这三个框架，也是用过国内的一些产品，不过已经很少了。
 
虽然已经使用了很长时间，但是还没有认真的读过该项目的源码，不读一下总感觉有点遗憾，为此写出了该系列的博文，能力有限，不足或纰漏之处希望读者指正。

以下是对我常用的持久层框架的简单对比，不喜欢的可以忽略以下内容

## Hibernate
` Hibernate` 是我最早使用，曾经也是我十分热爱的框架 ：
<!-- more -->

首先说这个框架的主旨思想是要从开发人员的思维中把表这一概念隐去，只保留对象的概念。到现在我还一直认为这是一个非常先进的理念，这样有一个非常明显的好处，就是可以让开发人员更专注于业务，不考虑与数据库交互的过程。

但是就是她的思想太先进了，实际上到目前为止，与数据的交互一直是一个瓶颈，无论怎么做都不能实现几乎无延迟的数据检索与写入，` Hibernate`要做到好用就必须与数据产生大量的交互，截止到现在我们在数据存储和检索方面还做不到接近于无感知，而且可以断定在将来相当长的一段时间内也不太可能做得到。

要解决这一问题就必须使用手写SQL 一旦使用手写SQL，这就已经不是 ` Hibernate`的优势了，` Hibernate` 手写SQL时还是相当的繁琐的，而且不方便修改，这对开发人员来说是很不友好的事情。
## MyBatis
　　我使用最多， 也是目前为止我最喜欢的一个框架，原因就是他实用，方便快捷。使用`MyBatis`时通常我们需要定义一个Mapper 每一个Mapper对应一个相应的 xml 文件，由框架处理 JAVA 代码与 XML 文件之间的联系，这样激活就可以实现JAVA代码和SQL开发的独立执行，调试SQL再也看不见烦人的 “” 和字符串拼接了。

下面是一个Mapper的示例文件
 ```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.pos.mapper.PosMapper" >
	<select id="findByAgentNo" resultType="com.pos.entity.Agent">
		select
        a.id id,
        a.agent_no agentNo,
        a.short_name shortName,
        a.full_name fullName,
        a.sales sales,
        a.status status,
        sale.staff_no ,
        sale.staff_name ,
        a.role_type roleType,
        a.create_time createTime
    from user a
         left join staff sale on a.sales = sale.staff_no
    where a.agent_no = #{agentNo}
	</select>
</mapper>	
   ```
   从以上的代码中可以看出，除了标签之外，几乎完整的保留了一个完整的SQL格式，可以直接在SQL编辑器中进行调试SQL,十分方便。
## valuelist
　`valuelist` ，这个框架可能对很多人来说比较陌生，不做过多介绍了，简单和 `MyBatis`对比一下
||MyBatis|valuelist|
|--|--|--|
|SQL编写|简单，可在SQL编辑器中直接使用|简单，可在SQL编辑器中直接使用|
|SQL调用|简单，对应的命名空间即为对应的JAVA类，通过正常的工具即可进行大量的代码提示不需要硬性记忆|麻烦，调用时必须明确的知道自己调用的SQLkey值是多少，这个是不能通过开发工具进行提示的|
|数据库记录与对象的映射|框架完成，非常方便快捷|需要自己进行手工适配|
|分页操作|不提供默认分页功能，需要自己书写相关代码或者使用插件|默认带有分页功能，分页比较方便|
|SQL查找方便程度|方便，通常我们的文件名称与对应的类名一致，文件为xml格式，通过命名空间进行隔离| 从JAVA查找SQL方便，在合理规范名称下，可方便查找对应的文件中的SQL；在逆向进行查找的时候很不方便，不能很快的锁定调用关系|
通过对比可以发现只有在需要分页时`valuelist` 稍微占优，但是`MyBatis`的生态中已经存在很好使用分页插件，引入后只需要简单的几行代码便可实现一个非常优秀的分页功能。我使用的是 PageHelper，你可以在[Github](https://pagehelper.github.io) 获取相关信息引入项目使用。