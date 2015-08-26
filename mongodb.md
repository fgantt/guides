https://www.mongodb.org/
[Robomongo shell](http://robomongo.org/)

Mongo Apps
=================
mongod - server process

mongo - JavaScript shell

mongos - Routing server

mongodump / mongorestore - native BSON backup

mongoexport / mongoimport - JSON, CSV, TSV

mongosniff - wire sniffing tool

mongostat - polls status of mongod or mongos

bsondump - convert BSON files to human-readable

mongofiles - manipulate files stored in your MongoDB instance in GridFS objects

mongotop -

mongoperf - 

mongooplog -

OS X install with Homebrew
==========================
```
brew update

$ brew install mongodb
==> Downloading https://homebrew.bintray.com/bottles/mongodb-3.0.5.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring mongodb-3.0.5.yosemite.bottle.tar.gz
==> Caveats
To have launchd start mongodb at login:
  ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
Then to load mongodb now:
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
Or, if you don't want/need launchctl, you can just run:
  mongod --config /usr/local/etc/mongod.conf
==> Summary
🍺  /usr/local/Cellar/mongodb/3.0.5: 17 files, 154M
```

