# Blair Nums
Base:

blair num of 1 = 1

blair num of 2 = 2

```ruby
...
@blair_cache = { 1 => 1, 2 => 2 }
...

def blair_nums(n)
  return @blair_cache[n] if @blair_cache[n]
  odd_num = 2 * (n-1) - 1
  @blair_cache[n] = blair_nums(n-1) + blair_nums(n-2) + odd_num
end
```

# Frog Hops

Base:

0 steps = [[]]

1 step = [[1]]

2 steps = [[1,1], [2]]

3 steps = [[1,1,1], [1,2], [2,1], [3]]

```ruby
# n = number of steps
def frog_hops_bottom_up(n)
  frog_cache_builder(n)[n]
end

def frog_cache_builder(n)
  ways_collection = [[[]], [[1]], [[1,1], [2]]]
  return ways_collection if n < 3

  (3..n).each do |i|
    new_way_set = []

    (1..3).each do |first_step|
      ways_collection[i - first_step].each do |way|
        new_way = [first_step]

        way.each do |step|
          new_way << step
        end

        new_way_set << new_way
      end
    end

    ways_collection << new_way_set
  end

  ways_collection
end
```