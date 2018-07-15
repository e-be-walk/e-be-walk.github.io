---
layout: post
title:      "Many-to-many, too many."
date:       2018-07-15 17:10:15 +0000
permalink:  many-to-many_too_many
---


It’s not hard to visualize and demonstrate most model relationships. Most relationships can be easily visualized with books. For instance, `belongs_to` and `has_many` is easy- an author has_many books and a book belongs to an author. Let’s say a book is published- chances are, the book only `has_one` publisher, right? These relationships can be easily defined with a foreign key in the corresponding table- in this case, a book would have a foreign key for to identify the author and an additional foreign key to identify the publisher.

Establishing and visualizing a many-to-many relationship is a little bit tougher. The `has_many_through` relationship gets a little abstract and it can not only be harder to identify these relationships but also to implement ensuring that your table has a correct key. So what is a many-to-many relationship? In trying to figure one out that applies to books, I had to meander a little bit and think outside the box. We’ve got this sculpture at work which demonstrates it quite well- one sculpture, `has_many` alligator heads, and many alligator heads `has_many` teeth. Many teeth `belongs_to` one alligator and many alligators `belongs_to`  one sculpture. Many teeth! Many alligator heads! ONE sculpture.

![](https://imgur.com/a/NfVXVqf)

So going back to our books, it could be said that an author has many chapters through their books. And just to be safe, let’s assume we’re talking about a prolific author- like Stephen King or Tolstoy or something- not a one hit wonder like J.D. Salinger. So one author `has_many` books, the author also `has_many` chapters `through` each of their books. So far, so good, right? If we were to map this out, it would look something like this: 

![](https://imgur.com/a/PszCD4Y)

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
	has_many :chapters, through: books
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

With that, you’ll be able to start working on all the CRUD driving the controller actions and views enabling an author to add their books, chapters, and and publisher. As always, check out the [docs](http://guides.rubyonrails.org/association_basics.html) for more information.
