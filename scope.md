# Scope

> são consultas comumente usadas que podem ser referenciadas como chamadas de método nos objetos ou em modelos de associações. 

São consultas ao banco feita por meio de código __Rails__. Como pode ver a seguir:

```ruby
class Article < ApplicationRecord
    scope :published, -> { where(published: true)}
end

# pode ser escrita da mesma maneira que:

class Article < ApplicationRecord
    def self.published
        where(published: true)
    end
end
```

você também consegue fazer pesquisas __aninhadas__ o que torna interessante para a organização do código:

```ruby
class Article < ApplicationRecord
    belongs_to :user

    # scope para inner join com user
    scope :user_join, -> {
        join(:user)
    }

    scope :published, -> { 
        where(published: true)
    }
    
    scope :order, -> { 
        order(title: :asc)
    }
end

class User < ApplicationRecord
    has_many :articless
end 
```

você poderá usar da seguinta forma:

```ruby
Article.user_join.published.ordered_by_title
```