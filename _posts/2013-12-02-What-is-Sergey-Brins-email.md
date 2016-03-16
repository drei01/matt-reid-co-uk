---
layout: post
title: What is Sergey Brins' email?
---

I recently read a
[couple](http://jordan-wright.github.io/blog/2013/10/14/automated-social-engineering-recon-using-rapportive/)
of
[blog](http://nathanleclaire.com/blog/2013/11/23/how-i-automated-finding-almost-anyones-email-address/)
posts on using socially engineering to get the emails to top players in
big organisations. This enables you to send a cold email to the people
with the power inside an organisation and hopefully get a sale for you
product.








I set about writing a nodejs implementation of this tool and here is the
result. The [source code is available
here](https://github.com/drei01/node-rapportive)










First we authenticate with the rapportive api (used by their chrome
extension). Next we query the api with a generated list of possible
emails to see which ones come back with the most info.













    var request = require('request'),
        randomstring = require("randomstring"),
        colors = require('colors'),
        templates = require('./email-list.js').templates,
        args = process.argv.slice(2);

    if (args.length < 3 || args.length > 3) {
        console.log('Usage node rapportive.js firstname lastname domain.com');
        return;
    }

    var randomEmail = randomstring.generate(7) + [email protected]/*  */',
        firstName = args[0].toLowerCase(),
        lastName = args[1].toLowerCase(),
        domain = args[2];

    request('https://rapportive.com/login_status?user_email=' + randomEmail, function (error, response, body) {
        if (!error && response.statusCode === 200) {
            var sessionToken = JSON.parse(body).session_token;
            
            for (key in templates){
                var targetEmail = templates[key].replace(/{fn}/g, firstName).replace(/{ln}/g, lastName) + '@' + domain;
                
                request({
                    url : 'https://profiles.rapportive.com/contacts/email/' + targetEmail,
                    headers : {'X-Session-Token' : sessionToken}
                }, function (error, response, body) {
                    var contact = JSON.parse(body).contact;
                    
                    if (contact.first_name.length === 0 && contact.last_name.length === 0) {
                        console.log(contact.email.red);
                    } else {
                        console.log(contact.email.green);
                            
                        return;//found someone rapportive knows about
                    }
                });
            }
        }
    });

 









