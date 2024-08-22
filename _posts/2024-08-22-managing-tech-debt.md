---
layout: post
title: "Stop fighting tech debt, start managing it"
categories: "software-excellence"
---


At this point, maybe even your parents have heard about tech debt.

You know, it's that thing that your engineers keep talking about to justify their damn low velocity.
I know what you're thinking: "I don't care about _the_ tech debt, I only care about value delivery and deadlines!"

But what if I told you that managing tech debt can actually help you:
- Deliver consistently?
- Plan deadlines confidently?
- Keep team morale high?
- Keep your stakeholders' trust in you?  

   

---    

   

## A typical project start

Let's start with a simple example of a new project:

Business has greenlit the MVP, the team is excited, and the first lines of code are being written.
Within a week or so, the first feature is live, and the team is celebrating. The business is happy, and the team is motivated to keep going.
Business provides feedback, some adjustments are made, but nothing the team can't handle.
On the contrary it creates a synergy that pushes them to deliver more.
Features keep getting added, everyone is happy.

If we plot the value over time on a graph, it would look like this:

![Value delivery over time](/assets/img/steep-start.png)

This is a typical "high-velocity" start.

But as the project grows, the team starts taking more time to add or modify basic features - when it was taking them mere hours a few months prior.
And now at the end of a sprint, you realize that only a fraction of what was promised could be delivered. The team start talking about doing a big refactor, or even worse a complete rewrite??

And now the value over time looks more like this:

![hitting-tech-debt-wall.png](/assets/img/hitting-tech-debt-wall.png)

The velocity has gone down, dramatically.
This is a huge problem as you cannot promise anything in reasonable time to the business anymore, and you start making excuses as well.
And if you ever bring up the concept of "tech debt", you only see their eyes glazing over, and they start thinking about alternatives to your product.

And if you would carry on like this, your team will eventually burn out and quit. Sealing definitely any hope of delivering anything more.

IF you are one of the few product/team leads that can convince the business and the team to carry on the required refactoring, you will see the value delivery brought to a halt for a while.  

But keep your hopes up! After some time, the value delivery will start to go up again, and you will be able to deliver again:

![big-refactor.png](/assets/img/big-refactor.png)

And here we see that after the refactoring, the value delivery is back on track.

But there is a bittersweet taste left: your risked your team and your product to get here.

## What happened?

This is a typical example of hitting the "critical tech debt mass".
It is a point where people lose confidence in the ability to deliver, team and business alike.

![ciritical-tech-debt-mass.png](/assets/img/ciritical-tech-debt-mass.png)

## What is tech debt really?

I believe there are 2 types of tech debt:
- Corner Cuts
- Implicit Assumptions

Some believe that tech debt is only about the first type, but I think that it hinders value delivery and requires to be adressed all the same to restore velocity.

### Corner Cuts

Corner cuts are the original definition of tech debt: when you knowingly make a decision that will make you go faster now, but will slow you down later.
That is why this is called "debt": you borrow velocity now, pay interests constantly until your pay it back.
In software that would mean typically to not write tests, to deploy manually, to not document your code, to not make along-the-way refactors, etc...

These _of course_ take time, but will make any future addition take more time, code breaks more easily, is less readable, etc...

### Implicit Assumptions

These are unfortunately unavoidable, and is the reason why even the best team in the world, with the best practices and the best tools, will still accumulate tech debt.
Implicit assumptions are the things that you don't know you don't know about the business, the technology etc...
And these will only be revealed when you hit them.

A typical example is in manufacturing. You start by writing software to automate a machine which does a simple operation A.  

But the business wants to add a machine that does a different operation, B, and that operation produces multiple outputs, which you did not anticipate.
No problem right? The team can just add a special case.

But of course at some point yet another machine is added, with multiple operations this time: C, D & E. Damn, yet another special case.
And so on... and so forth.

![special-case.png](/assets/img/special-case.png)

As you can guess, you cannot keep adding special cases. Although these machines are definitely unique, in manufacturing they represent very simple processes.
And no proper manufacturing software will handle these cases as "special", this is business as usual.

So your team *HAS* to refactor and represent the general case of manufacturing, which could be:

A machine of type **M**:
- can apply **P** different operations
- Takes **I** items as inputs
- Produces **J** items as outputs
- ... and more

Failing to do so, will make the software unnecessarily complex and verbose.
Changing a feature would require to change it for all machines separately instead of changing the general case.

## The trap of going the other way

Let's say you are a team lead, and you have been through this before. It is tempting to try and address the problems from the start.  
Let's build a platform with automated testing, automatic deployment, built-in documentation, etc...  
Also let's discover as much information about the field, and let's try to solve the general problem from the start.  
(Like the general case of manufacturing, typically)

Well that is a trap. You will spend a lot of time on things that are not bringing value to the business.  
Starting with building a platform too abstract to build a viable product is typical "Speculative Engineering" and is as bad as hitting the critical tech debt mass.

![speculative-engineering.png](/assets/img/speculative-engineering.png)


## Managing tech debt with 2 tickets

This type of visualisation leads to me to believe that there is an optimal amount of value delivery that can be delivered for a given amount of time.
Which keeps in balance tech debt and speculative engineering. On the graph it can be represented by the diagonal line.
But it will be different for each team, and each project.

However, corner cuts and implicit assumptions will always show up. The business will ask for a short term delivery when the team needs take a step back and refactor.
I tend to believe that the business usually have the priority, at the end of the day, they pay the bills.

Therefore, I propose to manage tech debt with 2 tickets:
- 1 ticket for the business: Feature is delivered in time, with an acceptable amount of tech debt
- 1 ticket for the team: Refactoring is planned and worked on just after the feature is delivered

With this, I usually create a contract with the business: you will have the feature delivered in time, but the teams takes extra time in the (short) future to stabilize the software.
Everyone involved should be made aware of this. And surprisingly sometimes the business might agree to delay the feature to "make it the right way from the start".

If applied rigorously, the team will be able to deliver consistently, honor deadlines, keep morale high, keep stakeholders' trust.

![2-tickets.png](/assets/img/2-tickets.png)












