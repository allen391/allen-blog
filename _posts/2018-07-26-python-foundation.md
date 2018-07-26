---
layout:     post
title:      Python Foundation(Object)(ZH)
subtitle:   Python Foundation 对象
date:       2018-07-26
author:     Allen
catalog: true
tags:
    - Python Foundation
    - Object
---

大纲
类的构造方法
类的访问权限
继承
多态
项目实践
作业
1. 类的构造方法

链接：类

#### 调用时间：在对象被实例化时被程序自动调用
#### 作用：用于对象创建时初始化
#### 书写格式：init前后分别是两个下划线
#### 程序不显示定义init方法，则程序默认调用一个无参init方法
#### 对象创建过程
类

实例1： ``` class Dog: def init(self): print("我是构造方法，在创建对象时自动调用")

self.gender = gender
self.variety = variety
self.name = name
self.__age = age
# 获取对象属性，并打印出来
def get_pro(self):
    print("gender:{},variety:{},name:{},age:{}".format(self.gender,self.variety,self.name,self.__age))
#设置对象内部属性
def set_pro(self,**kwargs):
    if "gender" in kwargs:
        self.gender = kwargs["gender"]
    elif "age" in kwargs:
        if kwargs["age"] < 0 or kwargs["age"]>20:
            print("非法年龄")
        else:
            self.__age = kwargs["age"]

def eat(self):
    print("正在吃骨头...")

def drink(self):
    print("正在喝水....")
wangcai = Dog() wangcai.eat() wangcai.drink()

wangcai就是就是类所创建的实例对象
结果：
我是构造方法，在创建对象时自动调用 正在吃骨头... 正在喝水....

从结果可以看出，在创建对象的时候，init的方法会自动调用

- #### __init__构造方法
##### 1. 设置对象属性
##### 2. 创建对象过程

![创建对象过程](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/A05261BCD77447929EE010EF5AC1E3EE/2615)

<font color = red>实例2：</font>
class Dog:

通过init的构建方法来设置对象属性
def __init__(self,gender,variety,name,age):
    #print("我是构造方法，在创建对象时自动调用")
    self.gender = gender
    self.variety = variety
    self.name = name
    self.age = age
wangcai = Dog('man','golden','wangcai','20') print(wangcai.gender) print(wangcai.variety) print(wangcai.name) print(wangcai.age) ``` 结果：

man
golden
wangcai
20
2. 类的访问权限

2.1 修改对象属性的方法

##### 方法1：对象变量名.属性 = 新值
##### 方法1的问题：
可能修改的属性值不合法
在类的外部可以随意修改类的内部属性

方法2：对象变量名.内部修改属性方法

实例3：

class Dog:
    def __init__(self,gender,variety,name,age):
        #print("我是构造方法，在创建对象时自动调用")
        self.gender = gender
        self.variety = variety
        self.name = name
        self.age = age
        
        

wangcai = Dog('man','golden','wangcai','20')

#修改对象属性，方法1直接修改
wangcai.age = 100
print(wangcai.age)
结果： 100

实例4： ``` class Dog: def init(self,gender,variety,name,age): #print("我是构造方法，在创建对象时自动调用") self.gender = gender self.variety = variety self.name = name self.age = age def getpro(self): print("gender:{},variety:{},name:{},age:{}".format(self.gender,self.variety,self.name,self.age)) #设置对象内部属性 def setpro(self,**kwargs): if "gender" in kwargs: self.gender = kwargs["gender"] elif "age" in kwargs: if kwargs["age"] < 0 or kwargs["age"]>20: print("非法年龄") else: self.age = kwargs["age"]

wangcai = Dog("male","golden","wangcai",1)

方法2：通过内部方法修改属性
wangcai.setpro(age=10) wangcai.getpro()

这种方法还是可以直接从外部直接修改属性，不够安全，所以引入私有属性概念
结果：
gender:male,variety:golden,name:wangcai,age:10


#### 2.2 私有属性
- ##### 定义：__私有变量名
- ##### 只能在类内部使用，类外部不能访问，否则报错

<font color = red> 实例5：</font>
将age变为私有属性
class Dog: def init(self,gender,variety,name,age): #print("我是构造方法，在创建对象时自动调用") self.gender = gender self.variety = variety self.name = name self.age = age def get_pro(self): print("gender:{},variety:{},name:{},age:{}".format(self.gender,self.variety,self.name,self.age)) #设置对象内部属性 def setpro(self,**kwargs): if "gender" in kwargs: self.gender = kwargs["gender"] elif "age" in kwargs: if kwargs["age"] < 0 or kwargs["age"]>20: print("非法年龄") else: self._age = kwargs["age"]

wangcai = Dog('man','golden','wangcai',20) wangcai.get_pro()

如果defpro和def setpro中的age不加双下划线，则会报错出不存在age这个属性

结果：
gender:man,variety:golden,name:wangcai,age:20


#### 2.3 私有方法
- ##### 只有在类内部调用，在类的外部无法调用
- ##### 定义私有方法在方法名前添加两个下划线
- ##### 类内部调用私有方法要使用self.私有方法的方式调用

<font color = red >实例6：</font>
私有方法的使用
class Comrade: #私有方法 def _sendmessage(self): print("消息已经向上级汇报")

def answer_secret(self,secret):
    if secret == "芝麻开门":
        print("接头成功!")
        self.__send_message()#调用私有方法
    else:
        print("接头失败！")
comrade = Comrade() comrade.answer_secret("芝麻开门") ``` 结果：

接头成功!
消息已经向上级汇报
3. 继承

#### 在程序中，继承描述的是类中类型与子类型之间的所属关系，例如猫和狗都属于动物
#### 单继承 ##### 1. 子类继承一个父类，在定义子类时，小括号()中写父类的类名 ##### 2. 父类的非私有属性、方法，会被子类继承 ##### 3. 子类中方法的查找方式：先查找子类中对应的方法，如果找不到，再到父类中查找 ##### 4. 子类可以继承父类的属性和方法，也可以继承父类的非私有属性和方法，依次类推 ##### 5. 在子类中调用父类的方法：ClassName.methodname(self)
实例7：

class Animal:
    def __init__ (self):
        print("---animal构造方法----")
    
    def __private_method(self):
        print('私有方法')
    def eat(self):
        print('-----吃-----')
    def drink(self):
        print('-----喝-----')
    def run(self):
        print('-----跑-----')

class Dog(Animal):
    def __init__(self):
        print('dog构造方法')
        
    def hand(self):
    ##子类在类里面调用父类的方法
        Animal.run(self)
        print('----握手-----')

wangcai =Dog()
#调用从父类继承的方法
wangcai.eat()
wangcai.drink()
wangcai.run()
#调用自身的方法
wangcai.hand()

#调用父类的私有方法，会被报错，不能继承父类的私有方法
# wangcai.__private_method


#如果在子类中没有定义init构造方法，则自动调用父类的init构造方法，如果在子类中定义了init构造方法，则不会调用父类的构造方法
duoduo = Dog()
duoduo.run()
结果：

dog构造方法
-----吃-----
-----喝-----
-----跑-----
-----跑-----
----握手-----
dog构造方法
-----跑-----
#### 重写父类方法 ##### 1. 子类对父类允许访问的方法的实现过程进行重新编写 ##### 2. 在子类中定义与父类同名的方法 ##### 3. 优点：子类可以根据需要，定义合适的方法实现逻辑
实例8： ``` class Animal: def init (self): print("---animal构造方法----")

def __private_method(self):
    print('私有方法')
def eat(self):
    print('-----吃-----')
def drink(self):
    print('-----喝-----')
def run(self):
    print('-----跑-----')
class Dog(Animal): #父类方法重写 #只要够名称覆盖掉父类的方法就可以实现重写 def run(self): print('摇着尾巴跑') def hand(self): print('----握手-----') wangcai =Dog() wangcai.run()

结果：
---animal构造方法---- 摇着尾巴跑

- #### 多继承
##### 1. object 类是所有类的基类，在定义类的时候不需要显示的在括号中表明继承自object类
##### 2. 多继承：一个子类可以继承多个父类
##### 3. 多继承定义方式：在类名后的括号中添加需要继承的多个类名
##### 4. 多继承中，如果多个类中有同名的方法，子类调用查找方法的顺序是按照小括号内继承父类从左到右的顺序查找，第一个匹配方法名的父类方法将会被调用

<font color = red >实例9：</font>
多继承中方法的名称尽量不一样，要不然会出现不必要的错误和困扰，比如下面的data_handle
class AI: #人脸识别 def facerecongnition(self): print("人脸识别") def datahandle(self): print("AI数据处理")

class BigData: def dataanalysis(self): print("数据分析") def datahandle(self): print("BigData数据处理")

class Python(BigData,AI): def operation(self): print("自动化运维")

py = Python() py.facerecongnition() py.dataanalysis() py.operation() py.datahandle() print(Python.mro) #查看调用方法的搜索顺序 结果： 人脸识别 数据分析 自动化运维 BigData数据处理 (<class 'main.Python'>, <class 'main.BigData'>, <class 'main_.AI'>, ) ``` - #### 多态

一个抽象类有多个子类，不同的类表现出多种形态

实例10： ```

子类的的方法是会覆盖掉父类的方法，只有存在继承，才能存在多态
class Animal: def eat(self): print("Animal正在吃饭")

class Dog(Animal): def eat(self): print("Dog正在吃饭")

class Cat(Animal): def eat(self): print("Cat正在吃饭")

def show_eat(obj): obj.eat()

wangcai = Dog() showeat(wangcai) tom = Cat() showeat(tom) 结果： Dog正在吃饭 Cat正在吃饭

## 4.项目实践
### 无人便利店
- 用户管理系统
- 仓库管理系统
- 货架管理系统
- 升级购物车
- 推荐系统

<font color = red >实例11：</font>
import datetime import csv ''' 用户管理系统 仓库管理系统 货架管理系统 升级购物车 推荐系统 '''

class WarehouseManageSys:

"""
仓库管理系统
"""
def __init__(self):
    #商品清单
    self.item_detail = {"老坛酸菜":5, "红烧牛肉":4, "酸辣粉":6, "拉面":7,"老干妈":10, "乌江":2,"王中王":2, "蒜肠":12, "淀粉肠":8}
'''
功能：根据商品类型返回商品列表
参数说明：
    item_type:商品类型
'''
def get_item_list(self,item_type):  #为什么这里要输入item_type
# 泡面
    pm_list = ["老坛酸菜", "红烧牛肉", "酸辣粉", "拉面"]
# 榨菜
    zc_list = ["老干妈", "乌江"]
# 香肠
    xc_list = ["王中王", "蒜肠", "淀粉肠"]
    if item_type == "pm":
        return pm_list
    elif item_type == "zc":
        return zc_list
    elif item_type == "xc":
        return xc_list

'''
功能：添加或者更新商品价格
参数说明：
    kwargs：商品名称和价格的键值对，可以传入多个
'''
def add_update_item_info(self,**kwargs):  #利用不定长参数
    for item,price in kwargs.items():
        self.item_detail['item'] = price
货架管理系统
class RackManageSys: ''' 功能：检测货架上的商品是否需要补货 参数说明： rack：货架列表 itemtpye:商品类型 itemcounts:货架可摆放的商品数量 warehousemanage:仓库管理系统的对象 ''' def checkaddrack(self,rack, itemtype, itemcounts,warehousemanage): if len(rack) == 0: print("---正在更新货架，请稍等---") #根据商品类型从仓库中获取商品列表 itemlist = warehousemanage.getitemlist(itemtype) while len(rack) < itemcounts: rackindex = len(rack) % len(itemlist) rack.append(itemlist[rackindex]) print("----商品已上架----")

日志管理系统
class LogMangerSys: def init(self): self.buylogs = [] ''' 功能：获取写日志的当前时间 参数： format：日期格式化方式，如："%Y%m%d" ''' def getlogtime(self, format): logtime = datetime.datetime.now().strftime(format) return log_time

'''
功能：将日志追加到csv文件持久化存储
参数：
file_path：文件路径
file_name：文件名称
header：文件标题
data：日志数据，[{key:value}]
'''
def write_log_append_csv(self, file_path, file_name, header, data):
    # 写日志时间
    log_time = self.get_log_time("%Y%m%d")
    print("log_time:{}".format(log_time))
    # 文件格式：file_path + file_name+log_time
    # 输出的csv文件名称
    new_file_name = file_path + file_name + "_" + log_time + ".csv"
    with open(new_file_name, "a", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, header)
        # writer.writeheader()
        writer.writerows(data)

'''
功能：用户购买日志写入到日志文件
参数说明：
    user_id：用户编号
    money：消费金额
    items：购买商品列表，格式:[{"user_id":"user_id1","money":20,"items":(item1,itme2....)}]
'''
def buy_log_manage(self,user_id, money, *items):
    buy_log = {"user_id": user_id, "money": money, "items": items}
    self.buy_logs.append(buy_log)
    # ------------v4 start------------------#
    item_str = ""  # 格式：老干妈|王中王
    for item in items:
        if item_str == "":
            item_str = item
        else:
            item_str += "|" + item

    file_path = "d://"
    file_name = "user_buy_log"
    header = ["user_id", "money", "items"]
    buy_log = [{"user_id": user_id, "money": money, "items": item_str}]
    #调用自身将日志数据写入到CSV文件的方法
    self.write_log_append_csv(file_path, file_name, header, buy_log)
用户管理系统
class UserManageSys: def init(self): self.useridset = set() ''' 功能：添加新用户 参数说明： userid：用户编号 ''' def addnewuser(self,userid): if userid not in self.useridset: self.useridset.add(userid) ''' 功能：验证用户是否是VIP 参数说明： userid：用户编号 ''' def ifvip(self,userid): if userid in self.useridset: return True else: return False

购物车
class BuyCar: def init(self,userid,usermanage): self.userid = userid #验证用户是否是VIP self.ifvip = usermanage.ifvip(self.userid) #初始化一个购物车的车筐 self.buycar = [] ''' 功能：向购物车添加商品 参数说明： pmrack：泡面货架 zcrack：榨菜货架 xcrack：香肠货架 itemid：商品编号 ''' def additem2car(self,pmrack,zcrack,xcrack,itemid): if int(itemid) == 1: if len(pmrack) >= 1: self.buycar.append(pmrack[len(pmrack) - 1]) pmrack.pop() else: print("亲！非常抱歉，泡面已卖完。") elif int(itemid) == 2: if len(zcrack) >= 1: self.buycar.append(zcrack[len(zcrack) - 1]) zcrack.pop() else: print("亲！非常抱歉，榨菜已卖完。") elif int(itemid) == 3: if len(xcrack) >= 1: self.buycar.append(xcrack[len(xcrack) - 1]) xcrack.pop() else: print("亲！非常抱歉，香肠已卖完。") else: print("亲！您输入的商品还在火星，请输入在售的商品编号！")

'''
功能：购物车结算
参数说明：
    warehouse_manage：仓库管理系统对象，用于获取商品价格清单
'''
def account(self,warehouse_manage):
    total_money = 0
    for item in self.buy_car:
        total_money += warehouse_manage.item_detail.get(item, 0)
    if self.if_vip:
        vip_money = total_money * 0.9
        total_money = float("%.2f" % vip_money)
    return total_money
推荐系统父类
class RecommendSys: def recommend(self): print("推荐商品")

基于物品的推荐系统
class BaseItemRecommendSys(RecommendSys): def recommend(self,userid,buylogs): useritemset = set() #被推荐人历史购买商品 otheruseritemdict = {} # 其他用户历史购买商品 {"userid":{item1,item2}} for log in buylogs: useridkey = log["userid"] itemsvalue = log["items"] if useridkey == userid: useritemset.update(itemsvalue) else: itemsset = otheruseritemdict.get(useridkey) if itemsset == None: otheruseritemdict[useridkey] = set(itemsvalue) else: itemsset.update(itemsvalue) otheruseritemdict[useridkey] = itemsset

    recommend_list = []  # 被推荐列表
    for value_set in other_user_item_dict.values():
        inner_set = user_item_set & value_set
        length = len(inner_set)
        if length > 0 and length < len(value_set):
            diff_set = value_set - user_item_set
            recommend_list.append({"common_num": length, "items": diff_set})
    if len(recommend_list) > 0:
        recommend_list.sort(key=lambda x: x["common_num"], reverse=True)
        recommend_set = recommend_list[0]["items"]
        return list(recommend_set)  # 集合转列表
class UnstaffedStore: # 购物大厅 def shoppinghall(self): #仓库管理系统初始化 warehousemanage = WarehouseManageSys() #货架管理系统初始化 rackmanage = RackManageSys() #用户管理系统初始化 usermanage = UserManageSys() #日志管理系统初始化 logmanage = LogMangerSys() #推荐系统初始化 recommendsys = BaseItemRecommendSys()

    # 三个空货架
    pm_rack = []
    zc_rack = []
    xc_rack = []
    # 货架摆放商品数量
    pm_rack_counts = 1
    zc_rack_counts = 1
    xc_rack_counts = 1

    while True:
        print("欢迎光临")
        user_id = ""
        while True:
            user_id = input("请输入手机号作为用户id使用：")
            if user_id != "":
                user_manage.add_new_user(user_id)
                break
            else:
                print("输入的手机号不能为空，请输入正确的手机号！")
        #给用户分配一个购物车
        buy_car = BuyCar(user_id,user_manage)

        while True:
            # 自动检测货架是否需要补货
            rack_manage.check_add_rack(pm_rack, "pm", pm_rack_counts,warehouse_manage)
            rack_manage.check_add_rack(zc_rack, "zc", zc_rack_counts,warehouse_manage)
            rack_manage.check_add_rack(xc_rack, "xc", xc_rack_counts,warehouse_manage)
            item_id = input("==本店售卖商品：1 泡面，2 榨菜，3 香肠。请输入想要购买的商品编号：")
            #向购物车添加商品
            buy_car.add_item_2_car(pm_rack,zc_rack,xc_rack,item_id)
            if_buy = input("请输入y或者n选择是否继续购物：")
            if if_buy == "n":
                #购物车结算
                if len(buy_car.buy_car) > 0:
                    total_money = buy_car.account(warehouse_manage)
                    print("您的购物车商品如下：", buy_car.buy_car)
                    print("$您本次消费金额{}元：".format(total_money))
                    # 购物日志管理
                    log_manage.buy_log_manage(user_id, total_money, *buy_car.buy_car)
                    recommend_item_list = recommend_sys.recommend(user_id,log_manage.buy_logs)
                    if recommend_item_list != None:
                        print("买了该商品的其他用户，还买了{}".format(recommend_item_list))
                    print("欢迎下次光临")
                else:
                    print("您没有购买任何商品")
                    print("欢迎下次光临")
                break
store = UnstaffedStore() store.shopping_hall() 
```
