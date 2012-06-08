---
layout: post
title: "Glass Bottles and the Law of Demeter"
date: 2012-06-07 21:41
comments: true
categories: 
---

I can't throw glass bottles in the bin anymore.  I'm not a dread-locked earth hippy but I've been recycling for so many years that it just feels...wrong.

Good habits work best when they're instinctual - like muscle memory.

<!-- more --> 

What if this looked weird to you?

{% codeblock lang:ruby %}
organisation.subscription.memberships.create(user_id: user.id)
{% endcodeblock %}

If you're a Rails developer this kind of thing probably litters your code but anyone with a site of significant size knows what impact this has on your tests.

{% codeblock lang:ruby %}
it "creates a membership" do
  o = Organisation.create
  subscription = o.subscription.create
  
  # hit the database a few more times
end
{% endcodeblock %}

Anyone else tried TDDing with a 10 minute-long test suite?

It also makes inject additional logic into process a real pain:

{% codeblock lang:ruby %}
class Membership
  before_create :sadface
end
{% endcodeblock %}

So what if you instinctually *had* to abstract that interface - because chaining methods just feels wrong:

{% codeblock lang:ruby %}
organisation.issue_membership(user)
{% endcodeblock %}

You only have to test the logic within the object you're interested in. If the connections to other objects are only one level too, simple stubbing is all you need:

{% codeblock lang:ruby %}
it "creates a membership" do
  o = Organisation.build
  subscription = stub
  subscription.should_receive(:issue_membership).and_return(true)
  o.stub(subscription: subscription)

  o.issue_membership(stub)
end
{% endcodeblock %}

Injecting logic becomes trival and remains in the right place.  It also means the top-level interface to ```Organisation``` stays untouched, regardless of what happens futher down the logic chain.

{% codeblock lang:ruby %}
class Subscription
  def issue_membership(user)
    happy_face
    memberships.create(user_id: user.id)
  end
end
{% endcodeblock %}

The thinking here is nothing new and is only a shallow implementation of a deeper concept, but small habits can reap big rewards as your application grows.

## Key Points

* Consider the entry points into the objects you create
* You shouldn't have to poke into objects that aren't directly connected an object
* Testing first will help with this - if you're creating a load of objects just test one line of logic in a method - you should hear alarm bells

## Further Reading

* [Objects on Rails](http://objectsonrails.com/)
