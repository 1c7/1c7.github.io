---
layout: post
title:  "Ajax image upload view paperclip"
date:   2016-07-17 19:33:43 +0800
categories: rails paperclip
---


I was trying to create a API for Ajax Image Upload,  
Search about it on Google,   
Article about Ajax image upload is either from 2011~2013 or not working or seem over complex.
I poke around little bit, and come with a simple solution  


Here is my soluation: Rails + Paperclip + Ajax  upload image file

note: image in this example are store in paperclip default location.  now Amazon AWS.  

let's create a example rails project first.  

[Create rails project]
```
rails new ajaximg --skip-bundle
```

[Install Paperclip gem]
do as officer guid says:https://github.com/thoughtbot/paperclip

add following line to gemfile
`
gem "paperclip", "~> 5.0.0" 
`
and then `bundle install`

or `gem install paperclip`

[]





rails g model Image

class Image < ActiveRecord::Base
  has_attached_file :image, styles: { medium: "300x300>", thumb: "100x100>" }, default_url: "/images/:style/missing.png"
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\Z/
end


rails g migration addAttachmentToImage

go to
db/migrate/20160721100726_add_attachment_to_image.rb

class AddAttachmentToImage < ActiveRecord::Migration
  def up
    add_attachment :images, :image
  end

  def down
    remove_attachment :images, :image
  end
end



bundle exec rake db:migrate



routes

	# for view
  get '/image' => 'test#image'	

  # for ajax
  put 'api/image_upload' => 'api#image_upload', as: :api_image_upload




Rails.application.routes.draw do

  get '/image' => 'test#image'
  put 'api/image_upload' => 'api#image_upload', as: :image_upload

end







rails g controller test image

rails g controller api image_upload



view
	test/image.html.erb

```
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


controller
	api#image_upload

`
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
`

let's try if this work

rails s -b 0.0.0.0 -p 5000

-b mean you can visit this outside vmware..
-p mean port 5000
s mean server

![image]()
![image]()
![image]()






let's preview file





<%= file_field_tag :image %>
<img id='preview' src="#">




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
	}).done(function(result){

		console.log(result.image_url);
		$('#preview').attr('src', result.image_url);

	});
})

</script>






if you need validate:


    image = Image.new(img_params)
    image.user_id = current_user.id
    if image.save
      render :json => {:status => 'success',:image_url => image.image.url}
    else
      render :json => {:status => 'fail',   :info => image.errors.full_messages}
    end


and you may want change model as well


class Image < ActiveRecord::Base

  has_attached_file :image, styles: { medium: "160x160>", thumb: "60x60>" }
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\Z/
  
  validates_attachment :image, :presence => true,
    :size => { :in => 0..2048.kilobytes }
end










( I haven't put Disqus in this blog yet, so sorry about you can't comment )
( If this post really save your time, just send me a email: chengzheng.apply@gmail.com
"hey man you solution work, awesome!" that...make me feel little better :D )