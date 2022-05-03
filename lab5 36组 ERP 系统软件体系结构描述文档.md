# ERP 系统软件体系结构描述文档

## 0. 小组成员名单及分工

组长：杨昊锦 201250013 ： 负责lab5的接口视角和信息视角的编写

组员：凌毓辰 201250007：负责lab5 的引言、产品概述、逻辑视角和组合视角

​		   丁宇辰 201250012：负责讨论总体思路

​           胡睿     201250026：负责讨论总体思路

## 1. 引言

### 1.1 编制目的

本报告详细完成对 ERP 系统的概要设计，达到指导详细设计和开发的目的，同时实现和测试人员及用户的沟通。本报告面向开发人员、测试人员及最终用户而编写，是了解系统的导航。

### 1.2 词汇表

| 词汇名称 | 词汇含义                 | 备注   |
| -------- | ------------------------ | ------ |
| ERP      | 为公司设计的统筹管理系统 | ...... |
| ......   | ......                   | ...... |

### 1.3 参考资料

1. [南京大学软件工程与计算II课件08-需求文档化与验证 ](http://seec-helper-pdf.oss-cn-hangzhou.aliyuncs.com/slide/288/08-需求文档化与验证.pdf?Expires=1649034561&OSSAccessKeyId=LTAI4Fi1qmL4iuhH8t7G7r2H&Signature=X6zw6oqnEeAcVR56Jz68hrUnQOA%3D)

## 2. 产品概述

本产品是一套为了让规模扩大的民营企业适应新的环境，提高 工作效率和用户满意度而开发的 ERP 系统。该系统主要包括库存管理、销售管理、财务管理、人事管理和企业经营管理。

## 3. 逻辑视角

ERP 系统中，选用了分层体系结构风格，将体系分为3层（展示层、业务逻辑层、数据层）能够很好地示意整个高层抽象。展示层包含 GUI 页面的实现，业务逻辑层包含业务逻辑处理的实现，数据层负责数据的持久化和访问。分层体系结构的逻辑视角和逻辑设计方案如下图所示。

<img src="https://seec-homework.oss-cn-shanghai.aliyuncs.com/参照体系结构风格的包图表达逻辑视角.png" style="zoom: 50%;" />

![软件体系结构逻辑设计方案](https://seec-homework.oss-cn-shanghai.aliyuncs.com/软件体系结构逻辑设计方案.png)

## 4. 组合视角

### 4.1开发包图

ERP 系统的最终开发包设计如下表。

| 开发（物理）包       | 依赖的其他开发包                                             |
| -------------------- | ------------------------------------------------------------ |
| mainui               | promotionui, saleui, commodityui, financeui, customui, purchaseui, employeeui, userui, vo |
| promotionui          | promotionblservice, 界面类库包                               |
| promotionblservice   |                                                              |
| promotionbl          | promotionblservice, promotiondataservice, po                 |
| promotiondataservice | Java RMI, po                                                 |
| promotiondata        | Java RMI, po, databaseutility                                |
| saleui               | saleblservice, 界面类库包                                    |
| saleblservice        |                                                              |
| salebl               | saleblservice, saledataservice, commoditybl, custombl, userbl, promotionbl, po |
| saledataservice      | Java RMI, po                                                 |
| saledata             | Java RMI, po, databaseutility                                |
| commodityui          | commodityblservice, 界面类库包, vo                           |
| commodityblservice   |                                                              |
| commoditybl          | commodityblservice, commoditydataservice, salebl, po         |
| commoditydataservice | Java RMI, po                                                 |
| commoditydata        | Java RMI, po, databaseutility                                |
| financeui            |                                                              |
| financeblservice     |                                                              |
| financebl            | financeblservice, financedataservice, salebl, purchasebl, userbl, custombl, po |
| financedataservice   | Java RMI, po                                                 |
| financedata          | Java RMI, po, databaseutility                                |
| customui             | customblservice, 界面类库包, vo                              |
| customblservice      |                                                              |
| custombl             | customblservice, customdataservice, po                       |
| customdataservice    | Java RMI, po                                                 |
| customdata           | Java RMI, po, databaseutility                                |
| purchaseui           | purchaseblservice, 界面类库包                                |
| purchaseblservice    |                                                              |
| purchasebl           | purchaseblservice, purchasedataservice, custombl, userbl, po |
| purchasedataservice  | Java RMI, po                                                 |
| purchasedata         | Java RMI, po, databaseutility                                |
| employeeui           | employeeblservice, 界面类库包, vo                            |
| employeeblservice    |                                                              |
| employeebl           | employeeblservice, employeedataservice, userbl, po           |
| employeedataservice  | Java RMI, po                                                 |
| employeedata         | Java RMI, po, databaseutility                                |
| userui               | userblservice, 界面类库包, vo                                |
| userblservice        |                                                              |
| userbl               | userblservice, userdataservice, po                           |
| userdataservice      | Java RMI, po                                                 |
| userdata             | Java RMI, po, databaseutility                                |
| vo                   |                                                              |
| po                   |                                                              |
| utilitybl            |                                                              |
| 界面类库包           |                                                              |
| Java RMI             |                                                              |
| databaseutility      | JDBC                                                         |

ERP 系统客户端开发包图和服务器端开发包图如下所示。

<img src="https://seec-homework.oss-cn-shanghai.aliyuncs.com/客户端开发包图.png"  />

<img src="https://seec-homework.oss-cn-shanghai.aliyuncs.com/服务器端开发包图.png"  />

### 4.2 物理部署

ERP 系统中客户端构件是放在客户端机器上，服务器端构建是放在服务器端机器上。在客户端节点上，还要部署 RMIStub 构件。由于 Java RMI 构件属于 JDK 8.0 的一部分，所以在系统 JDK 环境已经设置好的情况下，不需要再独立部署。部署图如下所示。

![部署图](https://seec-homework.oss-cn-shanghai.aliyuncs.com/部署图.png)

## 5. 接口视角

### 5.1 模块职责

客户端模块视图如下

![lab5 客户端模块视图](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5 客户端模块视图.png)

服务器端模块视图如下

![lab5  服务器端模块视图](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5服务器端模块视图.png)

客户端各层职责如下表

|          层          |                            职责                            |
| :------------------: | :--------------------------------------------------------: |
|       启动模块       |            负责初始化网络通信机制，启动用户界面            |
| 用户界面层（展示层） | 基于窗口的连锁商店客户端用户界面，显示各种UI方便使用者操作 |
|      业务逻辑层      |         响应用户界面的输入，并根据业务逻辑处理输入         |
|    客户端网页模块    |                使用 Java RMI机制查找RMI服务                |

服务器端各层职责如下

|       层       |                 职责                 |
| :------------: | :----------------------------------: |
|    启动模块    | 负责初始化网络通信机制，启动用户界面 |
|     数据层     |    负责数据的持久化及数据访问接口    |
| 服务器网络模块 |  使用 Java RMI机制开启并注册RMI服务  |

应注意的是，每层都只通过接口调用直接使用下方接触的层。层与层之间的接口如下表所示

|                             接口                             |    服务调用方    |    服务提供方    |
| :----------------------------------------------------------: | :--------------: | :--------------: |
| PromotionBLService<br />SaleBLService<br />CommodityBLService<br />FinanceBLService<br />CustomBLService<br />PurchaseBLService<br />EmployeeBLService<br />UserBLService |   客户端展示层   | 客户端业务逻辑层 |
| PromotionDataService<br />SaleDataService<br />CommodityDataService<br />FinanceDataService<br />CustomDataService<br />PurchaseDataService<br />EmployeeDataService<br />UserDataService<br />DataFactoryService | 客户端业务逻辑层 |  服务器端数据层  |

下面以销售用例层为例用图说明层与层之间的接口调用

![Lab5 销售用例层之间接口调用图](https://seec-homework.oss-cn-shanghai.aliyuncs.com/Lab5销售用例层之间接口调用图.png)

### 5.2 用户界面层的分解

根据需求，系统存在32个用户界面：登陆界面、财务人员主界面、库存管理人员主界面、销售员主界面、总经理主界面、销售经理主界面、人力资源人员主界面等。界面跳转如下图所示。

![lab5 用户界面跳转](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5用户界面跳转.png)

服务器端和客户端的用户界面设计接口一致，但是具体界面不同。用户界面类如下图所示。

![lab5 用户界面类](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5用户界面类.png)

#### 5.2.1 用户界面层

下表显示了用户界面层模块的接口规范

|   模块    |              职责               |
| :-------: | :-----------------------------: |
| MainFrame | 界面Frame，负责界面的显示和跳转 |

#### 5.2.2 用户界面层的接口规范

用户界面层的接口规范如下表所示

|           |     语法     | init(args:String[])       |
| :-------: | :----------: | ------------------------- |
| MainFrame | **前置条件** | 无                        |
|           | **后置条件** | 显示Frame 以及 LoginPanel |

用户界面层所需要的接口规范如下表

|               服务名                |                 服务                 |
| :---------------------------------: | :----------------------------------: |
| businesslogicservice.LoginBLService |        登陆界面的业务逻辑接口        |
|   businesslogicservice.*BLService   | 每一个界面都有一个对应的业务逻辑接口 |

#### 5.2.3 用户界面模块设计原理

用户界面利用Java的Swing和AWT库实现

### 5.3 业务逻辑层的分解

业务逻辑层包括多个针对界面的业务逻辑处理对象。例如，User对象负责处理登陆页面的业务逻辑；Sales对象负责销售界面的业务逻辑。业务逻辑层的设计如下图所示。

![lab5 业务逻辑层的设计](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5业务逻辑层的设计.png)

#### 5.3.1 业务逻辑层模块的职责

业务逻辑层模块的职责如下表

|  模块   |                职责                |
| :-----: | :--------------------------------: |
| userbl  | 负责实现对应于登陆界面所需要的服务 |
| salesbl |    负责实现销售界面所需要的服务    |
|   ...   |                ...                 |

#### 5.3.2 业务逻辑层模块的接口规范

userbl和salesbl的接口规范分别如下表所示

userbl模块的接口规范

|                                   |   提供的服务（供接口）   |                                                              |
| :-------------------------------: | :----------------------: | ------------------------------------------------------------ |
|                                   |           语法           | public ResultMessage.login(long id, String password)         |
|            User.login             |         前置条件         | password符合输入规则                                         |
|                                   |         后置条件         | 查找是否存在相应的User, 根据输入的password返回登陆验证的结果 |
|                                   | **需要的服务（需接口）** |                                                              |
|              服务名               |           服务           |                                                              |
|  DatabaseFactory.getUserDatabase  | 得到User数据库的服务引用 |                                                              |
| UserDataService.insert(UserPO po) | 向数据库中插入UserPO对象 |                                                              |
|                ...                |           ...            |                                                              |

salesbl模块的接口规范

|                                                 |       提供的服务（供接口）       |                                                           |
| :---------------------------------------------: | :------------------------------: | --------------------------------------------------------- |
|                                                 |               语法               | public ResultMessage addMember(long id)                   |
|                 Sales.addMember                 |             前置条件             | 启动销售流程                                              |
|                                                 |             后置条件             | 在销售流程中增加购物者的会员信息                          |
|                                                 |               语法               | public ResultMessage addCommodity(long id, long quantity) |
|               Sales.addCommodity                |             前置条件             | 启动销售流程                                              |
|                                                 |             后置条件             | 在销售流程中增加购买的商品的信息和数量                    |
|                                                 |               语法               | public ResultMessage addTotal(long id, long quantity)     |
|                 Sales.getTotal                  |             前置条件             | 买家信息和已购商品信息和数量已经被填写                    |
|                                                 |             后置条件             | 返回该次销售的商品总额                                    |
|                                                 |               语法               | public double getChange(double payment)                   |
|                 Sales.getChange                 |             前置条件             | 已经计算出总额                                            |
|                                                 |             后置条件             | 根据商品总额返回找零金额                                  |
|                                                 |               语法               | public void endSales()                                    |
|                 Sales.endSales                  |             前置条件             | 支付完成                                                  |
|                                                 |             后置条件             | 结束该次销售流程，更新涉及的数据                          |
|                                                 |     **需要的服务（需接口）**     |                                                           |
|                     服务名                      |               服务               |                                                           |
|          SalesDataService.find(int id)          |     通过ID查找单一持久化对象     |                                                           |
| SalesDataService.finds(String field, int value) | 通过字段名和值查找多个持久化对象 |                                                           |
|       SalesDataService.insert(SalesPO po)       |        插入单一持久化对象        |                                                           |
|       SalesDataService.delete(SalesPO po)       |        删除单一持久化对象        |                                                           |
|       SalesDataService.update(SalesPO po)       |        更新单一持久化对象        |                                                           |
|        DatabaseFactory.getSalesDatabase         |   得到Sales数据库的服务的引用    |                                                           |
|       SalesDataService.insert(SalesPO po)       |    向数据库中插入SalesPO对象     |                                                           |
|                       ...                       |               ...                |                                                           |

### 5.4 数据层的分解

数据层主要给业务逻辑层提供数据访问服务，包括对于持久化数据的增删查改。Sales业务逻辑需要的服务由SalesDataService接口提供。下图所示是对数据层模块的具体描述

![lab5 数据层模块的描述](https://seec-homework.oss-cn-shanghai.aliyuncs.com/lab5数据层模块的描述.png)

#### 5.4.1 数据层模块的职责

数据层模块的职责如下表所示

|                 模块                 |                             职责                             |
| :----------------------------------: | :----------------------------------------------------------: |
|           SalesDataService           |     持久化数据库的接口，提供集体载入和集体的增删查改操作     |
|     SalesDataServiceTxtFilelmpl      | 基于Txt文件的持久化数据库的接口，提供集体载入和集体的增删查改操作 |
| SalesDataServiceSerializableFilelmpl | 基于序列化文件的持久化数据库的接口，提供集体载入和集体的增删查改操作 |
|      SalesDataServiceMySqllmpl       | 基于MySql数据库的持久化数据库的接口，提供集体载入和集体的增删查改操作 |

#### 5.4.2 数据层模块的接口规范

数据层模块的接口规范如下表所示

|                         | 提供的服务（需接口） |                                                        |
| ----------------------- | -------------------- | ------------------------------------------------------ |
|                         | 语法                 | public SalesPO find(long id) throws RemoteException;   |
| SalesDataService.find   | 前置条件             | 无                                                     |
|                         | 后置条件             | 按照ID查找满足条件的SalesPO结果                        |
|                         | 语法                 | public void insert(SalesPO po) throws RemoteException; |
| SalesDataService.insert | 前置条件             | 在数据库中不存在同样ID的记录                           |
|                         | 后置条件             | 在数据库中增加一个po记录                               |
|                         | 语法                 | public void delete(SalesPO po) throws RemoteException; |
| SalesDataService.delete | 前置条件             | 在数据库中存在同样ID的记录                             |
|                         | 后置条件             | 在数据库中减少一个po记录                               |
|                         | 语法                 | public void update(SalesPO po) throws RemoteException; |
| SalesDataService.update | 前置条件             | 在数据库中存在同样ID的记录                             |
|                         | 后置条件             | 在数据库中更新一个po记录                               |
|                         | 语法                 | public void init(\) throws RemoteException;            |
| SalesDataService.init   | 前置条件             | 无                                                     |
|                         | 后置条件             | 初始化持久化数据库                                     |
|                         | 语法                 | public void finish() throws RemoteException;           |
| SalesDataService.finish | 前置条件             | 数据库已经被init                                       |
|                         | 后置条件             | 结束数据库的使用                                       |

## 6. 信息视角

###  6.1 数据持久化对象

系统的PO类为对应的相关实体类

- UserPO：包含用户的用户名和密码
- CommodityPO：包含商品的编号、价格、数量和名字
- MemberPO：包含会员的编号、生日、姓名、性别、电话、积分
- SalesPO：保存销售时的数据类，包括编号、会员编号、商品列表、总价、折扣、客户支付金额、找零金额、赠品
- SalesLineItemPO：保持销售纪录中一行的信息，包括商品编号、数量、小计
- CommodityGiftPromotionPO：包括商品ID、促销起始日期和终止日期、礼物编号和礼品数量

持久化对象CommodityPO的定义如下

```java
public class CommodityPO implements Serializable {
    int id;
    double price;
    String name;
    int quantity;
    
    public CommodityPO(int i, String n, double p, int q){
        this.id = i;
        this.name = n;
        this.price = p;
        this.quantity = q;
    }
    
    public String getName(){return this.name;}
    public int getID(){return this.id;}
    public int getQuantity(){return this.quantity;}
    public double getPrice(){return this.price;}
}
```

### 6.2 Txt 持久化格式

Txt持久化格式以UserPO.txt为例，每行分别对应用户名和密码，中间以":"分割

张三:123456

李四:234567

### 6.3 数据库表

数据库表中包括User表、Commodity表、Member表、Sales表、SalesLineItem表、CommodityGiftPromotion表、CommodityPricePromotion表、GiftLineItem表。
