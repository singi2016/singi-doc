# sql

## count(*) vs count(val)

优化器里的算法是这么的，列的偏移量决定性能，列越靠后，访问的开销越大。由于count(*)的算法与列偏移量无关，所以count(*)最快，count(最后列val)最慢

> count(1) vs count(*),两者完全一样