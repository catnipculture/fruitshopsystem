> #### 作者主页：[舒克日记](https://blog.csdn.net/cativen)
>
>  简介：Java领域优质创作者、Java项目、学习资料、技术互助
>
> <b><font color=red>文中获取源码</font></b>

# 项目介绍

系统分为用户、管理员两个角色

​

主要适用于实体店的线上销售，打造线上线下一体化的销售模式，带动蔬菜的销售量，提高店铺的销售额。

前台主要是登录注册、首页展示、分类搜索、购物车、地址信息、个人信息、订单信息等功能模块；

后台主要实现对数据库的管理，实现管理员对注册用户信息的增删改查，以及对网站首页的蔬菜促销信息更新等功能。

# 环境要求

1.运行环境：最好是java jdk1.8,我们在这个平台上运行的。其他版本理论上也可以。

2.IDE环境：IDEA,Eclipse,Myeclipse都可以。推荐IDEA;

3.tomcat环境：Tomcat7.x,8.X,9.x版本均可

4.硬件环境：windows7/8/10 4G内存以上；或者Mac OS;

5.是否Maven项目：是；查看源码目录中是否包含pom.xml;若包含，则为maven项目，否则为非maven.项目

6.数据库：MySql5.7/8.0等版本均可；

# 技术栈

运行环境：java8+mysql8

服务端技术：java+mysql+bootstrap+jquery+mybatis+springboot

# 使用说明

1.使用Navicat或者其它工具，在mysql中创建对应sq文件名称的数据库，并导入项目的sql文件；

2.使用IDEA/Eclipse/MyEclipse导入项目，修改配置，运行项目；

3.将项目中config-propertiesi配置文件中的数据库配置改为自己的配置，然后运行；

# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq

源码地址：[http://www.codegym.top](http://www.codegym.top/)


# 运行截图

## 文档截图

前台

![image20241201155138644](https://i-blog.csdnimg.cn/img_convert/bc365ef59e5c3e8fbd2184c4c14394b5.png)

![image20241201154951787](https://i-blog.csdnimg.cn/img_convert/f4177b4cc890d26b10b57250bb5148ec.png)

![image20241201155014871](https://i-blog.csdnimg.cn/img_convert/d0319e7ea4e5dd5c068d277f924a32b3.png)

![image20241201155038819](https://i-blog.csdnimg.cn/img_convert/a6fccde73f909c6df1dadccf5023db37.png)

![image20241201155055869](https://i-blog.csdnimg.cn/img_convert/1e2ba358e8be8ec06f6b8705b1df66da.png)

![image20241201155105739](https://i-blog.csdnimg.cn/img_convert/d8c0a4cba3cd9274e57e327c2f57d9c9.png)

![image20241201155120627](https://i-blog.csdnimg.cn/img_convert/3b61a13eff55b1bdba59bd5ffc3069c6.png)

后台

![image20241201155152920](https://i-blog.csdnimg.cn/img_convert/ea60d955f9338dbd8cec9749d762b974.png)

![image20241201155230495](https://i-blog.csdnimg.cn/img_convert/690281ed1b182e586d19c308c33237ed.png)

![image20241201155239923](https://i-blog.csdnimg.cn/img_convert/bece5b4de369ced14b7ac31e4ef7d541.png)

![image20241201155250010](https://i-blog.csdnimg.cn/img_convert/fbefb69826c018a058b5006652baa2c4.png)

![image20241201155258675](https://i-blog.csdnimg.cn/img_convert/dbba8f856b7a0256b51ebf40a42c7ca0.png)

### 代码

```
      String externalTenantId = data.getJSONObject("orgInfo").getString("orgId");
        TenantMappingDTO tenantMappingDTO = tenantMappingService.getTenantMapping(externalTenantId, BUSINESS_TYPE_CLIFE);
        //绑定用户与租户的关系
        if (tenantMappingDTO == null) {
            log.warn("未找到对应的租户信息，无法创建用户, externalTenantId={}", externalTenantId);
        } else {
            String prefix = String.valueOf(IdWorker.getId());
            // 创建tingsBoard用户
            UserDO userDO = new UserDO();
            userDO.setTenantId(tenantMappingDTO.getTenantId());
            userDO.setTelephone(telephone);
            String tbUserId = tenantServiceGateway.createUser(userDO, UserConstant.DEFAULT_PASSWORD , prefix, false, tenantMappingDTO.getTenantId());
            String email = prefix + "@quanqiutiao.com";
            customerDTO.setTenantId(tenantMappingDTO.getTenantId());
            SingleResponse<String> save = customerService.save(customerDTO);
            String customerId = save.getData();
            // 创建用户与租户之间的绑定关系
            bindCustomerTenant(customerId, tenantMappingDTO.getTenantId(), email, tbUserId);
        }
```
