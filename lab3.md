## Lab 3

### 画出销售模块的概念类图

#### 销售处理用例描述

- 销售处理

<table>
    <tr>
        <td>用例项目</td>
        <td>内容描述</td>
    </tr>
    <tr>
        <td>ID</td>
        <td>1</td>
    </tr>
    <tr>
        <td>名称</td>
        <td>销售处理</td>
    </tr>
    <tr>
        <td>参与者</td>
        <td>销售员</td>
    </tr>
    <tr>
        <td>触发条件</td>
        <td>客户携带商品到达销售点</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>销售员必须已经被识别和授权</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>生成并保存销售单；记录系统操作并写⼊系统⽇志</td>
    </tr>
    <tr>
        <td>正常流程</td>
        <td>
            <ol>
                <li>销售员获取客户信息，如关键字或客户编号</li>
                <li>系统显示客户信息</li>
                <li>销售员根据客户选择的商品添加出货商品清单
                    <ol>
                        <li>选择商品名称</li>
                        <li>输入商品数量</li>
                    </ol>
                </li>
                <li>系统显示出货商品清单</li>
                销售员重复 3~4 步，直到完成所有商品的输入
                <li>如果客户使用代金券，销售员向单据中添加代金券信息</li>
                <li>系统根据代金券和折让计算商品总额</li>
                <li>销售员确认销售单信息</li>
                <li>系统生成销售单</li>
                <li>销售单通过审批</li>
                <li>系统更改库存数据和客户的应收应付数据</li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>扩展流程</td>
        <td>客户应收超出应收额度</td>
    </tr>
    <tr>
        <td>特殊需求</td>
        <td></td>
    </tr>
</table>
- 销售退货处理

<table>
    <tr>
        <td>用例项目</td>
        <td>内容描述</td>
    </tr>
    <tr>
        <td>ID</td>
        <td>2</td>
    </tr>
    <tr>
        <td>名称</td>
        <td>销售退货处理</td>
    </tr>
    <tr>
        <td>参与者</td>
        <td>销售员</td>
    </tr>
    <tr>
        <td>触发条件</td>
        <td>客户携带商品到达销售退货点</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>销售员必须已经被识别和授权</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>生成并保存销售退货单；记录系统操作并写⼊系统⽇志</td>
    </tr>
    <tr>
        <td>正常流程</td>
        <td>
            <ol>
                <li>销售员获取客户信息，如关键字或客户编号</li>
                <li>系统显示客户信息</li>
                <li>销售员根据客户选择的商品添加退货商品清单
                    <ol>
                        <li>选择商品名称</li>
                        <li>输入商品数量</li>
                    </ol>
                </li>
                <li>系统显示退货商品清单</li>
                销售员重复 3~4 步，直到完成所有商品的输入
                <li>系统计算商品总额</li>
                <li>销售员确认销售退货单信息</li>
                <li>系统生成销售退货单</li>
                <li>销售退货单通过审批</li>
                <li>系统更改库存数据和客户的应收应付数据</li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>扩展流程</td>
        <td></td>
    </tr>
    <tr>
        <td>特殊需求</td>
        <td></td>
    </tr>
</table>




#### 销售处理概念类图

![销售模块概念类图](lab3.assets\销售模块概念类图.svg)



### 查看经营历程表的系统顺序图

似乎没有 opt 和 loop 组件

![business-process-sequence](lab3.assets/business-process-sequence.svg)





### 单据的状态图

![receipt-state](lab3.assets/receipt-state.svg)



