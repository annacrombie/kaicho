# Kaicho

Kaicho is the boss for your resources.  It handles keeping everything up to
date.

```ruby
class Fruits
  include Kaicho

  def intialize
    def_resource :apples, accessor: :both { @apples || 0 }
    def_resource :oranges, accessor: :both { @oranges || 0 }
    def_resource :total, depend: { apples: :fail, oranges: :fail } do
      puts "computing total"
      @apples + @oranges
    end
  end
end

f = Fruits.new
f.apples         #=> 0
f.apples += 1    #=> 1
computing total
f.oranges = 10   #=> 10
computing total
f.total          #=> 11
f.oranges = 2
computing total
f.total          #=> 13
f.total          #=> 13
```