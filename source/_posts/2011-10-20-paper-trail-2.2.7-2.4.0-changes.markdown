---
layout: post
title: PaperTrail 2.2.7-2.4.0 changes
date: 2011-10-20
comments: true
categories: papertrail
---

## 1. Changeset

From PaperTrail 2.2.7 release you can find a new method of <b>Version</b> instances, called <b>changeset.</b>
PaperTrail doesn't have <b>diffs</b> mechanism inside, but now if you have <b>object_changes</b> column in <b>versions</b>
table (it can be generated automatically if you install PaperTrail with <b>--with-changes</b> option) it will store Rails' <b>changes</b> of dirty objects.

``` sh
$ rails g paper_trail:install --with-changes
# or manually add `object_changes` column in your `versions` table
```

``` ruby
>> widget = Widget.create :name => 'Bob'
>> widget.versions.last.changeset                # {}
>> widget.update_attributes :name => 'Robert'
>> widget.versions.last.changeset                # {'name' => ['Bob', 'Robert']}
```

More information about Diffing Versions you can find in PaperTrail [README](https://github.com/airblade/paper_trail#diffing-versions) on GitHub.

## 2. Flexibility in naming of methods

There are some situations when methods <b>version</b> and <b>versions</b> are already busy by other associations or smth.
In this case we can change the names of these methods in our application (but sometimes it's time-consuming)
or we can configure these methods in PaperTrail like that:

``` ruby
has_paper_trail :versions => :paper_trail_versions,
                :version_name => :paper_trail_version
```

## 3. Add :on option

With this option we can configure what events we need to track. For example, we don't need to track <b>create</b> events:

``` ruby
has_paper_trail :on => [:update, :destroy]
```

## 4. Without Versioning

In some cases some action/actions must be executed without versioning. Now PaperTrail has simple wrapper for this case:

``` ruby
# Executes the given method or block without creating a new version.
def without_versioning(method = nil)
  paper_trail_was_enabled = self.paper_trail_enabled_for_model
  self.class.paper_trail_off
  method ? method.to_proc.call(self) : yield
ensure
  self.class.paper_trail_on if paper_trail_was_enabled
end
```

Usage:

``` ruby
# With method name
@widget.without_versioning :destroy

# or with block
@widget.without_versioning do
  @widget.update_attributes :name => 'Ford'
end
```

## 5. Attr Accessible
Now we need to use <b>attr_accessible</b> if we want to store some <b>meta</b> info in <b>versions</b> table. Example of <b>meta</b> information from PaperTrail README:

``` ruby
class Article < ActiveRecord::Base
  belongs_to :author
  has_paper_trail :meta => { :author_id  => Proc.new { |article| article.author_id },
                             :word_count => :count_words,
                             :answer     => 42 }
  def count_words
    153
  end
end
```

In this case <b>author_id</b>, <b>word_count</b> and <b>answer</b> are <b>meta</b>, and we need to have these columns in <b>versions</b> table. And also we need to add these <b>attrs</b> to <b>attr_accessible</b>

## Peace!

