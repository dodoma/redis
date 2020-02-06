### ml's Redis fork with following changes made on official unstable branch.

* server side lua with dlopen enable.

* server side lua with os lib enable.

* change sort set to an collections of ~~unique~~, sorted string elements. (working in progress)

  - Add 'ax' parameter to *ZADD* command.

    + ZADD without 'ax' parameter works same as official redis.

    + ZADD with 'ax' parameter will create a new member with the new score, if the element already exist.

    + *ZRANGEBYSCORE* *ZREVRANGEBYSCORE* *ZRANGEBYLEX* *ZREVRANGEBYLEX* return list not guaranteed to be
      member uniqued (MAY contain duplicate elements), if this set ADDED some element multipile times
      with 'ax' parameter.'

## use it as you own risk!

[ORIGINAL README](README-ORI.md)
