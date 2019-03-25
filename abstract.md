# Abstract

---

随着互联网技术的不断发展迭代，整体的软件设计架构一直在更迭，慢慢的从原本单一的软件架构逐渐开始进行了功能区块的分离，如今流行的微服务应用就是基于这种分离思想诞生的，为了提高代码整体的容错率与拓展性。而分离思想的典型代表就是基于前后端分离的项目。何谓前后端分离，宏观上来讲就是前端人员和后端人员负责的功能模块进行代码的分离，从原本冗余在一份里的代码拆成两份完全独立的代码。微观上来讲就是将前端界面的逻辑和数据库的处理拆成两份独立的代码进行管理，让前端只专注于界面层的逻辑，而后端只专注于数据层的逻辑。<br>
为了研究前后端分离的思想，后台管控系统项目以前后端分离的形式进行软件架构设计，前端使用目前较为流行的单页面响应式前端架构 Vue，而后端使用比较成熟的后端服务器框架 ThinkPHP5，而中间件采用目前较为流行的 Nginx 进行反向代理服务。

---

With the deployment of the Internet technology, it's changing all the time in the software architecture. Gradually, Thought of separation have approached to the scene view of coder. The software architecture from gather mode to separation mode. Now, the popular microservices that was familier with us was born in the separation for increasing error-tolerant rate and extensibility. The program of separating between front-end and back-end was the classic.
From the micro, the program was separated from one code to two code. These code was separated in function distinction. From the macro, the program was separated to GUI Layer and Data Layer. Let the front coder was focus on GUI and the other was focus on data handler. <br>
The Background Admin System was designed to be the Separation. The System's front-end was coded in Vue framwork with the feature of SPA and Responsive. The System's back-end was codd in TP5 framwork. This is a mature framwork. The Middleware of Nginx was selected in the System which is popular at persent.
