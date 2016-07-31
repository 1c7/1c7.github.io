---
layout: post
title:  "How I feel after switch from PHP to Ruby on Rails (6 month now)"
date:   2016-07-31 10:41:01 +0800
---
##### Estimate reading time: 6 minute  

<br/>

I have been PHP developer for little bit more than a year (2014~2015, December).  
(CodeIgniter, ThinkPHP, pure PHP)  

not really happy period, just feel... ok.    

and then I switch to Ruby on Rails, (2016,January~now) feel much happier now.     
let me tell you why  

<br/>

### 1. Database schema synchronization    

Situation: you work with one other developer, two people in total.  

PHP   

```
[You]:
  1. trying to implement a new feature, you need new field in table

  2. Write SQL or use some tool(SQLyog) to generate SQL: `CREATE TABLE user{ }`

  3. copy & paste into phpMyAdmin, Pass, no SQL syntax error  

  4. copy & paste into a place both people can visit, probably Github Wiki  


[The other guy]:

  1. git pull

  2. error in browser? field close_time not exist? 
    "I think he/she change database schema"

  3. go to Github Wiki, "Yep, he/she changed that."
  	copy & paste SQL code into phpMyAdmin or any other SQL client software  

```

Rails

```Ruby
[You]:

  1. rails g migration add_something_to_some_model / rails g model User
  2. rake db:migrate


[The other guy]:

  1. (in browser) pending migration error?
  2. rake db:migrate
```
done!  


<br/>

### 2. Relation

PHP

```
  Define and remember it at database level
```


Rails

```
  has_one
  has_many
  belongs_to
  has_and_belongs_to_many
```




<br/>

### 3. Deploy  

PHP

```
  1. Open up FTP client like 'FileZilla'

  2. Remember which file you have changed
  
  3. Upload these file and cross finger hope you didn't miss any file 
	or acciently overwrite file that you shouln't overwrite  

  4. No Rollback, You have to manually upload previous version file  
````

Rails

```
  1. git push

  2. mina deploy

  3. things goes wrong?   mina deploy:rollback
```
done!  
You can use Capistrano or [Mina](https://github.com/mina-deploy/mina) to deploy your project, 
I have try both, Mina is better for me  



<br/>
<br/>

### 4. Conclusion
here just my feeling. for me, Rails make me a lot happier,  
the syntax of Ruby, the simplicity of Rails Active Record    

I don't want argue that, Ruby on Rails is 100% better than PHP or what,  
argue that is just like argue what music or food is the best.     
everyone got a favorite.     

but, for me, Rails make me much more productive and make me a much happier web developer  


<br/>
<br/>

### 5. btw (by the way)
My experience is not just Rails and PHP  

I have try a lot of other language and framework:  

    Node.js:     Express    
    Python:      Flask, Django, CherryPy, Bottle.py, Web.py, Tornado     
    PHP:         CodeIgniter, ThinkPHP  


I still think Rails is the best among all of them.  


(I heard about [Koa.js](http://koajs.com/) is awesome but I haven't try it)




#### For PHP developer:  

I heard about a PHP framework call [Laravel](https://laravel.com/) that feel like Rails but I have never try it  
so I am not sure how good it is,   
If you still don't want switch to Rails, maybe you should check that out.


<br/>
<br/>

### 6. My current status (2016, August)

1. Just finish two side project (All by my own, idea, design, code):  
[OneReco](https://www.onereco.com/) and [Sumup](http://www.youtube-sumup.com/)     


2. Side project:   
working with 4 other people on a side project call "FrontSeat"    
(I would put a link here once it we finish beta version)    
(it's a educational project)    



3. Job:    
Looking for Ruby on Rails REMOTE position (I am living in China right now)     




<br/>
<br/>

#### One last thing (Imaging Steve Jobs voice)  
I am not a native english speaker, so if I got grammar error,   
please point out, help me improve. Thanks
