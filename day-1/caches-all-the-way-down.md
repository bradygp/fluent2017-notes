# Caches All the Way Down
Yoav Welss @yaovwels

2 hard things in CS
  * naming things
  * cache invalidation

Eviction - the resources you put in the cache are more valueable than the resources you are throwing out.
Fresh - play it safe and revalidate the data even when you do not have to.

cache can hold an image/css/js, or any other type of resource.
First place to look for metric resources is `MemoryCache` it is part of the render.Once the user clicks away, that cache is destroyed

https://calendar.perfplanet.com/2016/a-tale-of-four-caches/

Service Workers can be unpredictable (from a request perspective)
HTTP Cache - extremly strict. Persistanct cache storage, slower but can be used for later navigation. (stored on disk)
H2 Push Cache - different browsers have different rules. (like different storage amounts, or duration of stay in cache)
Network Caches can be very unpredicatable because packets can be corrupted or lost or have a widely varying latency
  It goes from the the User -> ISP -> Edge -> Internet -> Reverse Proxy -> Origin


if we request the same URL twice, the first once is cached and the second one uses the cache.
cache-control: max-age=3600 
304 not modified
scope - `cache:control:private` can only be cached in the browser, public can be in an public spaces.
`cache-control:no-cache=set-cookie`
`cache-control:no-store` will not store the resource on disk
`Age:` - indidcates the time that has pased since the last revalidation ( used to help calculate max age)
mmutable cache-control would be good for things like logo

