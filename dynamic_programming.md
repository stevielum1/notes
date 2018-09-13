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

```ruby
...
@froggy_cache = [[[]], [[1]], [[1,1], [2]]]
...

def frog_hops_top_down(n)
  frog_hops_top_down_helper(n)
end

def frog_hops_top_down_helper(n)
  return @froggy_cache[n] if @froggy_cache[n]
  
  new_way_set = []

  (1..3).each do |first_step|
    frog_hops_top_down_helper(n-first_step).each do |way|
      new_way = [first_step]

      way.each do |step|
        new_way << step
      end

      new_way_set << new_way
    end
  end

  @froggy_cache[n] = new_way_set
end
```

# Super Frog Hops

```ruby
def super_frog_hops(n, k)
  ways_collection = [[[]], [[1]]]
  return ways_collection[n] if n < 2

  (2..n).each do |i|
    new_way_set = []

    (1..k).each do |first_step|
      break if i - first_step < 0
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

# Knapsack Problem
Capacity = 6
| Weight | Value | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|--------|-------|---|---|---|---|---|---|---|
| 1      | 1     | 0 | 1 | 1 | 1 | 1 | 1 | 1 |
| 2      | 3     | 0 | 1 | 3 | 4 | 4 | 4 | 4 | 
| 4      | 6     | 0 | 1 | 3 | 4 | 6 | 7 | 9 |

```ruby
def knapsack(weights, values, capacity)
  return 0 if capacity == 0 || weights.length == 0
  solution_table = knapsack_table(weights, values, capacity)
  solution_table[capacity][-1]
end

def knapsack_table(weights, values, capacity)
  solution_table = []

  (0..capacity).each do |i|
    solution_table[i] = []

    (0...weights.length).each do |j|
      if i == 0
        solution_table[i][j] = 0
      elsif j == 0
        solution_table[i][j] = i < weights[0] ? 0 : values[0]
      else
        option1 = solution_table[i][j - 1]
        option2 = i < weights[j] ? 0 : solution_table[i - weights[j]][j-1] + values[j]
        optimum = [option1, option2].max
        solution_table[i][j] = optimum
      end
    end
  end

  solution_table
end
```