---
layout: post
title:  "Detection Surface Series: 1) Loggable to Detectable"
author: Balazs Greksza
date:   2024-01-31 01:00:00 +0200
categories: detectionengineering, logging, appdev
permalink: /blog/:title/
tags: detectionengineering logging, appdev
---

The basic activity diagram of security logging is as follows:
![logging_activity_diagram]({{urlimg}}/assets/img/logging_activity_diagram.jpg)
Note that there are many steps involved in this process. It all starts with, "do we even really want to log and monitor this activity?"
In a hypothetical world, a security professional's dream answer would be, "Yes, and every single action that may represent a `security relevant` event should indeed be logged."

Understanding Detection Surface
--------------------

Forrester (Allie Mellen) just shared a [wonderful article](https://www.forrester.com/blogs/introducing-detection-surface-the-cybersecurity-defense-that-parallels-attack-surface/) coining the quintessential term `Detection Surface.` It is a recurring topic amongst Cybersecurity professionals, when talking about what is possible to monitor, detect, and respond to.

A simplifying concept was much needed, and as such, the Forrester team defined detection surface as:

`"The IT asset type upon which detection of attacker activity occurs.`
`Detection surface directly parallels attack surface.`
`It describes the IT assets upon which we can detect attacker activity, much like attack surface describes the IT assets within an estate."`

So what is worth logging?
--------------------

If you happened to learn some basic coding, as some beginners would, you would perhaps insert lines like:
`print(apples)` just to see what is happening with the variable apples after a specific code segment is executed, and you would like to learn from the value, if your understanding of the system state was correct.

Of course, there are more professional ways of `creating a record(=metadata of the) actual system state`, which is the definition of `logging`. Some basic examples of built-in logging opportunities in different languages are below:

{% highlight ruby %}
console.log('something is happening')			# in JavaScript or 
logging.warning('Warning!') 				# in Python or 
logger.log(Level.WARNING, "This is a warning!"); 	# in JAVA
{% endhighlight %}

Imagine that every single line of code of an application or service is executed and logged extensively. This high level of logging is what we call high **verbosity**.

For instance, authentication events are almost always logged in every commercial software(often required by law), but users can do many different things, usually interacting with other objects, data or users. This is entirely dependent on the fantasy and functionality of the application, and the way it was written by the programmers.

The key however is the aforementioned `security relevancy`. This cannot be very easily defined, however you may have a pretty good idea about it.


Start Concise
--------------------

Let's take a random web project, for demonstration purposes I am borrowing some basic code regarding logging, from the [Flask Logging](https://flask.palletsprojects.com/en/2.3.x/logging/) documentation.

{% highlight ruby %}
@app.route('/login', methods=['GET'])
def login():
    user = get_user(request.form['username'])
    if user.check_password(request.form['password']):
        login_user(user)
        app.logger.info('%s logged in successfully', user.username)
        return redirect(url_for('index'))
    else:
        app.logger.info('%s failed to log in', user.username)
        abort(401)
{% endhighlight %}

At best, from the above code we will get a log which may look approximately like this:

{% highlight ruby %}
user_alice logged in successfully
user_bob failed to log in
user_bob failed to log in
user_bob failed to log in
user_bob logged in successfully
user_alice logged in successfully
mallory logged in successfully
{% endhighlight %}


Add Verbosity
--------------------

Of course, we can add timestamps and context, and follow some additional guidelines, but we still won't be able to see any change, that a user would make (for example if `mallory` was created using user_bob's account, after successfully brute-forcing it's password) could be of interest, say initiate a payment, change it's phone and recovery email address to steal an account, etc.
Such transactions may contain personally identifiable information(PII) or details of the system, that should not be openly shared in a logfile. The reason is, that transactional events should belong to a database, that has limited access, and not dumped into a logfile. 

While the above example was demonstrating conciseness, it was missing required verbosity. We can extend verbosity by combining the above with information such as `logged in from IP 10.10.10.23 using MFA with the role_financial_approver from device <unknown>` , which requires that the application knows and logs such as temporary and immutable properties of the user, and can retrieve them(IP address vs. <unknown> device. 

{% highlight ruby %}
class User:
  def __init__(self, username, name, role, email, phone, mfa, lastip):
    self.username = username
    self.name = name
    self.role = role
    self.email = email
    self.phone = phone
    self.mfa = mfa
    self.lastip = lastip

alice = User("user_alice", "Alice Allister", "finance_admin", "aalice@abc.com", "+1(234) 567-8900", "otp", "0.0.0.0")
{% endhighlight %}

We can refer to each property of alice with it's property, such as `alice.name` or `alice.lastip`
This will also mean, that in our example flask application routing we will also have to handle the user's IP address. Note: It's all pseudocode, for very easy readability. Also, Flask-Security has solved Flask-Login already.

{% highlight ruby %}

{% endhighlight %}

This definitely adds context:

{% highlight ruby %}
user_alice logged in successfully from IP 10.10.10.23
user_bob failed to log in 51.37.81.9
user_bob failed to log in 51.37.81.9
user_bob failed to log in 51.37.81.9
user_bob logged in successfully 51.37.81.9
user_alice logged in successfully 10.10.10.20
mallory logged in successfully 51.37.81.9
{% endhighlight %}

We may think that login from an external IP address is not desired, and that mallory is perhaps a newly created user, not following the user naming conventions(`user_`), and perhaps added by `bob` after a successful attack.

Know when to Stop
--------------------
Adding further attributes such as **timestamp**, **http response codes**, **user agents**, **authentication type**, can all be useful to add **context** and make events **detectable**, and will increase the application development cost, and after a certain point can add unnecessarily verbosity without adding actual detection engineering value.

This is the first in the series of posts, check out the next ones:

[Detection Surface - Security Relevancy](https://inverze.io/blog/detection-surface-series-security-relevancy/)
