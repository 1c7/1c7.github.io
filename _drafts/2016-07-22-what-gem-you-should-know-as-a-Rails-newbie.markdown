---
layout: post
title:  "What gem you should know as a Rails newbie"
date:   2016-07-22 19:33:43 +0800
---
Estimate reading time: 5 minute  

### Target reader: People who just finish Rails 101 tutorial.  
by 101, I mean general introduction tutorial, probably the offcial Rails guide, or video on Youtube.  
maybe some Blog.    


Well, now you want learn more,     
You may be thinking, in real world production enviroment, what gem are people use?     
here's a list of gem I think you should know.  




### Database
sqlite is for small website,  
if you want grow bigger than that,  
you need MySQL or PostgreSQL or some other DB(maybe MongoDB or RethingDB?)

for MySQL you should use gem `mysql2`
for PostgreSQL you should use gem 'pg'


### Deploy
really? you want open up a FTP software like FileZilla to upload your code to server?  
like PHP developer?  
it's 2016! the age of auto deploy!    

Mina(Recommend)
Cap3



### Server  
Well, 
Unicorn
Thin
Passanger
Puma(I am using this)

### File, Image upload
CarrierWare
PaperClip (I am using this)
Refile



### Login

Devise speed up for making your own login, like email&password, username@password
Omniauth for third party login, like facebook twitter github google linkedin



### Test
Rspec


### Pagination
Kaminari 
 will_paginate 









 