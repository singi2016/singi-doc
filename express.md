#[express](http://expressjs.com/)

##1 生成[express](http://expressjs.com/en/starter/generator.html)项目，并按照自己开发需要整理

##2 安装[supervisor](https://www.npmjs.com/package/supervisor),便于express开发
 ```cmd
 npm install supervisor -g
 ```
 ```cmd
 supervisor ./bin/www  //启动express,每次有改动会自动重启服务
 ```
 