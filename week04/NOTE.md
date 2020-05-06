# 第四周小结

##### 事件循环

* 事件循环不属于JavaScript引擎实现的东西，而是由浏览器或node js宿主环境实现的

##### 宏任务与微任务

* setTimeout会产生宏任务
* 每个宏任务里有一个微任务列表，列表里的所有微任务执行完才会执行下一个宏任务
* Promise的then方法以及async函数里的await会将一个微任务入队，微任务列表里的微任务按入队顺序执行

##### 代码示例

```javascript
async function afoo(){
    console.log("1");
    await new Promise(resolve => resolve());
    console.log("2");
}

new Promise(resolve => (console.log("3"), resolve()))
    .then(()=>(
        console.log("4"), 
        new Promise(resolve => resolve())
            .then(() => console.log("5")) ));

setTimeout(function(){
    console.log("6");
    new Promise(resolve => resolve()) .then(console.log("7"));
}, 0);
console.log("8");
console.log("9");
afoo();

// 3
// 8
// 9
// 1
// 4
// 2
// 5
// 6
// 7
```

解析：
* 第一个宏任务：
    * 3
        * 入队 4
    * 8
    * 9
    * 1
        * 入队 2
    * 4
        * 入队 5
    * 2
    * 5
* 第二个宏任务：
    * 6
        * 入队 7
    * 7

##### 与ECMAScript相关的章节
* RunJobs（P.104）
    
#### 个人感悟
前端基础进阶正是围绕这条线索慢慢展开，而事件循环机制(Event Loop)，则是这条线索的最关键的知识点。但是在我学习的过程中，找到的许多国内博客文章对于它的讲解浅尝辄止，不得其法，很多文章在图中画个圈就表示循环了，看了之后也没感觉明白了多少。

winter老师的讲解很透彻，需要重复过几遍，只有搞懂了原理，才能真正把握精髓，体会学习的乐趣。
