---
title: Chat Room System Design 
date: 2017-12-19 16:21:09
categories: CMU Course Project
tags:
	- Project
	- Web Application
	- Socket
---

## Background
This is a course project of 18652-Foundation Of Software Engineering in Carnegie Mellon University Silicon Valley Campus. It aims to build a web application using some specific techniques including JavaScript, Node.js, express.js and so on.

## Scenerio
Implement a simple web version of Chat Room, including functions:

1. Regist and Login.
2. Post messages in chat room.
3. See other users' chat messages.
4. Leave the chat room.
5. Reload history messages when a user re-enters the chat room.

## Architecture
After figuring out the scenerio, it is easy to figure out an initial system architecture diagram.

![system_architecture_diagram_1](/images/Chat_Room/20171219_Chatroom_System_Design_1.png)

In the diagram, the users are divided into two pools: Online pool and Offline pool. The Webserver will build long connection with each online user and inform them with new messages posted by other users immediately. Correspondingly, online users can post messages to the Webserver which will be seen by others.

But which pool will a user belong to? 

![system_architecture_diagram_2](/images/Chat_Room/20171219_Chatroom_System_Design_2.png)

An offline user will become an online user by **signing in** and will return to offline status by **leaving**. **Leaving** means turning off the browser or signing out. Once a new user have registered successful, this user will automaticly login and become an online user.

## Flow Chart

### Login 

![Chatroom_System_Flowchart_Login](/images/Chat_Room/20171225_Chatroom_System_Flowchart_Login.png)

### Regist

![Chatroom_System_Flowchart_Regist](/images/Chat_Room/20171230_Chatroom_System_Flowchart_Regist.png)

### Post

![Chatroom_System_Flowchart_Post](/images/Chat_Room/20171230_Chatroom_System_Flowchart_Post.png)

### Logout

![Chatroom_System_Flowchart_Logout](/images/Chat_Room/20171230_Chatroom_System_Flowchart_Logout.png)

## Technique
	Webserver: express.js
	Database: Mysql
	Frontend: Bootstrap
	Socket: socket.io

There may exist plenty of choices. But in this case, we use these lightweight tools to implement it to meet the requirements of course.

## Extensibility

### Growth of Users
If we have a good fortune, millions of users love and join our Online Chat Room, the rapid growth of users will make our server under pressure. 

Let's say there are 1 million registered users and at most 30% of them (300,000) will be online concurrently. In average, at most 20% of online users (60,000) will post in one second.

On this occation, many problems will occur:

1. One webserver could not keep 300,000 connections and process such great amounts of queries. 
2. The Mysql server will have a high load and refuse most of queries.
3. The messages will have a long time latency and even be able to be lost. 

#### 1. Connections
We need more servers to provide connections. Assume each server could establish 500 connections, then we will need 300000/500 = **600** servers. 

When we try to inform the users with new posts, we must know which users should be sent and where the connections are. So it is necessary to store the status  of connections like this: 

User| Instance | UpdateTime
:-------:|:----------:|:-----:
Sam | 100.ChatRoom.bj | 2017-12-20 13:26:00
Peter | 200.ChatRoom.ca | 2017-12-20 14:26:00
Maria | 300.ChatRoom.pa | 2017-12-20 16:30:00

> Instance is named by ${instanceId}.${product}.${idc} 

Now, we know who we should inform and where to find them as long as this table is constantly updating.

#### 2. Storage
At least 60,000 write queries per second to the storage and obviously Mysql can not handle it. 


#### 3. Messages


### Multiple Rooms

With the growth of users, they would have many other requirements. One of them will be Multiple Room, after all we can not have all of users intermixed in one room.

Then, it is necessary to allow users to establish and enter different rooms as they wish.
