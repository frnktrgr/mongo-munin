# Munin Plugins for MongoDB

Forked from https://github.com/comerford/mongo-munin.

Thanks to Adam Comerford. Changes: Removed broken plugins for MongoDB 3.2+

# Provided Munin Plugins

* mongo_ops   : operations/second
* mongo_mem   : mapped, virtual and resident memory usage
* mongo_conn  : current connections
* mongo_docs  : number of documents (inserted, updated...)

# Requirements
* MongoDB 3.2+ (tested with 3.2)
* python/pymongo

## Install python pymongo

### Ubuntu

```bash
sudo apt-get install -y python-pymongo
```

## Install plugins
```bash
git clone https://github.com/frnktrgr/mongo-munin.git /tmp/mongo-munin
sudo cp /tmp/mongo-munin/mongo_* /usr/share/munin/plugins
sudo ln -sf /usr/share/munin/plugins/mongo_conn /etc/munin/plugins/mongo_conn
sudo ln -sf /usr/share/munin/plugins/mongo_docs /etc/munin/plugins/mongo_docs
sudo ln -sf /usr/share/munin/plugins/mongo_mem /etc/munin/plugins/mongo_mem
sudo ln -sf /usr/share/munin/plugins/mongo_ops /etc/munin/plugins/mongo_ops
sudo chmod +x /usr/share/munin/plugins/mongo_*
sudo systemctl restart munin-node.service
```

Check if plugins are running:
```bash
munin-node-configure | grep "mongo_"
```

Test plugin output:
```bash
munin-run mongo_conn
munin-run mongo_docs
munin-run mongo_mem
munin-run mongo_ops

```

## Configuration

Add connection URI to `/etc/munin/plugin-conf.d/munin-node`:
```
[mongo_*]
env.MONGO_DB_URI mongodb://user:password@host:port/dbname
```

