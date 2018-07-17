---
layout: post
title:      "Many-to-many, too many."
date:       2018-07-15 13:10:16 -0400
permalink:  many-to-many_too_many
---


It’s not hard to visualize and demonstrate most model relationships. Most relationships can be easily visualized with books. For instance, `belongs_to` and `has_many` is easy- an author `has_many` books and a book `belongs_to` an author. Let’s say a book is published- chances are, the book only `has_one` publisher, right? These relationships can be easily defined with a foreign key in the corresponding table- in this case, a book would have a foreign key to identify the author and an additional foreign key to identify the publisher.

Establishing and visualizing a many-to-many relationship is a little bit tougher. The `has_many_through` relationship gets a little abstract and it can not only be harder to identify these relationships but also to implement ensuring that your table has correct keys and relationships. So what is a many-to-many relationship? In trying to figure one out that applies to books, I had to meander a little bit and think outside the box. We’ve got this sculpture at work which demonstrates it quite well- one sculpture, `has_many` alligator heads, and many alligator heads `has_many` teeth. Many teeth `belongs_to` one alligator and many alligators `belongs_to`  one sculpture. Many teeth! Many alligator heads! ONE sculpture.

![Many teeth! Many alligator heads! ONE sculpture.](https://imgur.com/hnJNbU1.jpg)

So going back to our books, it could be said that an author has many chapters through their books. And just to be safe, let’s assume we’re talking about a prolific author- like Stephen King or Tolstoy or something- not a one hit wonder like J.D. Salinger. So one author `has_many` books, the author also `has_many` chapters `through` each of their books. So far, so good, right? If we were to map this out, it would look something like this: 

![Mapping out the relationships](https://imgur.com/xQoD06F.jpg)

It’s not the prettiest chart, but having it drawn up at least helps to make a bit of sense of this. So how would you go about setting this up in your rails application? We need to create our migrations! Run `rake db:migration CreateTableName` for each one, ensuring to include your foreign keys as columns. 
```
class CreateBooks < ActiveRecord::Migration[5.2]
  def change
   create_table :books do |t|
		t.string :title
		t.integer :author_id
		t.integer :publisher_id
		t.timestamps
   end
  end
end
```

After you’ve fleshed out all your migrations, run `rake db:migrate`  and your schema might look something like this:

```
ActiveRecord::Schema.define(version: 2018_07_15_020021) do

  create_table "author", force: :cascade do |t|
    t.string "name"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end 

create_table "books", force: :cascade do |t|
   t.string "title"
   t.integer "author_id"
   t.integer "publisher_id"
   t.datetime "created_at", null: false
   t.datetime "updated_at", null: false
end 

create_table "chapters", force: :cascade do |t|
   t.string "title"
	 t.integer "author_id"
	 t.integer "book_id"
	 t.datetime "created_at", null: false
	 t.datetime "updated_at", null: false
end 

create_table "publisher", force: :cascade do |t|
  t.string "name"
  t.integer "book_id"
  t.datetime "created_at", null: false
  t.datetime "updated_at", null: false
end 
```

Now for the final part before you can start working on your controller and your views: Models. We have to declare the relationship within our models too. The models would look something like this:

```
class Author < ApplicationRecord
  has_many :books
	has_many :chapters, through: :books
	has_one :publisher, through: :book
end 

class Book < ApplicationRecord
  belongs_to :author
	has_one :publisher
	has_many :chapters
end 

class Chapter < ApplicationRecord
	belongs_to :book
	belongs_to :author
end 

class Publisher < ApplicationRecord 
  belongs to :book
	belongs_to :author
end 
```

Let's say that you're no Stephen King but instead, a forward looking writer who wants to use the internet as a place for your thoughts via blogging and you want a way for authors using your blog to give and receive feedback about your writing. There is an additional many-to-many relationship that can be implemented to accomplish this. Let's start by mapping out that relationship. 

![Bidirectional has_many_through relationship](https://imgur.com/F6054XB.jpg)

So looking at this chart, we have an author, a blog, and finally comments. An author can `has_many` comments and a blog can `has_many` comments too. This enables an author to make comments on any blog s/he wants and for the relationship with that blog to be conveyed through the comments which serves as the join table. Essentially this means that an author `has_many :blogs through: :comments` and a blog `has_many :authors through: :comments`. For this relationship, your migrations are set up in much the same way, but you must ensure that your comments- or whatever is serving as the join- has not only it's own id, but a foreign key for both models it belongs_to. Your schema might look something like this:
```
ActiveRecord::Schema.define(version: 2018_07_15_020021) do

  create_table "author", force: :cascade do |t|
    t.string "name"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end 

create_table "blog", force: :cascade do |t|
   t.string "title"
   t.datetime "created_at", null: false
   t.datetime "updated_at", null: false
end 

create_table "comments", force: :cascade do |t|
   t.string "comment_text"
	 t.integer "author_id"
	 t.integer "blog_id"
	 t.datetime "created_at", null: false
	 t.datetime "updated_at", null: false
end 
```

And to be thorough, let's break this down in our models:

```
class Author < ApplicationRecord
  has_many :comments
	has_many :blogs, through: :comments
end 

class Blog < ApplicationRecord
	has_many :comments
	has_many :authors, through: :comments
end 

class Comments < ApplicationRecord
	belongs_to :blog
	belongs_to :author
end 
```

Now this is a relationship that I feel is less common and practical in the way of real-life examples and applications you would use it in. Maybe some day after you've learned ALOT more dev, you are managing a bank's website- this `has_many` relationship could apply to the bank- an account serving as the join between the banking institution and the banking institution `has_many` users through their accounts. The docs (link below) include the example of appointments serving as a join between physicians and patients. Another example could be a work-out routine whereby the exercises serve as the join and belong to a user and a routine- the user `has_many` routines and `has_many` individual exercises through those routines which woud mean that a routine `has_many` exercises and `has_many` users through their exercises. Admittedly, I found illustrating practical examples for this type of `many_to_many` association a bit more difficult.  


 If you're still struggling with associations, check out the [docs](http://guides.rubyonrails.org/association_basics.html) for more information.
