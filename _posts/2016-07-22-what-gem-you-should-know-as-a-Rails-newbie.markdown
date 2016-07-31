---
layout: post
title:  "What gem you should know as a Rails newbie"
date:   2016-07-22 19:33:43 +0800
---
##### Estimate reading time: 2 minute, 21 second, 220 milliseconds  

<br/>

### Target reader: People who just finish Rails 101 tutorial.  
by 101, I mean general introduction tutorial, probably the offcial Rails guide, or video on Youtube.  
maybe some Blog.    

<br/>
<br/>

Well, now you want learn more,     
You may be thinking, what gem are people using?     
here's a list of gem I think you should know.  


<br/>

### Database
SQLite is for Small website,  
if you want grow bigger than that,  
you need MySQL or PostgreSQL or some other DB (maybe MongoDB or RethinkDB?)

for MySQL you should use gem [mysql2](https://rubygems.org/gems/mysql2)    
for PostgreSQL you should use gem [pg](https://rubygems.org/gems/pg/)  

<br/>

### Deploy
Mina (Recommend)   
Capistrano 3    

it's 2016, if possible, don't use FTP software like FileZilla to deploy.  
you will get tried very soon.  
try to automate everything, that's the beauty of computer right?     
  

<br/>


### Server  
Unicorn  
Thin  
Passanger  
Puma (I am using this, and it's Rails 5 default Server)  


<br/>


### Upload image/file 
CarrierWare  
PaperClip (I am using this)  
Refile  



<br/>

### Login

[Devise]   
	Speed up making your own login, like email & password, username & password


[Omniauth]    
	Third party login, like Facebook Twitter Github Google Linkedin


<br/>


### Test
Rspec


<!-- <br/>

### Pagination

Kaminari 
will_paginate  -->









 