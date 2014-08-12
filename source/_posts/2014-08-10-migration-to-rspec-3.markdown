---
layout: post
title: "Migration to Rspec 3"
date: 2014-08-10 11:28:57 +0200
comments: false
categories: Ruby Rspec Testing
---

I had a little break with my blog and a lot of things happend from the last blog post. I decided try it again and make a second attempt to this with more regular publications.

Few months ago the new version of the Rspec finally arrived. Rspec 3 included many changes which broke the compatibility with the previous version. After reading the [blog post](http://myronmars.to/n/dev-blog/2014/05/notable-changes-in-rspec-3) about the release changes I relized how many thing were changed and may impact on my testing Ruby code.

There are many interesting features provided by the Rspec 3, the most important for me is moving away from monkey patching and introduce verifing doubles. Using those new hot stuff in to new project is so easy (just add the latests version in the project's Gemfile), but how to handle smooth migration process to Rspec 3 in the production/legacy code? The [Transpec](http://yujinakayama.me/transpec/) created by [ Yuji Nakayama](https://twitter.com/nkym37) is awesome tool which moves your specs with easy way to the latest version.

At the beginning you have to install the Transpec gem via `gem install transpec` (it doesn't require to be part of the project. Make sure that the project uses the Rspec 2.14 or higher and you have a clean repository without any changes. In the next step run the test suite and check if all off them are green, then finally run the migration via `transpec` in the project root directory. In the end Transpec creates the summary about the changes which can be included as the commit message e.g

{% codeblock %}
Convert specs to RSpec 2.99.1 syntax with Transpec

This conversion is done by Transpec 2.3.2 with the following command:
  transpec --force --convert stub_with_hash

* 396 conversions
    from: obj.should_receive(:message)
      to: expect(obj).to receive(:message)

* 239 conversions
    from: obj.should
      to: expect(obj).to

* 113 conversions
    from: obj.stub(:message)
      to: allow(obj).to receive(:message)
{% endcodeblock %}

I made migrations to Rspec 3 for my all projects using the Transpec and I didn't find any issues, so in my opinion it's worth to try. You can find more info about the Transpec at the project page at [github](https://github.com/yujinakayama/transpec) and I encourage to check the official [update guide](https://relishapp.com/rspec/docs/upgrade).
