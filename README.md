# Otp-Qr

Simple wrapper for implement otp (one time password) and create QR codes for use e.g with google authenticator.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'otp-qr'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install otp-qr

## Usage

Create a otp.rb file in initializers folder and put this
```ruby
ActsAsOTPable.configure do |config|
  config.issuer       = 'your issuer name'
  config.size         = '150x150'
  config.margin       = 0
end
```
In your user model add ``include ActsAsOTPable``
```ruby
class User < ActiveRecord::Base
  include ActsAsOTPable
  
end
```
then from your controller you can access to the following methods
```ruby
class HomeController < ApplicationController

  def index
    user = User.first
    user.otp_generate_secret => "oouj2cjbkivwzft7"
    code = user.otp_current_code => 123456
    user.otp_valid_code?(code) => true
    user.otp_valid_code?(123456) => false
    user.otp_qr_code => "https://chart.googleapis.com/chart?cht=qr&chl=otpauth%3A%2F%2Ftotp%2FPatricio%2520Jofre%3Aemail%40email.com%3Fsecret%3Doouj2cjbkivwzft7%26issuer%3DPatricio%2BJofre&chs=150x150&chld=L%7C0"
  end
end
```
## Using Google Authenticator

Scan the QR code generated by ``otp_qr_code`` method and receive random codes every 30 seconds
<br><br>
<img src="https://raw.githubusercontent.com/patriciojofre/otp-qr/master/docs/qr.png" align="left"> 
<img src="https://raw.githubusercontent.com/patriciojofre/otp-qr/master/docs/google-authenticator.png" align="left" height="550" width="350">

