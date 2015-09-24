# POST to an API

## Main Concepts

In this section we will get further experience making network calls over HTTP. 

We continue with the theme of separating code into classes and functions. 

## Objective

In step 3 we fetched data from an API using a GET request. In this section we are going to send data to an API using a POST request. The API will be using is the Skinder API.

This is the same web application we have been using in the browser to send messages. Now we will write an a Ruby application that will send this information via the API. 


## A POST request to the Skinder API

To achieve this create a new file called `main_skinder.rb` and add the following code:

```ruby
# main_skinder.rb

require 'unirest'

body_text = "This was posted from ruby"
user = "Bob"
email = "bob@gmail.com"

event_code = <-- enter the actual event code here

post_url = "http://skinder.herokuapp.com/events/#{event_code}/messages"

response = Unirest.post post_url, 
                        headers:{ "Accept" => "application/json" }, 
                        parameters:{ :message => { :body => body_text, :username => user, :email => email } }


puts response.code # Status code
# puts response.headers # Response headers
# puts response.body # Parsed body
# puts response.raw_body # Unparsed body
```

After you run this code you should see the message appear within your web browser.

## Move the logic into a class

Create a file called `skinder.rb` and add the following:

```ruby
# skinder.rb

class Skinder
  def post(event_code, message, username, email)
    
      post_url = "http://skinder.herokuapp.com/events/#{event_code}/messages"
    
      response = Unirest.post post_url, 
                        headers:{ "Accept" => "application/json" }, 
                        parameters:{ :message => { :body => message, :username => username, :email => email } }
                        
      return response
  end
end

```

Now we can use this class in `main_skinder.rb`:

```ruby
# main_skinder.rb

require_relative 'skinder'

skinder = Skinder.new

event_code = <-- enter the actual event code here
message = "This is a message"
user = "Bob"
email = ""

response = skinder.post(event_code, message, user, email)

puts response.code # Status code

```

Please make sure this is working before moving onto the final challenge...
