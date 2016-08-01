# hello_bot

hello_bot is a skeleton for a facebook messenger bot to run on Openshift.<br>
If you follow the tutorial below, your bot should be up and running in less than an hour... or at least a couple of hours... at most a day :D

If you find any errors in this tutorial, don't keep them! Send them to me, so we can make this tutorial even better.
The same obviously goes for any suggestions or ideas ;)

## Accounts, Accounts, Accounts

First of all, let's create all the accounts you need for this tutorial (if you haven't yet):
* [Facebook Developer Account] (https://developers.facebook.com/) <br>
* [Openshift] (https://www.openshift.com/) We will use this service to host your bot. Just think of it as the magical box that makes your bot able to talk to Facebook. <br>
* Useful for the future, not needed for this tutorial: [Github] (https://github.com/) <br>

## Tools & SDK

If you work on a Windows computer, you will first and foremost need these things. Go ahead and install them right now. (They are already pre-installed on Mac. However, we encourage you to update ruby on your Mac):
* [Python 2.7](https://www.python.org/downloads/ ) <br>
* [Ruby 2.0.0](https://www.ruby-lang.org/en/downloads/) If you're on windows, make sure to install version 2.0.0!!

The things you will need to work on your bot:

* [Git](https://git-scm.com/downloads) install this ominous thing right now, we will need it later<br>
* [RHC Tools](https://developers.openshift.com/managing-your-applications/client-tools.html) these tools will help you with openshift things like ssh-keys and finding out what you're bot is doing, we will come to that in a bit <br>
* [Postman](https://www.getpostman.com/) (optional) you can use this chrome extension to send HTTP requests to facebook for testing reasons, however you don't have to do that <br>

To actually produce code, choose your option:

* [PyCharm Community Edition](https://www.jetbrains.com/pycharm/download/) this IDE (integrated development environment) will make a beginner's life easier as it helps with syntax and stuff <br>
* [Sublime Text] (https://www.sublimetext.com/) if you prefer a simple text editor <br>
* [Atom] (https://atom.io/) if you prefer a simple text editor based on web technologies <br>
* whatever you want to use, just have something ready.

## Hello Bot

We have setup a very simple hello_bot that just throws everything you write back at you.
It is based on the awesome [Flask Framework](http://flask.pocoo.org/) and should allow you to be up and coding in no time.

If you have no idea about Git, maybe check out [this](http://rogerdudler.github.io/git-guide/) tutorial.
In case you have a little more time check out [this](https://try.github.io/levels/1/challenges/1) too ;)

## Openshift

Go to [Openshift Web Console](https://openshift.redhat.com/app/console/applications) and sign up for their free plan, if you haven't yet. Here you can host up to 3 applications for free. <br>
(INFO: The only restriction is that if your bot doesn't receive any request for 24 hours
your free Openshift gears will go into idle mode. That means the next request will take a little longer (up to 30 seconds) until the gear is booted up again.)

On the Openshift website add your first application and choose the Python 2.7 Cartridge.
<br>Set your application name (e.g. name of your bot without spaces) and the domain (e.g. `lemmings`) under which it will be hosted.
<br>Further down you see the point `Source Code`. Here add `https://github.com/moccadroid/hello_bot.git` and the branch `openshift`.<br>
<br> Skip the rest, it doesn't make any difference and will mostly confuse you. Just jump to `Create Application` <br>

Openshift will now pull the `hello_bot` from our github account and deploy it.
<br>After this you can go to the URL you created for your Openshift application (something like https://yourbot-yourdomain.rhcloud.com) and should see "Hello World".
Congrats, you just created an application on the Interwebs :+1:

Now some nerdy stuff ;)
I hope you've installed Ruby at that point, because now we'll need it.
Open up a terminal... ***whaaaat?*** :cold_sweat:
On Windows you press the Windows Key and just type `cmd`. A black window should open which is a terminal. Windows calls it "Command Prompt"<br>
On Mac OSX you press Command + Space and type `terminal`. A white window should open which is a terminal. OSX calls it "terminal" ;) <br>

Now we're going to install the RHC Tools (i.e. client tools for Openshift). These tools will help you build cool stuff:

Enter your first command to install the RHC Tools:
```
$ gem install rhc
```
This takes a bit... when you're done you have to setup your openshift account with the following command:
```
$ rhc setup
```
1. It will ask for the server hostname. Just hit enter!
2. You need to provide your username (your e-mail address, you registered with) and your password
3. It will ask you to create a token for you. Type `yes` and hit enter! This will create an ssh-key for you.
You can answer any questions with yes, if you're unsure ;)


In your Openshift Cartridge you see a link to the Source Code that looks something like this:
<br>`ssh://xxxxxxxxxxxxxxxxxxxxxxxxxx@yourbot-yourdomain.rhcloud.com/~/git/yourbot.git/`
Copy this link to your clipboard.

If this doesn't show and you only see a link to "add an ssh-key", click on that and cancel. When you go back to your application, you should see the link to your Source Code (like above).

For the next step open your (git) terminal:
**Windows people**: You need to open the git command line to do this. It is hidden in your git folder in programs.
**Mac people**: this works with your built-in terminal :tada: :tada:

First you need to navigate to the folder where you want your code to reside. When you open a terminal, you start in your user's directory. To change the directory you need the `cd` command (cd as in Change Directory :wink:).

Type `cd Desktop` to change to your Desktop. Hava a look at Codecademy's [Command Line Tutorial] (https://www.codecademy.com/learn/learn-the-command-line) to discover the basic navigation on the terminal. We know the Desktop seems like a nice place in the beginning, but we encourage you to make use of your file system :wink:

Now that your at your chosen destination, type the following:
```
$ git clone ssh://xxxxxxxxxxxxxxxxxxxxxxxxxx@yourbot-yourdomain.rhcloud.com/~/git/yourbot.git/
```

Open this folder with your editor and you're set up to develop your first bot!! :)
<br> If you don't know where your sourcecode is, it should be in your home directory in the folder named like your bot ;)

## Facebook

We're halfway through, so now we need to set up Facebook, to work with our hello_bot.
If you haven't already, go and create a Facebook Developer Account [here](https://developers.facebook.com).
<br>While you are there, create a Facebook Page that you will use with and for your bot.
<br>I will wait :)

Done?<br>
Nice!

Log in to your Developer Account and create a new App. If Facebook asks you what type you want, just click "basic setup" at the bottom, fill out the fields and choose "Apps for Pages" as your category.

In your new App you see the menu point "+Add Product" on the left side. I suggest you click on it to see what happens :)
<br>
The next couple of steps might seem a little confusing at first, but bear with me, we're almost done.

Click on "Messenger", select your page and copy the Page Access Token.

Remember your hello_bot's sourcecode you checked out before?
<br> Go to your editor, open "main.py" and at the very top you see a variable "access_token". Add your Facebook Access Token here and save the file.
<br> On your command line, go to your bot directory (where the sourcecode is, remember the `cd` command :wink:) and enter the following command:
```
$ git commit -a -m "access_token changed" && git push
```
You have now committed and pushed the changes back to the Openshift Git Repository.<br>
Openshift does everything for you now and deploys your code directly to your cartridge.
<br> Like before, go to your bot URL and look for "Hello World".

Everything cool?

Great!! Let's tell Facebook where our bot is!

On your Facebook developer page we left off, when you created the Page Access Token. <br>
The next step is to setup the **Webhook**.<br>
Copy the Access Token again, click on "setup webhook" (underneath) and paste it into the field that says "Verify Token".<br>
In callback URL you enter `https://yourbot-yourdomain.rhcloud.com/webhook`.<br>
It's the same URL that you used to see the "Hello World", but this time with "/webhook" added at the end. <br>
Facebook will POST all its communication to this endpoint, which in turn becomes the starting point for your bot.

Check all the Subscription Fields... just to be sure ;)

Click on "verify and save".

You should now see a green checkmark saying "Complete". Select your Facebook page underneath to subscribe your webhook to it. You can now chat with your bot by messaging your Facebook page.

To add people who can interact with your bot, you can add them under "Roles" in your App's Facebook Dashboard.

If you want to use Postman to checkout HTTP requests, do the following to talk to your bot:

Open Postman and send a POST request to the following URL:<br>
`https://graph.facebook.com/v2.6/me/subscribed_apps?access_token=PAGE_ACCESS_TOKEN`<br>
PAGE_ACCESS_TOKEN needs to be the same token that you've used twice now. Just replace it and POST the link.

The result in Postman should look like this:
```
{
  "success": true
}
```

## You did it!!! :tada: :tada: 

If you've made it this far (and everything worked out) you can finally go to your Facebook page and click on "message".
<br>
<br>
Type something... Raise your arms, and yell "Bots bots bots bots bots!!!" :D

## What now??

If you've never programmed, you now sit in front of your bot and have no idea what to do next.
<br> I have some suggestions you could try:

Find the following line in your main.py:
```
reply(sender_id, message_text)
```
and change it to:
```
rules(sender_id, message_text)
```

Now post the following code at the end of your main.py:
```
def rules(recipient_id, message_text):
    rules = {
        "Hello": "World",
        "Foo": "Bar"
    }

    if message_text in rules:
        reply(recipient_id, rules[message_text])

    else:
        reply(recipient_id, "You have to write something I understand ;)")
```

## What have we done??

We have added a new function that allows us to reploy to specific words that the user sends our bot.<br>
```
rules = {
    "Hello": "World",
    "Foo": "Bar"
}
```
This is called a dictionary. You can add as many variables as you like. The left side of each entry is what the user has to enter, to get the right side.<br>
You could for example send the user a link to a cat picture if they send your bot the word `cat`.
Your dictionary could then look like this:
```
rules = {
    "cat": "https://lazycuriokitty.files.wordpress.com/2013/06/36345108.jpg"
}
```
Now in your terminal (in the folder where your code is) just type this again to push all the code to openshift:
```
git commit -a -m "dictionary" && git push
```
