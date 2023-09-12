
## Mongo Backup & Restore

This is a minimal custom Docker image used to backup Mongo from within a Kubernetes cronJob.

### Usage

1. Create a Kubernetes cronJob definition that loads this image
1. Create configMap to load needed env variables
1. Set the `command` and `args` to run a command similar to:

```yaml
            command: ["sh", "-c"]
            args:
              - mongodump --host=$MONGODB_URL --port=27017 -u $MONGO_INITDB_ROOT_USERNAME -p $MONGO_INITDB_ROOT_PASSWORD --readPreference=secondaryPreferred --gzip --archive=/$BACKUP_PATH/$CLUSTER-$(date +%Y-%m-%d).tar.gz
            envFrom:
              - configMapRef:
                  name: mongo-env-conf
```
