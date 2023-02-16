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