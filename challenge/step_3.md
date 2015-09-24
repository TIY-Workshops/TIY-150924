# GET data from an API


## Main Concepts

In this section we will get some experience making network calls over HTTP. 

Once again we will see how separating code into classes and functions can help to make the code reusable. 

## Objective

In this section we are going to fetch data from a remote Application Program Interface (API). This will be a network call, very similar to how a browser requests web pages from a server. 

Remember that the main concepts are more important than the specific implementation details.

The remote API we will be using is called Yoda Speak. We will give the service a sentence and it will re-phrase it as if Yoda had said it. 

## Install Gems

In order to achieve this we will need to use some 3rd party libraries. In Ruby, libraries are known as 'gems'. The gems we will need are 'unirest' and 'nokogiri'.

To install these on your computer, type the following in the terminal window:

```
gem install unirest
(console output)
...
...
...
gem install nokogiri
(console output)
...
...
...
```

## A GET request to the YodaSpeak API

Create a file called 'main_yoda_speak.rb' and add the following code:

```ruby
# main_yoda_speak.rb

# We need to use classes and functions from these gems
require 'unirest'
require 'nokogiri'

plain_text = "We should take a holiday"

# all spaces need to be replaced with a plus sign so that we produce a valid URL
input = plain_text.gsub! /\s+/, '+'

# make a hash with the required request headers
request_headers = {}
request_headers["Accept"] = "text/plain" # this requests accepts a response in plain text and not other formats e.g. audio
request_headers["X-Mashape-Key"] = "YK9cMTQ2uJmshG36ASZtzZy3omeDp1ySVaQjsnGEhTDMjWWRkL" # the authentication key

# make a GET request to yodaspeak API
response = Unirest.get("https://yoda.p.mashape.com/yoda?sentence=#{input}", headers: request_headers )

# parsing response from API
# this uses 'xpath' to extract the first paragraph from the response
parsee = Nokogiri::HTML(response.body)
parser = parsee.xpath('//*/body/p').first

# display the content
yoda_text = parser.content

puts yoda_text

```

## Move the logic into a class

In the same folder, create a file call `yoda_speak.rb` and add the following to it:

```ruby
# yoda_speak.rb

# We need to use classes and functions from these gems
require 'unirest'
require 'nokogiri'

class YodaSpeak
	def translate(plain_text)
		# all spaces need to be replaced with a plus sign so that we produce a valid URL
		input = plain_text.gsub! /\s+/, '+'

		# make a hash with the required request headers
		request_headers = {}
		request_headers["Accept"] = "text/plain" # this requests accepts a response in plain text and not other formats e.g. audio
		request_headers["X-Mashape-Key"] = "YK9cMTQ2uJmshG36ASZtzZy3omeDp1ySVaQjsnGEhTDMjWWRkL" # the authentication key

		# make a GET request to yodaspeak API
		response = Unirest.get("https://yoda.p.mashape.com/yoda?sentence=#{input}", headers: request_headers )

		# parsing response from API
		# this uses 'xpath' to extract the first paragraph from the response
		parsee = Nokogiri::HTML(response.body)
		parser = parsee.xpath('//*/body/p').first

		# return the content
		parser.content
	end
end

```

We can change `main_yoda_speak.rb` to use this new class

```ruby
# main_yoda_speak.rb

require_relative 'yoda_speak'

yoda_speak = YodaSpeak.new

plain_text = "We should take a holiday"

yoda_text = yoda_speak.translate plain_text 

puts yoda_text

```

Please make sure that this works before moving on...

#### References and Credits
* https://www.mashape.com/ismaelc/yoda-speak
* https://gist.github.com/travismgordon/c1d63a7c4dc71ebe9ce3
