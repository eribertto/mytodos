Okay, so let's play with IAM policies.

So if we go into my user groups right now,

I can see that my group admin contains,

and this UI is a bit bugged,

contains one user, Stephane.

So if I go on the right hand side and go to my services

and I go to IAM, so I'll go to the IAM service.

I will show you one thing.

So, this user is an admin user.

And therefore, if you go to, for example, users,

you can see all the users.

Okay, great.

So, now what I'm going to do is I'm going

to remove Stephane from the admin groups.

I'm going to remove this user

and the user will lose the group permissions, that's true.

So the user has been removed from the group

and how do we make sure that this is applied?

Well, if I go on the right-hand side (normal user account)

and now refresh this page, as you can see,

I need permissions to access this page

and my user Stephane is not authorized

to perform IamListUsers on this page.

So that makes sense, right?

Because we removed the user Stephane from the admins group.

So, what I can do is I can fix this

and to fix it, I can go into my users (in root aws account)

Go to Stephane and now I can attach permissions

directly to my Stefane user.

So two ways of doing so, number one is to add permissions

and use policies that already exists or that you created

or add an inline policy to just add policies

directly to the user.

So, I'm going to add permissions

and I'm going to attach existing policies directly

and I will search for IAM.

And I'm going to look for IAM read-only access.

I review, I add these permissions

and now my user Stephane has IAM read only access.

What does that mean?

That means that, for example, if I refresh this page...

Then, as we can see, the user Stephane does exist.

But, for example, if I go to groups

and I try to create a group and call it "developers"

and create this group,

I'm going to get an exception

because I'm not authorized to do create group,

I was only authorized to have read-only access to IAM.

So this really shows the power of IAM and so on.

So, now if I go to my user groups, I can do two things.

So number one, I can go

into the admin group and I'm going to add back

this Stephane user so that we have administrator access.

The second thing I'm going to do is I'm going to

create a group named "developers".

And I'm also going to add Stephane into this group

and I'm going to attach a policy,

whatever the first policy I found

it was direct connect to read only access

and then create this group.

It doesn't matter which policy you're attached to,

I just want to show you a behavior.

Okay so, now we have two groups,

we have the admins and the developers,

and the user Stephane is in both groups.

So what's going to happen is

that if I click on the user Stephane

and look at the policies it has, it has three policies.

One that was attached directly named IAM ReadOnlyAccess.

One that was in two that were in Attached From Groups.

The first one is administrator access from the group admin.

And this one, it was direct connect read only access.

from the group's developers.

So, as we can see, the policies get inherited

in different ways through the IAM permissions.

So finally, I want to show you how policies work.

So if you go to policies,

we have a list of all the policies available

within AWS right here, their managed policy.

So this one is administrator access

and we've been using it before.

And if you look at the policy, JSON forum, as we can see

we have a version and we have a statement

that statement contains one statements

and the effect is allowed.

So to authorize action is "*",

that means any action resource is "*",

that means any resource.

So we allow all the actions on all the resources

therefore making this policy an administrator access policy.

We can go into policy summary as well

and this is another view of the policy.

We have allow on 284 services of 284.

Now services get added all the time,

so if you don't have the same number,

don't worry, the course is up to date.

So we can have a look at another policy.

For example, the IAM read only policy

that we've dealt with from before.

So, this time allows one service out of 284,

which is IAM.

And if we look at the JSON documents,

we can see all the actions that are authorized

by this IAM read only access.

So we get, for example, iam:get*,

the star GenerateCredentialsReport,

and so on, on the resource start.

There's also a way for you to create your own policy.

So you can go back to your policies and create a policy

and you have two ways of doing it.

Either, you want to write plain and simple JSON

or you can use the visual editor,

and this is quite handy.

For example, we can choose the service IAM,,

then we can choose an action.

And we can, for example, do a list user,

so I can filter for list users

for effects and I can do get user.

So, let's say we want to add these two actions

and on the resources we can specify specific resources

or all resources.

We could also specify a request condition if we wanted to.

So, once we've done that

if we go to the JSON documents

as we can see the visual editor SID was added,

which has the statement ID,

and we have two actions that were added.

So IAM list users and get users on resource start.

So it's quite a handy way to generate JSON directly

from the visual editor.

Okay. So, just to finish this lecture,

let's do a few things.

In user groups, I'm going to delete the developers group

cause I don't need it

and I need you to type the name of the group,

so I will type developers and click on deletes.

And also on my user as Stephane,

I'm going to remove the policy that was attached directly

because we don't need this IAM read only policy,

I will just remove it and we're good to go.

So, now my user Stephane has a full administrator access

because it is inherited from the admin group.

And so obviously if I go back to my IAM

also on the right side,

as we can see, everything is working just fine.

So I will refresh and here we go,

things are working.

So that's it for this lecture.

I hope you liked it

and I will see you in the next lecture.