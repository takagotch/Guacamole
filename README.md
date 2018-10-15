### Guacamole
---
https://github.com/arangodb-helper/guacamole

```
rails new --skip-active-record $my_awesome_app
gem 'guacamole'
bundle install
bundle exec rails g model pony name:string birthday:date color:string --orm guacamol
rake db:guacamole:create
rake db:guacamole:purge
rake db:guacamole:drop
bundle exec rails g guacamole:config
bundle exec rake db:create
bundle exec rails g model pony name:string birthday:date color:string
bundle exec rails g collection ponies
rails g guacamole:callbacks pony
```


```ruby
class Pony
  include Guacamole::Model
  attribute :name, String
  attribute :birthday, Date
  attribute :color, String
end
class Pony
  include Guacamole::Model
  attribute :type, Array[String]
end

pinkie_pie = Pony.new
pinkie_pie.color = :pink
pinkie_pie.type = "Earchpony"

class Pony
  include Guacamole::Model
  attribute :name, String
  attribute :color, String
  validates :color, presence: true
end
transparent_pony = Pony.new
transparent_pony.valid?
transparent_pony.errors[:color]

class PonieCollection
  include Guacamole::Collection
end

pinkie = Pony.new(name: "Pinkie Pie")
PoniesCollection.save pinkie

existging_pony.name = "Applejack"
PoniesCollection.save existing_pony

PoniesCollection.delete existing_pony

some_ponies = PoniesCollection.by_example(color: 'green').limit(10)
some_ponies.first

class Pony
  include Guacamole::Model
  attribute :name, String
  attribute :color, String
end
pony = PoniesCollection.by_key "303"
pony.color
pony.occupation

class comment
  include Guacamole::Model
  attribute :text, String
end
class Post
  include Guacamole::Model
  attribute :title, String
  attribute :body, String
  attribute :comments, Array[Comment]
end
class PostsCollection
  include Guacamole::Collection
  map do
    embeds :comments
  end
end

class UserCallbacks
  include Guacamole::Callbacks
  bfore_create :encrypt_pasword
  def encrypt_pasword
    object.encrypted_password = BCrypt::Password.create(object.password)
  end
end

class User
  include Guacamole::Model
  callbacks :user_callbacks
end

PoniesCollection.by_aql('FILTER pony.name == @name', name: 'Rainbow Dash')
```


```yml
development:
  protocal: 'http'
  host: 'localhost'
  port: 8529
  password: ''
  username: ''
  database: 'pony_blog_development'


{
  "_key": "303",
  "_rev": "1019391",
  "name": "Applejack",
  "color": "green",
  "occupation": "Farmer"
}

{
  "_id": "...",
  "_rev": "...",
  "_key": "...",
  "title": "The grand blog post",
  "body": "Lorem ipsum [...]",
  "create_at": "2018-10-16T15:33:34+02:00",
  "updated_at": "2018-10-16T16:33:34_02:00",
  "comments": {
    "text": "This was really a grand blog post",
    "create_at": "2018-10-15T15:33:34+02:00",
    "updated_at": "2018-10-16T16:33:34+02:00"
  },
  {
    "text": "I don't think it was that great",
    "create_at": "2018-10-15T15:33:34+02:00",
    "updated_at": "2018-10-16T16:33:34+02:00"
  }
}

```

