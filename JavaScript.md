
### ES6 编码规范

1. 基本数据类型 number string boolean null undefined
2. 引用 object function array
3. 对象方法简写，对象属性值简写
4. 数组用 push 添加，用 ... 复制，用 Array.from 转换类数组对象成数组
5. 对象解构
    ```
      function getFullName ({firstname, lastname}) {
        return `${firstname} ${lastname}`
      }
      const person = {
        firstname: "tony",
        lastname: "sr",
        age: 34
      }
      getFullName(person)
    ```

6. 数组解构  ``` const [a, b] = [1,2,3,4] ```
7. 使用字符串模板
8. 用 ..args 代替 arguments  因为arguments是一个类数组
9. 函数参数指定默认值
10. 在函数 **作为参数** 传递时使用箭头函数
11. 使用Class 和 extend 构造器
12. 每行变量声明都要有const和let，并且要把两种不同的声明方式分组
13. 对象、函数、实例用驼峰命名， 类和构造函数用帕斯卡， 私有变量用下划线开头

### JavaScript设计模式和开发实践

1. JavaScript是 一门动态类型语言，动态类型语言中实现面向接口设计原则。 例如，只要一个对象有push和pop的方法，就可以当做栈来使用 （鸭子模型）
2. 一段能体现多态性的代码：

  ```
    var makeSound = function (animal) {
      if (animal instanceof Duke) {
        console.log("嘎嘎嘎");
      } else if (animal instanceof Chicken) {
        console.log("咯咯咯");
      }
    };

    var Duke = function () {}
    var Chicken = function () {}

    makeSound( new Duke() );
    makeSound( new Chicken );
  ```

  虽能提现多态性，但是并不能建立在对象之上。面向对象是将变与不变分开，变化的是叫声，不变的叫的动作。

  把不变的部分隔离，将可能改变的部分封装，程序才会有良好的可扩展能力。

  修改后的代码：

  ```
    var makeSound = function (animal) {
      animal.sound();
    }

    var Duke = function () {}
    Duke.prototype.sound = function () {
      console.log('嘎嘎嘎');
    }

    var Chicken = function () {}
    Chicken.prototype.sound = function () {
      console.log("咯咯咯");
    }

    makeSound(new Duke);
    makeSound(new Chicken);
  ```

3. JavaScript本身就具有多态的性质。静态类型语言中，继承是实现多态的条件。
4. 书中的23种设计模式可以分为： 创建型，结构型，行为型

   创建型模式的目的就是封装创建对象的变化。而结构型模式封装的是对象之间的组合关系。 行为型模式封装的是对象的行为变化。

5. 原型编程泛型：

   * 所有的数据都是对象
   * 要得到一个对象，不是实例化一个类，而是找一个对象作为原型并克隆它
   * 对象会记住他的原型
   * 如果对象无法响应某个请求，会委托给自己的原型

6. JavaScript中任何对象的创建都是克隆某一个对象，把此对象作为原型，比如

   `var a = {}`

   此对象的原型就是Object.prototype，而要更改克隆对象也就是要更改原型，可用 *__proto__* 属性  

   `a.__prooto__ = Array.prototype`

7. this指向分为4种：

   * 作为对象的 **方法**    this指向此对象
   * 作为普通 **函数**      this指向全局
   * 构造器                this指向new运算符出来的对象
   * Function.prototype.call 和 Function.prototype.apply调用

8. 模拟Function.prototype.bind

   ```
    Function.prototype.bind = function (context) {
      // context为Function对象的作用域this
      var self = this;
      return function () {
        return this.apply(context, arguments);
      }
    }
   ```

9. [].slice.call 或 [].shift.call 函数都是想在 arguments对象上调用数组方法，所以才这么写（arguments不是数组）
10. 函数节流。某些情况下函数会被非常频繁的调用，造成性能问题，比如下面场景：

    * window.onresize
    * mousemove
    * 上传进度

  代码实现：

  ```
    var throttle = function (fn, interval) {

      var _self = fn,           // 保存需要延迟执行的函数引用
          timer,                // 定时器
          firstTime = true;     // 是否第一次调用

      return function () {
        var args = arguments,
            _me = this;

        if (firstTime) {   // 第一次调用不需要延迟
          _self.apply(_me, args);
          return firstTime = false;
        }

        if (timer) {      // 定时器存在说明上一次调用未执行完
          return false;
        }

        timer = setTimeout(function () {
          clearTimeout(timer);
          timer = null;
          _self.apply(_me, args);
        }, interval || 500);
      }
    }
  ```

11. 分时函数。 在短时间进行大量操作会导致浏览器卡死，比如同时创建1000个节点。

    1秒创建1000个节点可以改为200毫秒创建8个节点，代码实现：

    ```
      var timeChunk = function (ary, fn, count) {
        var obj, t;

        var len = ary.length;
        var start = function () {
          for (var i = 0; i < Math.min(count || 1, ary.length); i++) {
            var obj = ary.shift();
            fn(obj);
          }
        };

        return function () {
          t = setInterval(function () {
            if (ary.length === 0) {
              return clearInterval(t);
            }
            start();
          }, 200);
        }
      }
    ```

12. 单例模式： 保证一个类仅有一个实例，并提供一个访问他的全局访问点
13. 策略模式： 定义一系列的算法，把它们一个个封装起来，并且使它们可以相互替换。
14. 代理模式： 为一个对象提供一个代用品或占位符，以便控制对它的访问。前端常用 虚拟代理和缓存代理，其他还有防火墙代理、远程代理、保护代理等
15. 迭代器模式： 提供一种方法顺序访问一个聚合对象中的各个元素，而又不需要暴露该对象的内部表示
16. 观察者模式： 它定义对象间的一种一对多的依赖关系，当一个对象的状 态发生改变时，所有依赖于它的对象都将得到通知
