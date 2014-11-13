---
layout: post
title: "Playing with RubyMotion"
date: 2014-09-21 19:51:51 +0200
comments: true
categories: Ruby RubyMotion Mobile
---

For long time I have feelings that creating a mobile app is a nightmare. There are many ecosystems and each of them has a different technology stack (thanks God that we can focus only on few of them). For sure there are many different challenges when you are developing mobile
app rather than web based solution, but for me one of the major problem was using the native languages. Moreover I want to be available on both major platform(iOS and Android). In the result mobile dev didn't give me a joy and fun, so I have abandoned it for a while. I have returned recently to the mobile world thanks RubyMotion, which solves my previous problems.

## Ruby meets a mobile
The most important thing for me is fact that I can use my daily weapon of choice, Ruby to create a mobile app. In another hand it doesn't exempt from the knowledge of the iOS or Android SDK, yeah there are a lot of things to learn. The biggest advantage of the RubyMotion is possibility of using same native API from the Ruby side (even we can mix native method calls with the Ruby). There is no additional toolkit layers, you have to know how to translate native SDK to RUBY. Moreover you have to be aware off differences between MRI and RubyMotion, yeah there are few of them, but in my opinion it's a minor thing.

## Work flow
RubyMotion is a great example how to create awesome console tool which solves non trivial problem. After installation you get `motion` command which offers some basic options.

![Motion CLI](/images/motion.png)

Creating a new project is similar to `Rails` like way, just run `motion create project_name` and you create a new iOS project ( it's a default project template, you can use `--template=osx|android` option to change it). Keep on mind that currently Android in the beta stage and it's available in the pre channel `motion update --pre`.

![Motion CLI](/images/motion_create.png)

Inside the new project you have all necessary tasks available via our good friend `Rake` which simplified the hole development process. Moreover RubyMotion doesn't require the additional IDE, use your beloved editor and start working on your new idea. RubyMotion provides special task for generating ctags via `rake ctags` for a project, so if your editor support it, you should try it, the development is more easier.

![Motion Rake](/images/motion_rake.png)

## REPL is the power
The most awesome feature is interactive console which is available when you are running your app in the development environment. This kind of Rails like console give a developer a lot opportunities to debug application behaviour in simple way. Moreover you can easily switch to the context of selected UI element and invoke some events from the console using Firebug like style. Press command key and selected element should receive red borders and click on it. From that moment your main context is selected UI element.

![Motion REPL](/images/motion_repl.jpg)

## Testing culture
I have been on some mobile meetups in the 3city and I have found that writing unit/integrations tests for mobile is not so popular. Most common opinion was that it's hard and it doesn't have much sense. It's not a joke. I have good info for you, welcome in the Ruby world. RubyMotion promote one of the best practice from the Ruby community, testing culture. It support application testing via Rspec like framework, which based on [bacon gem](https://github.com/chneukirchen/bacon). Creating tests for mobile app is noting scary e.g:

```ruby
describe "ToDos View" do
  before do
    @app = UIApplication.sharedApplication
    @delegate = @app.delegate
    @table = @delegate.instance_variable_get("@table")
  end
  it 'should exist' do
    @table.should.not == nil
  end
end
```

## Conclusion

RubyMotion is great example how we can use Ruby for the new use cases. In my opinion this solution is worth to consider for every who want to build multi platform app, despite the fact that it requires purchasing the licence. Personally I have found a lot fun and joy working on my mobile apps thanks RubyMotion.
