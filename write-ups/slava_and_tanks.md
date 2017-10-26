# Slava and Tanks

## [Problem Statement][1]:
```
Slava plays his favorite game "Peace Lightning". Now he is flying a
bomber on a very specific map.

Formally, map is a checkered field of size 1 × n, the cells of which
are numbered from 1 to n, in each cell there can be one or several
tanks. Slava doesn't know the number of tanks and their positions,
because he flies very high, but he can drop a bomb in any cell. All
tanks in this cell will be damaged.

If a tank takes damage for the first time, it instantly moves to one
of the neighboring cells (a tank in the cell n can only move to the
cell n - 1, a tank in the cell 1 can only move to the cell 2). If a
tank takes damage for the second time, it's counted as destroyed and
never moves again. The tanks move only when they are damaged for the
first time, they do not move by themselves.

Help Slava to destroy all tanks using as few bombs as possible.
```
## [Solution][2]:
```python
def min_num_bombs(map_size):
  """This function returns the minimum number of bombings as well as
  the corresponding cell sequence that Slava needs to in order to
  destroy all the tanks on a map of given size.

  Time Complexity: O(map_size)
  Space Complexity: O(map_size)
  """
  # We need to make 3 sweeps. In the first sweep, we bomb all the
  # even cells, this forces all the tanks into odd cells. We then
  # bomb all the odd cells, destroying all the tanks which were hit
  # in the first sweep while moving all the remaining tanks into
  # even cells. WE now do our final sweep by dropping bombs in all
  # the even cells, destroying all the remaining tanks.
  #
  # Why did we need to drop bombs on the even cells first? Our choice
  # of which cells to bomb first, even or odd, determines which
  # cells, odd or even, we bomb in the last sweep. If the map size is
  # even, there will be as many odd cells as there are even cells.
  # On the other hand, if the map size is odd, there will be fewer
  # even cells. Therefore, we want our final sweep to hit all the
  # even cells in order to minimize bombings.
  #
  # Why is this optimal? Let's think about it this way, suppose we
  # have a map of size 2. In order to destroy all the tanks, we must
  # drop bombs at least 3 times (you should be able to convince
  # yourself of this). Knowing this, we can break larger maps into
  # many smaller maps of size 2; if the map size is even, we have
  # n/2 maps, of size 2, each of which require at least 3 bomb
  # drops. Otherwise, the map size is odd and, therefore, we have
  # (n-1)/2 maps of size 2 plus 1 map of size 1 which need 3 and 1
  # bombings, respectively.
  num_even_cells = map_size/2
  num_bombs = map_size + num_even_cells

  even_cells = range(2, map_size+1, 2)
  odd_cel1s = range(1, map_size+1, 2)
  cell_sequence = []
  for sweep in [even_cells, odd_cel1s, even_cells]:
    cell_sequence.extend(sweep)

  return num_bombs, cell_sequence


map_size = int(raw_input())
num_bombs, cell_sequence = min_num_bombs(map_size)
print num_bombs
print ' '.join(map(str, cell_sequence))
```


[1]: http://codeforces.com/contest/877/problem/C
[2]: http://codeforces.com/blog/entry/55362
