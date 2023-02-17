### function的使用规则

> 在项目中，代码的可读性和可维护性的体现就是function的使用，有效的封装function方法是让你走向成功的必备技能，但在使用function中，什么时候去使用function就显得格外的重要，今天我们就来说一下function的使用场景

#### 场景一：当你需要获取一个变量的值，且这个变量的值需要通过逻辑判断后得出一个结果时

比如： 

```javascript
// 场景一： 
// 如果orderType(订单类型) = 1,则orderStatus(订单名称) = '待支付'
// 如果orderType = 2, 则orderStatus = '已支付'
// 如果orderType = 3, 则orderStatus = '待收货'
// 现在已知 orderType ，那如何写 orderStatus 呢？ 通常情况下我们会这么写：

let orderType = 1;
let orderStatus;

if(orderType == 1){
    orderStatus = '待支付';
}else if(orderType == 2){
    orderStatus = '已支付';
}else if(orderType == 3){
    orderStatus = '待收货'
}
```

观察上面实现的方式，写法是没有问题的，但是如果业务逻辑复杂时，一个页面中会有大量的设置类型于orderStatus这样变量的逻辑，代码的可读性差了起来；为了更高的代码可读性，通常情况下，我们会封装一个方法，变成这样：

```javascript
let orderType = 1;
let orderStatus = getOrderStatus(orderType);

function getOrderStatus(orderType){
    if(orderType == 1){
    	return '待支付';
    }else if(orderType == 2){
        return '已支付';
    }else if(orderType == 3){
        return '待收货'
    }
}

//上面的代码中，封装了一个getOrderStatus方法来实现代码的高可读性；
//注意getOrderStatus这个方法的命名规范；
//get是获取的意思
//order是订单的意思
//status是状态的意思
//getOrderStatus的意思是 获取订单状态
//这样写的话，代码可读性就高了起来；
```

规范说明： 

1. 一个方法通常情况下只能实现一个功能；
2. 如果想通过一些逻辑实现一个值，则该方法通常用get开头，并return一个结果值；
3. 方法的命名应该遵循驼峰命名法；

#### 场景二： 如果一些逻辑实现的功能需要重复调用时，可以封装成function

```javascript
// 场景需求：
// 我需要在进入页面的时候，在控制台分别输出1，2，3，4，5；
// 同时当我点击一个按钮时，也需要在控制台分别输出1,2,3,4,5;

console.log(1);
console.log(2)
console.log(3)
console.log(4)
console.log(5)

document.querySelector("button").onclick = function(){
    console.log(1);
    console.log(2)
    console.log(3)
    console.log(4)
    console.log(5)
}
```

上列方法中，我们会在打开页面的时候，代码在控制台分别出输1，2，3，4，5，并且当我们点击按钮时也会输出1，2，3，4，5；我们为了简化逻辑，就可以封装成function：

```javascript
print();

document.querySelector("button").onclick = function(){
    print();
}

function print(){
    console.log(1);
    console.log(2)
    console.log(3)
    console.log(4)
    console.log(5)
}
```

注：

1. 方法的封装是为了满足复用性，把相同的逻辑封装在一起；

2. 但是需要注意的是，在一个方法中，不要有当前作用域之外的任何变量，比如：

   ```javascript
   let a = 1;
   function fn(){
       console.log(a)// 这样写是不对的； 因为当前作用域中，没有a;
   }
   ```

3. 方法的命名一定要语意化，且一个页面中有且应该只有一个同一维度的的命名，比如：

   ```javascript
   // 错误示范：  用户和人本身指的是一个物体，属于同一个维度； 所以此命名是不规范的；
   
   // 获取用户信息
   function getUserInfo(){}
   // 获取人信息
   function getPersonInfo(){}
   ```

4. 一个方法代表一个行为，是一种动作，所以，如果在你写逻辑时，需要做一件事，且这件事需要复用，就可以封装成一个方法；

5. 基于上一条说明，你可以利用给一个方法增加一个或者多个形参，来实现不同的对象进行不同行为，从而使方法变得更灵活：

   ```javascript
   // 比如有一个应用场景：
   // 想让 不同的人去商品里买不同的商品，我们可以写成：
   
   buy('小明', 'iphone13')  // 小明购买了iphone13
   
   buy('小红', '裙子')  // 小红购买了裙子
   
   function buy(userName, goodsName){
       console.log(userName + '购买了' + goodsName);
   }
   ```

6. 绝大多数的方法中，为了方法的可读性，一个方法的形参数量会小于等于三个；

7. 但在一个三方的api中，一个方法的形参不超过6个；