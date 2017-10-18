Bootstrapping without Reseed Servers
==============================================

In some cases I2P's default reseed servers (servers used to fill I2P router's netdb with initial peers) are blocked.

i2pd has a unique feature that allows it to bootstrap off of any I2P router that is participating in the DHT, they are called floodfill routers and have the router capacity `f` in their router info.

## How To

* obtain a `router.info` file of a floodfill router out of band, save to `/tmp/floodfill.router.info` or some other path
* run `i2pd --reseed.floodfill=/tmp/floodfill.router.info` and if that router is online you'll be able to bootstrap into the network from just that routers

## Caveats

* The floodfill *must* be trustworthy, it could give you all colluding peers if it's a baddie.
* *DO NOT* use a random floodfill unless you don't care about high security and just want to test out this feature.
* Java I2P routers seem to dislike this feature (sometimes) and may back off exponentially
