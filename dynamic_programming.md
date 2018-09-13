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