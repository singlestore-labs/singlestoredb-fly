# SingleStoreDB on Fly.io

This project contains everything you need to run [SingleStoreDB] on [Fly.io] for development. This deployment is **not supported for production workloads or benchmarks** so please keep that in mind when using it. Internally, this project uses the [singlestoredb-dev-image], please see the documentation for that project if you want to customize the deployment.

If you have any questions or issues, please file an issue on the [GitHub repo][gh-issues] or our [forums].

You can run this template project on your [Fly.io] account like so:

```bash
git clone https://github.com/singlestore-labs/singlestoredb-fly
cd singlestoredb-fly

# initialize the application in your fly account
fly launch --copy-config --no-deploy

# decide what size app to launch
# see sizes here: https://fly.io/docs/about/pricing/#virtual-machines
# dedicated-cpu-1x is minimum recommended size
flyctl scale vm dedicated-cpu-1x

# set your singlestoredb license key and root password like so:
flyctl secrets set SINGLESTORE_LICENSE="YOUR LICENSE KEY" ROOT_PASSWORD="SINGLESTORE PASSWORD"

# deploy singlestoredb-dev
flyctl deploy

# check the logs
flyctl logs
```

## Connect to SingleStoreDB

Once [SingleStoreDB] is running in [Fly.io], you can connect to it using either the app IP or hostname. You can retrieve the app IP using `flyctl ips list` or open up the Studio console using `flyctl open`.

> **Note**
> The Fly.io hostname (looks like `app-name.fly.dev`) can take a couple minutes to resolve, so if it doesn't work right away just use the IP address for now.

Once you have either the hostname or the IP, you can also run a local mysql shell like so:

```bash
mysql -u root -h <fly app ip> -p
```

[singlestoredb-dev-image]: https://github.com/singlestore-labs/singlestoredb-dev-image
[Fly.io]: https://fly.io
[SingleStoreDB]: https://www.singlestore.com
[gh-issues]: https://github.com/singlestore-labs/singlestoredb-fly/issues
[forums]: https://www.singlestore.com/forum/