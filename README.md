### ml's Redis fork with following changes made on official unstable branch.

* server side lua with dlopen enable.

* server side lua with os lib enable.

* change sorted set to an collections of ~~unique~~, sorted string elements.

  - Add 'ax' parameter to *ZADD* command.

    + ZADD without 'ax' parameter works same as official redis.

    + ZADD with 'ax' parameter will create a new member with the new score,
      if the element already exist. with the following side effect:

      * count

        - ZCARD     different score and element count in all set
        - ZCOUNT    different score and element count in score range
        - ZLEXCOUNT different score and element count in lex range

      * return list not guaranteed to be member uniqued
        (MAY contain duplicate elements).

        - ZRANGE
        - ZRANGEBYLEX
        - ZRANGEBYSCORE
        - ZREVRANGE
        - ZREVRANGEBYLEX
        - ZREVRANGEBYSCORE

      * return the min or max match member rank in skiplist.
      * return the min rank on ziplist

        - ZRANK
        - ZREVRANK

      * remove all matched elements(not just first or last one).

        - BZPOPMAX
        - BZPOPMIN
        - ZPOPMAX
        - ZPOPMIN

      * remove all matched elements(not just the matched one).

        - ZREM
        - ZREMRANGEBYLEX
        - ZREMRANGEBYRANK
        - ZREMRANGEBYSCORE

      * intersection, union operation use the element first score

        - ZINTERSTORE
        - ZUNIONSTORE

      * operate only on the element first added score
        (like ZADD with 'ax' take no effect)

        - ZSCAN
        - ZINCRBY
        - ZSCORE return the min score on ziplist

  - useage

  ![demonstrate useage](/demo.gif?raw=true "usage")

### TODO

Other zset commands also need 'ax' like parameter to perform special operation not
just ZADD.

## use it as you own risk!

[ORIGINAL README](README-ORI.md)
