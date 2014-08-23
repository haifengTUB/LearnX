## Express 资源汇总

### Express 相关教程和资料
- [Express 官网](http://expressjs.com/)
- [阮一峰出品: 《Express框架》](http://javascript.ruanyifeng.com/nodejs/express.html)
- [一起学node.js之使用 Express + MongoDB 搭建多人博客N-blog](https://github.com/nswbmw/N-blog/wiki/_pages)
- [一起学node.js之使用 Express + Socket.IO 搭建的多人聊天室N-chat](https://github.com/nswbmw/N-chat/wiki/_pages)
- [nodejs实战案例（Express框架+mongoDB）](https://github.com/tangguangyao/know)
- [在Express项目中使用Handlebars模板引擎](http://xvfeng.me/posts/Using-Handlebarsjs-with-Expressjs/)
- [(譯)深入理解Express.js](http://xvfeng.me/posts/understanding-expressjs/)
- [Express 入门](http://jinlong.github.io/blog/2014/01/07/introduction-to-express/)
- [《THE DEAD-SIMPLE STEP-BY-STEP GUIDE FOR FRONT-END DEVELOPERS TO GETTING UP AND RUNNING WITH NODE.JS, EXPRESS, JADE, AND MONGODB》](http://cwbuecheler.com/web/tutorials/2013/node-express-mongo/) or [On Github](https://github.com/cwbuecheler/node-tutorial-for-frontend-devs)
- [《CREATING A SIMPLE RESTFUL WEB APP WITH NODE.JS, EXPRESS, AND MONGODB》](http://cwbuecheler.com/web/tutorials/2014/restful-web-app-node-express-mongodb/) or [On Github](https://github.com/cwbuecheler/node-tutorial-2-restful-app)
- [《Write a todo list with Express and MongoDB》](http://dreamerslab.com/blog/en/write-a-todo-list-with-express-and-mongodb/) or [On Github](https://github.com/dreamerslab/express-todo-example/)
- [《Todo App with Express.js/Node.js and MongoDB》](http://webapplog.com/todo-app-with-express-jsnode-js-and-mongodb/)
- TBD

### Express 模板引擎
- [express-hbs](https://github.com/barc/express-hbs)
  - [express-hbs简介](http://ekoneko.github.io/node/express-hbs/)
  - [Handlebars templates with Express 3](http://derpturkey.com/handlebars-templates-with-express-3/)
  - TBD
- [Jade](http://jade-lang.com/)
  - [Jade语法文档例子](http://jade-syntax.coffee-js.org/)
  - [Making use of utility libraries in server-side Jade templates](https://coderwall.com/p/egh53a)
    <pre><code>
    app.locals.moment = require('moment');  
    span.created-at= moment(product.createdAt).format('DD.MM.YYYY')
    </code></pre>
  - [How do I display todays date in nodejs jade](http://stackoverflow.com/questions/12419396/how-do-i-display-todays-date-in-nodejs-jade)

    Question:  
    > I am new to node.js and jade and I have tried to use #{Date.now()} and its giving me numbers. How do I display the date in mm/dd/yy format? 

    Answer:
    > You can use moment.js  
	First, add moment to your express application locals  
	express = require('express');  
	...  
	app = express();  
	app.locals.moment = require('moment');  
	Then you can use moment within a jade template like this:  
	p #{moment(Date.now()).format('MM/DD/YYYY')}  
	Moment takes Date.now() by default, so yo can also write:  
	p #{moment().format('MM/DD/YYYY')}
  - TBD
- TBD

### Express 书籍