---
layout: post
title: PaperTrail Ignore vs Skip
date: 2011-11-17
comments: true
categories: papertrail
---

:skip attribute/key was released in PaperTrail 2.4.1 What are the differences between :ignore and :skip?
For example we have <b>Article</b> model with ignored <b>title</b> field and skipped `file_upload` field:

``` ruby
class Article < ActiveRecord::Base
  has_paper_trail :ignore => :title,
                  :skip   => :file_upload
end
```

Create empty article object, initial version'll be created:

``` ruby
>> a = Article.create
>> Article
=> Article(id: integer, title: string, content: string, file_upload: string)
>> a.versions.count
=> 1
```

If we update ignored <b>title</b> attribute, version won't be created.
If we update non-ignored <b>content</b> column, version'll be created
and we'll have stored changes of object in <b>object_changes</b> column that available through <b>changeset</b> attribute.

``` ruby
>> a.update_attributes :title => 'Title'
>> a.versions.count
=> 1
>> a.update_attributes :title => 'New Title', :content => 'Content'
>> a.versions.count
=> 2
>> a.versions.last.changeset
=> {"content"=>[nil, "Content"]}
>> a.versions.last.reify
=> #<Article id: 1, title: "Title", content: nil, abstract: nil, file_upload: nil>
```

As we see ignored <b>title</b> column not stored in changeset but it stored in dumped object.
But there are some cases when we don't need to store some columns in dump object by various reasons.
For these cases :skip key has been created. :skip and :ignore work identically, but :skip doesn't store
data of <b>skiped</b> columns in object dump. That's it.

Information about attributes tracking you can find in paper_trail PaperTrail
[README](https://github.com/airblade/paper_trail)
(Choosing Attributes To Monitor) on GitHub.

[Issue](https://github.com/airblade/paper_trail/issues/92) about :skip on GitHub.

## Peace!

