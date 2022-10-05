# SingleStoreDB on Fly.io

This project contains everything you need to run the singlestoredb-dev-image on fly.io for development.

You can run this template project like so:

```bash
git clone https://github.com/singlestore-labs/singlestoredb-fly
cd singlestoredb-fly

# you can customize the fly app name like so:
flyctl config save -a <your-singlestoredb-app-name>

flyctl deploy
```

[singlestoredb-dev-image]: https://github.com/singlestore-labs/singlestoredb-dev-image