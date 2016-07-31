---
layout: post
title:  "[Ruby on Rails 4 + Paperclip gem]: Ajax image upload"
date:   2016-07-17 19:33:43 +0800
---
##### Estimate reading time: 6 minute  

<br/>


## 0. why
I was trying to create __Ajax Image Upload API__ for My Rails application,  
So I search on Google,   
These article:

  1. 80% from 2011~2013
  2. not working
  3. over complex.  

I poke around little bit, and come with a simple solution  
Here is my solution




<br/>


## 0.5 Preview final result:  
![page](/images/post1/5.png)
![page](/images/post1/6.png)
![page](/images/post1/7.png)
![page](/images/post1/8.png)
![page](/images/post1/9.png)
![page](/images/post1/10.png)
![page](/images/post1/11.png)





<br/>
<br/>

## Well, let's do this step by step  


<br/>


## 1. Create a Rails project  
`ruby 
rails new img --skip-bundle
`

<br/>

## 2. Install Paperclip gem: 
[following instruction come from offcial guide](https://github.com/thoughtbot/paperclip)

add following line to gemfile    

`ruby
gem "paperclip", "~> 5.0.0" 
`

and then   
`bundle install`

or   
`gem install paperclip`


<br/>

## 3. Create model for Image and necessary migration

run   

`ruby
rails g model Image
`

copy & paste following code into `app/models/image.rb`  

```ruby
class Image < ActiveRecord::Base
  has_attached_file :image, styles: { medium: "300x300>", thumb: "100x100>" }
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\Z/
end
```

`rails g migration addAttachmentToImage`

inside `db/migrate/20160721100726_add_attachment_to_image.rb` file

```ruby
class AddAttachmentToImage < ActiveRecord::Migration
  def up
    add_attachment :images, :image
  end

  def down
    remove_attachment :images, :image
  end
end
```

and finally  

`
bundle exec rake db:migrate
`

<br/>


## 4. Routes

config/routes.rb  

```ruby
Rails.application.routes.draw do

  # for view
  get '/image' => 'test#image'

  # for ajax
  put 'api/image_upload' => 'api#image_upload', as: :image_upload

end
```

`rails g controller test image`

`rails g controller api image_upload`



<br/>

## 5. View

put following content into: `app/views/test/image.html.erb`

```javascript
<%= file_field_tag :image %>


<script type="text/javascript">

$('#image').change(function(){

  var formData = new FormData(),
    $input = $(this);
    
	formData.append('image[image]', $input[0].files[0]);

	$.ajax({
	  url: '<%= image_upload_path %>',
	  data: formData,
	  cache: false,
	  contentType: false,
	  processData: false,
	  type: 'PUT'
	});
})

</script>
```


<br/>


## 6. Controller

in file: `app/controller/api_controller.rb`


```ruby
class ApiController < ApplicationController
	
  def image_upload
    @image = Image.create(img_params)

    if @image
      render :json => {:status => 'success',:image_url => @image.image.url}
    else
      render :json => {:status => 'fail'}
    end

  end


  private
  def img_params
      params.require(:image).permit(:image)
  end

end
```


<br/>


## 7. Experiment Time!



`ruby
rails s -b 0.0.0.0 -p 5000      
`

s mean server      
-b mean you can visit this outside vmware  
-p mean port 5000  


<br/>


### 7.1 First 
`http://192.168.1.139:5000/image`  
your address is different from mine, don't forget change it   
![page](/images/post1/1.png)

### 7.2 Let's Choose a file

![page](/images/post1/2.png)


### 7.3 It work!

![page](/images/post1/3.png)


### 7.4 Image work!

![page](/images/post1/4.png)





<br/>
<br/>

## Done! over.
but we can push little further

<br/>

### Let's preview file




```javascript
<%= file_field_tag :image %>
<img id='preview' src="#">   <!-- new code here-->


<script type="text/javascript">

$('#image').change(function(){

	var formData = new FormData(),
    $input = $(this);
    
	formData.append('image[image]', $input[0].files[0]);

	$.ajax({
	  url: '<%= image_upload_path %>',
	  data: formData,
	  cache: false,
	  contentType: false,
	  processData: false,
	  type: 'PUT'
	}).done(function(result){  <!-- new code here-->

		console.log(result.image_url);    <!-- new code here-->
		$('#preview').attr('src', result.image_url); <!-- new code here-->

	}); <!-- new code here-->

})

</script>
```


<br/>


### if you need validate:


Model  

```ruby 
class Image < ActiveRecord::Base

  has_attached_file :image, styles: { medium: "160x160>", thumb: "60x60>" }
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\Z/
  
  validates_attachment :image, :presence => true,
    :size => { :in => 0..2048.kilobytes }
end
```

Controller  

```ruby
class ApiController < ApplicationController
  
  def image_upload

    image = Image.new(img_params)

    if image.save
      render :json => {:status => 'success',:image_url => image.image.url}
    else
      render :json => {:status => 'fail',   :info => image.errors.full_messages}
    end

  end


  private
  def img_params
      params.require(:image).permit(:image)
  end

end
```

<br/>
<br/>

----  

<br/>

## Conclusion   

### Most important part is     

view:  

```javascript

<%= file_field_tag :image %>
<img id='preview' src="#">   <!-- new code here-->


<script type="text/javascript">

$('#image').change(function(){

  var formData = new FormData(),
    $input = $(this);
    
  formData.append('image[image]', $input[0].files[0]);

  $.ajax({
    url: '<%= image_upload_path %>',
    data: formData,
    cache: false,
    contentType: false,
    processData: false,
    type: 'PUT'
  }).done(function(result){  <!-- new code here-->

    console.log(result.image_url);    <!-- new code here-->
    $('#preview').attr('src', result.image_url); <!-- new code here-->

  }); <!-- new code here-->

})

</script>
```

controller:  

```ruby
class ApiController < ApplicationController
  
  def image_upload

    image = Image.new(img_params)

    if image.save
      render :json => {:status => 'success',:image_url => image.image.url}
    else
      render :json => {:status => 'fail',   :info => image.errors.full_messages}
    end

  end


  private
  def img_params
      params.require(:image).permit(:image)
  end

end
```


<br/>
<br/>
<br/>
