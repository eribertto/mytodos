Let me show you how to create access keys.

I'm going to click on my user

and as you can see right now in the top right-hand side,

I am connected using the my IAM User on my account.

So this is something you have to do,

do not use your root account

to create security credentials.

Okay?

So I'm using my IAM User,

and I'm going to go and create Security credentials.

So I'm gonna just scroll down

and again create Access keys.

So Access keys are going to be very helpful

if we use the CLI.

So if we use the command line interface,

or if we use the SDK

to implement some programming language against AWS.

So I'm going to create this Access key

and they are very, very secret.

This is the only time you will see them

and that they can be downloaded.

You cannot recover them later,

but you can create new ones if you wanted to.

So never, ever share them before.

And I will invalidate mine after this hands on.

So you can download a CSV file if you wanted to,

to keep them on your computer,

or you can show the Access key ID and the Secret access key.

Again, these are secrets

and they will be worthless for you

because I'm going to invalidate them.

Then we need to use these secret Access key

and Access key ID.

The first thing you have to do

is to configure my AWS utilize.

So I'm going to type "aws configure".

And then I am greeted with entering my Access key ID.

Very nice.

I can just enter this one and press Enter,

and then I'm greeted with entering my Secret access key,

which I will enter right here as well.

The Default region name,

so this is a region that is close to you,

I will choose eu-west-1

because I will be doing all my tutorials in eu-west-1,

but you will choose your own region

and you can enter your own region name,

that the region name, by the way,

you can get directly from this drop down right here.

It shows you the name of the region,

as well as the region code.

So for me, I'm going to use my eu-west-1.

I'll press Enter.

And then the Default output format,

I'll just press Enter as well.

So now my AWS CLI is configured.

And so we can have a look at how it works.

We can do "aws iam list-users" and press Enter,

and this will list all the users in my accounts.

And as we can see,

the user I have right now is called "stephane".

Here is a UserId.

Here is an Arn when he was created

and when the password was last used,

which is very similar to what I would get

if I were to go into this UI right here.

So the management console

and the CLI do provide similar kind of information.

Next, I want to show you what happens

if we remove permissions from our users.

So I'm going to go to admins

and I'm going to remove the stephane user

from the group admin.

And so again, if I go back to my user stephane,

it doesn't have any permissions.

And I did this obviously with my root account,

not the other account.

So now if I go into my UI and obviously refresh this page,

I'm going to get an error saying that, "Yes,

"I do not have the permissions to do this,"

but let's try to do the same thing with a CLI.

So we're going to do an iam list user call,

and we get no response because actually it was being denied.

So the CLI permissions are obviously going to be

the exact same as the permissions you get

from the IAM console.

So the takeaway from this lecture

is that you can access AWS using the management console

or using access key and secret access key

that you can configure and then use into the CLI.

So hope you liked it.

And I will see you in the next lecture.

And obviously do not forget to add your user back

into the group.

Otherwise, that would be horrible.

So I'm going to go into groups, admins,

and I'm going to add my stephane user back into my group.

And now I am an administrator again.

So that's it.

I will see you in the next lecture.
