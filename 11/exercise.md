Description: There's an etcd server running on https://localhost:2379 , get the value for the key "foo", ie etcdctl get foo or curl https://localhost:2379/v2/keys/foo

Test: etcdctl get foo returns bar.
