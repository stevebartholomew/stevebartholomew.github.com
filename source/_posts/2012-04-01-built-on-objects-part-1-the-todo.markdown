---
layout: post
title: "Built on Objects Part 1: The Todo"
date: 2012-04-01 20:55
comments: true
categories: 
---
Todoist is a simple todo list application that I’ll be building from the ground up, focussing on the objects and interactions first.
<!-- more -->

I’ll be using Ruby 1.9.3, Rails 3.2 and Rspec with Capybara for testing.

## Feature #1: Adding a Todo

### An integration test
The first thing I do is create a test explaining how I as a user want to interact with the application:

*spec/integration/todos_integration_spec.rb:*

{% codeblock lang:ruby %}
require "spec_helper"

describe "Todoist" do
  context "creating a todo" do
    it "provides a form to create a new todo" do
      visit "/"
                                                                                                      
      fill_in "todo[body]", :with => "Just something I need to do"
    
      click_button "Save"
  
      page.should have_content("Added")
    end
  end 
end 
{% endcodeblock %}

This wont pass and there’s a lot that needs to be hooked up for it to work so I’m going to forget about it for the moment.

The Todo class
My feature is ‘Adding a Todo’ so the first thing I’ll do is make a spec for a class called ‘Todo’ and a method called ‘add’:

*spec/models/todo_spec.rb:*

{% codeblock lang:ruby %}
require_relative ‘../../app/models/todo’

describe Todo do
  it "adds a new todo item" do
    task = "Something I have to do"
      
    todo = Todo.add(task: task)
    todo.task.should == task
  end
end
{% endcodeblock %}

Getting this to pass is straight forward:

*app/models/todo.rb:*

{% codeblock lang:ruby %}
class Todo 
  def initialize(attributes)
    @attributes = attributes
  end 
    
  def task 
    @attributes.fetch(:task)
  end
  
  def self.add(attributes)
    new(attributes)   
  end
end
{% endcodeblock %}

More than one object
A single instance on its own isn’t particularly useful though.  I’ll add storage and retrieval:

*spec/models/todo_spec.rb:*

{% codeblock lang:ruby %}
it "gets all todos" do
  todo = Todo.add(task: "Something")
  Todo.get_all_todos.last.should == todo
end
{% endcodeblock %}

And my Todo class becomes: 

*app/models/todo.rb:*

{% codeblock lang:ruby %}
class Todo 
  @@_todos = []

  def initialize(attributes)
    @attributes = attributes
  end
    
  def task 
    @attributes.fetch(:task)
  end
  
  def self.add(attributes)
    todo = new(attributes)   
    @@_todos << todo
    todo
  end

  def self.get_all_todos
    @@_todos
  end
end
{% endcodeblock %}

I can now add todo and retrieve them later.

**Next up:** I'll hook this up to a controller.

You can [view this commit on github](https://github.com/stevebartholomew/todoist/tree/77c29e49ae38a6b8ce3be2254b3809b43349fc18)

Got a comment? Drop me a message on [twitter](http://twitter.com/sbartholomew).

[Subscribe](/atom.xml) to hear about the next in the series. 
