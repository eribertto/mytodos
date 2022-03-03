So we are going to be launching

our first EC2 instance,

and it will be running on the Linux operating system,

and to do so we will do it using the AWS Management Console.

That will allow us to get a high-level approach

to understanding some parameters

for the configuration of your EC2 instances.

Then, we'll use something called an EC2 user data script

to configure our web server.

And then, we can see how we can start,

stop, and terminate our instances,

just to see how the cloud can be powerful for elasticity,

agility, and all these kinds of things, okay?

So let's get started.

So let's get our first hands-on with the EC2 service.

So let's type EC2 in the search bar

and go directly into the EC2 console.

So what we're going to do is launch EC2 instances.

But before we do so,

please make sure you're choosing a region,

again, that is close to you.

So for me, I'm in Europe, Ireland.

So we'll go into instances,

and we will start our first EC2 instance.

So for this, we first have to choose an AMI,

called Amazon Machine Image,

and we have a bunch of different choices right here.

We have Quick Start,

which is a way to use the AMIs that are provided by AWS,

but also My AMIs, as we'll see, we can create our own AMIs.

There is an AWS marketplace for AMIs

and finally, Community AMIs.

So for this instance, we're going to use the Quick Start

to launch an AMI named Amazon Linux 2 AMI.

And as we can see, this AMI is free tier eligible.

That means that we will be able to launch it

while not spending any money for now.

So let's select this instance.

And next, we have to choose the instance type.

So as we can see in the screen, the instance type,

there are so many of them.

So you can scroll down and see really different kinds

of instance types for this.

So they're instance families.

As you can see, they're grouped into different names,

and we'll learn about those in this course.

But for now, because we wanna get started with a free tier,

our only option is to choose a t2 micro.

Next, we will configure the instance details.

And so for this, we'll choose

to launch one number of instance.

We will not modify any of the network settings.

So we will launch it into our VPC

or virtual private cloud that is selected by default.

And for IAM role, for now, we don't touch anything.

We won't select it. We'll leave it as none.

But later on, we will have it with an IAM role.

And if I scroll down, the one thing I'm really interested

about is the EC2 user data.

So this EC2 user data is a script that will be launched

during the very and only first boot of the instance.

And so for this, I have created a little script

in the ec2-user-data.sh.

So you have to copy this script entirely

from the very, very top to the very, very bottom,

and then you take that script and you paste it here.

This is going to launch a web server onto our EC2 instance

and write a file to it.

Next, we're getting into the storage.

So in the storage, it say how much data's disk

is going to be available on our EC2 instance.

We'll leave everything as default.

As you can see here, there's a Delete on Termination option.

That means that when we terminate our instance,

the disk is going to go away as well, which is perfect.

Next, for tags, this is how we can add tags

to our EC2 instance.

So for example, we can add a first tag named Name,

and the name is, My First Instance.

We could add another tag, for example, Department,

and choose Finance.

So you can have as many tags as you want.

As you can see, it's going to tag the instance, the volumes,

as well as the network interfaces.

Next, for the security group,

we're going to view them in details later on,

but we're going to, in this case,

create a new security group,

and we're going to add a rule to it.

So I'm going to click on Add Rule,

and I will choose HTTP right here on port 80,

and this rule means from anywhere.

This is going to allow us to access the website

onto our EC2 instance.

So we're good here.

And then, we click on Review and Launch.

As we can see, we get a warning about our instance security

because the group is open to the world.

That's okay. This is intended.

So we can review everything we've done here.

And once we're ready, we'll just click on Launch.

When we launch this, we need to select a key pair.

Now, the key pair is something that we'll be using to SSH,

to login to our instance.

And for now, we don't have any key pairs in our account,

so what we have to do is to create a new key pair.

And then, we have to name it.

So I will name it EC2 Tutorial.

And then, you have to download this key pair.

So this file is downloaded and please do not lose this file.

Once you have downloaded it, please do not lose it.

We will be using it later on in this course.

So when I'm done, I'm going to launch my instance,

and the wizard is complete,

and now my instance is now launching.

So I can click here on this instance

to get to the link of it,

or I can just go on the left-hand side

and click on Instances to load that screen.

So our instance is launching.

And this is the cloud, so the state is pending.

But within 10 to 20 seconds,

my instance is going to be ready.

And here is the whole power of the cloud

is that I can request one instance,

and as you can see right now, it's ready,

in less than 10 seconds, have it ready,

but I could also launch 100 instances like this

and have them ready in 10 seconds.

So the cloud really allows you to be flexible

and to get computing power very, very quickly

whenever you need it.

So our instance is ready,

and we're going to review a few details about it, okay?

So first of all, if we look at the name,

it says, My First Instance,

and this is directly linked to the fact

that we had a tag here named Name,

and the value was My First Instance.

Another thing we can notice is that if I scroll down,

we can look at the fact that the instance type is t2 micro,

which is something we chose, and is part of the free tier.

And if I scroll again down, what I'm going to find

is that the key pair name is EC2 Tutorial,

which corresponds to the key pair

that we have downloaded from before, okay?

And by the way, you can only download it once,

so please do not lose that file.

Okay, so this is good, right?

Next, if we go up, we can see that our instance

has what's called a public IPv4 address right here,

and it has a private IPv4 address right here.

This is what you should expect if you have a new account.

If you don't have a public IPv4 address,

it's maybe because you're using

one of your corporate accounts and they disabled that.

But if you're using a new account just like me,

you will have a public IPv4 address.

If you don't have one,

I'd suggest you get in touch with your corporation

so you can follow this training.

Okay, so why don't we just copy this public IPv4?

Actually, you can just click on open address.

And this is going to open a new webpage in a new tab

to get access to our instance.

So now, we're connecting to our instance.

As you can see, this is not working.

And the reason is, if you look at the full URL in here,

it says HTTPS, but we haven't configured secure HTTP,

so this is never going to work,

and you're going to get an error of a time-out.

So let's not do that.

Instead, and I want to show you the normal type of errors

you're going to get, so you don't have to reproduce them.

Instead, you're going to just copy the IPv4 address,

open a new tab, press Enter, and now this is going to work.

What we get is a response named Hello World from this IP.

So the idea is that we have started a web server

on our EC2 instance

using the little script on the user data,

and it did execute at the instance first boot.

And it is very common in programming

that whenever you're first trying something

for the first time and show that it works,

you just respond with Hello World.

So in this case, I said, Hello World from,

and then here is an IP.

So this IP is different from the public IP we used

to access our instance.

This is because this is the private IP of our instance.

So if I look at the value right here,

and I compare it to the private IPv4 address,

as we can see, they are exactly the same.

So we used a public IP to access our web server,

but it responded on purpose, because I created the script,

with its private IP.

So this is good, right?

So we are starting to get a feel for the power of the cloud.

But now, let's start a new experiment.

I'm going to take this instance,

and I'm going to do Instance State, Stop Instance,

that you can do exactly the same way

by just right-clicking on the instance

and doing Stop Instance.

And this is going to stop the instance.

So in the cloud, you're free to choose

whenever you want to have your instance to be running,

or to be stopped, or to be terminated.

And so that's the whole power of it.

You don't want to leave things running for nothing.

Whenever you're not using an instance,

it is best practice to stop it.

So when you're stopping the instance,

it goes into a state named stopping,

and then it will be stopped.

And so, while this happens, if I try to refresh my webpage,

as we can see now, it's still connecting,

but it's connecting and obviously not succeeding

because my instance is now stopped.

So another thing I could be doing in the cloud

would be to say, "Okay, I have this server,

"but I don't need it anymore.

"I'm going to get rid of it."

So to do so, we do Instance State,

and then we're going to terminate this instance.

So instance termination means that you're going to delete it

and you'll never be able to get back to it.

And it is very common in the cloud to terminate instances.

The reason is, in the cloud, everything is disposable,

and so it is very normal for you to terminate instances,

as we'll see, when we look at auto-scaling,

because you don't need them anymore, you don't need them.

And so it's common to backup the data

before you terminate your instances,

but it is very possible.

But because in this tutorial,

I wanna keep on using my first instance,

I'm not going to terminate it.

Instead, what I'm going to do is to start it again.

So I'm going to start the instance again,

and we're going to see what happens.

So my instance is now running,

but if I try to go back to my website and refresh,

as you can see, it still doesn't work.

And the reason is when you stop an instance

and then start it again after a little while,

the public IPv4 is going to be changed.

So we're going to get a new public IPv4.

The private IPv4 will not have changed,

but the public will have changed.

So I need to copy and paste the new public IPv4,

press Enter, and yet again, I receive my Hello World back.

So this really demonstrates the power of the cloud.

While my instance is running, I'm going to pay for it.

And if I stop it, I'm not going to pay for it.

And I can terminate my instance at any time I want.

I can also request one instance

or 100 instances when I want.

And so this is really a huge shift in the mindset

from traditional IT on-premises.

When you're on-premises, you have to order your servers,

get it delivered, you plug it into your infrastructure,

and you use them for the next three to five years.

But in the cloud, we're talking about seconds,

and you can get rid of it at any time whenever you want.

And this huge change, thanks to the cloud,

is making IT so flexible that it allows people

to run companies with a very, very little IT department.

So that's it for this lecture.

I hope you liked it, and I will see you in the next lecture.