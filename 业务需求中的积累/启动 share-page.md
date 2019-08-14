### 前端如何启动 share-page
1. git clone xxx
2. npm install（npm i -g nodemon）
3. cd app
4. npm install
5. cd ..
6. vi dev.json（文件内容和 pre.json 保持一致，端口改为 80）
7. sodu vi /etc/hosts 将 127.0.0.1 映射为 xxx.gotokeep.com
8. 启动两个终端，根目录和 /app 都为 npm run dev
9. 打开浏览器，输入 xxx.gotokeep.com 即可启动
