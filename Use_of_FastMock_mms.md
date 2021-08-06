# [FastMock](https://www.fastmock.site/#/)使用🍦

> [B站学习网址在此](https://www.bilibili.com/video/BV15B4y1M7nQ?from=search&seid=13738859397349790945)
>
> 在前端开发中，没有接口数据的话，通常会推荐使用Mock。但我今天下午跟着[这篇文章](https://www.jianshu.com/p/f3adb1aab09e)操作半天，大佬是真大佬，我菜也是真的菜…………除了一步步CV+CV+CV 报错后再CV去百度 再CV+CV……我打数据结构OJ加起来可能都没今天下午CV的次数多，关键是，CV之后还是啥也不会啥也看不懂。
>
> 幸好去了趟B站，刷了几个视频后，其中一个视频推荐了[fastmock](https://www.fastmock.site/#/)这个网站，很好用是真的好用，但视频看起来不直观，下面把步骤整理一下🍣
>
> 后期应该有补充，现在发现的确能调用接口就行哈哈哈哈哈~

## 👆🏻添加项目

项目名称 和 项目描述 自己喜欢就好，后期用不到。

接口基础路径：==/api==   🍨

## ✌🏻新增接口

先点击 新增接口button

从右边出来了好多东西：

- 蓝色的里面：

  - 接口名：自己喜欢就好
  - 类型：get  🍰
  - 返回延时：不填，空着
  - url：==/test==  🌈这个要好好填 起个自己能记得的名字，下面代码要用到
  - 接口描述：自己开心就好
  - Mock状态：开

- 黑色的里面：

  代码如下

  ```json
  {
    "code":0,
    "data":{
      "username":"@cname",
      "age|10-30":20,
      "email":"@email",
      "token":"12345"
    }
  }
  ```

  具体解释如下

  ```json
  {
    "code":0,
    "data":{
      "username":"@cname",
      "age|10-30":20,//从10-30当中随机一个数字
      "email":"@email",
      "token":"12345"//一直都是12345
    }
  }
  ```

  输入的是JSON数据，但不能带注释🍿

  整套还是基于[Mock.js](http://mockjs.com/)官网的，其他接口的需要再去[这个网站](http://mockjs.com/examples.html)去调用

## 👌🏻上号! VScode

保存后，页面上有“接口根地址”，复制下来🍙

要记得 [新增接口蓝色里面的url](#✌🏻新增接口)🍛

```html
<script>
import axios from 'axios'

export default {
  mounted(){
    const baseUrl='https://www.fastmock.site/mock/24d31b30752a6298b929a0902b1fa56c/api';
      //刚刚复制的接口根地址
    axios.get(`${baseUrl}/test`)//这里的baseUrl和上一行的const起名保持一致
      							//   /test是新增接口蓝色里面的url
      .then(({data}) => {
        console.log('data',data);
      })
  }
}
</script>
```

页面跑出来是下面的结果

```
data 	code: 0
		data:
			age: 15
			email: "q.mdzvc@lhyercwxg.hk"
			token: "12345"
			username: "金敏"
```

再加一句：npm run dev报错的话，就搞npm run serve

可能是下午装一堆东西的时候改了参数。。。
