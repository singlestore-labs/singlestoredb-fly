# SingleStoreDB on Fly.io

This project contains everything you need to run [SingleStoreDB] on [Fly.io] for development. This deployment is **not supported for production workloads or benchmarks** so please keep that in mind when using it. Internally, this project uses the [singlestoredb-dev-image], please see the documentation for that project if you want to customize the deployment.

If you have any questions or issues, please file an issue on the [GitHub repo][gh-issues] or our [forums].

## Quick Start

Before you can run this application you will need to get a free SingleStore License key. [Sign up for a SingleStore account][signup] and then grab your license key from the [customer portal] to use below.

You will also need to [install flyctl] and [sign up][fly signup] for a [Fly.io] account before continuing.

Next, follow these steps to deploy [SingleStoreDB] on your [Fly.io] account:

```bash
git clone https://github.com/singlestore-labs/singlestoredb-fly
cd singlestoredb-fly

# initialize the application on your Fly.io account
flyctl launch --copy-config --no-deploy

# decide what size app to launch
# see sizes here: https://fly.io/docs/about/pricing/#virtual-machines
# dedicated-cpu-1x is minimum recommended size
flyctl scale vm dedicated-cpu-1x

# set your SingleStoreDB license key and root password like so:
flyctl secrets set SINGLESTORE_LICENSE="YOUR LICENSE KEY" ROOT_PASSWORD="SINGLESTORE PASSWORD"

# deploy the fly application
flyctl deploy

# check the logs
flyctl logs

# check the app status
flyctl status
```

## Connect to SingleStoreDB

Once [SingleStoreDB] is running in [Fly.io], you can connect to it using either the app IP or hostname. You can retrieve the app IP using `flyctl ips list` or open up the Studio console using `flyctl open`.

> **Note**
> The Fly.io hostname (looks like `app-name.fly.dev`) can take a couple minutes to resolve, so if it doesn't work right away just use the IP address for now.

Once you have either the hostname or the IP, you can also run a local mysql shell like so:

```bash
mysql -u root -h <fly app ip> -p
```

The [Data API][data-api] can also be accessed over HTTPS on port 9000 using your app hostname (`app-name.fly.dev`) like so:

```bash
~ ➜ curl -s -XPOST -H "content-type: application/json" -d '{ "sql": "select 1" }' root:YOUR_ROOT_PASSWORD@APP_NAME.fly.dev:9000/api/v1/query/rows
{
  "results": [
    {
      "rows": [ { "1": 1 } ]
    }
  ]
}
```

> **Note**
> For more information on how to use the Data API please [visit the documentation.][data-api]
> 
## Where can I learn how to use SingleStoreDB?

Now that you have SingleStore running, please check out the following sections of our official documentation for guides on what to do next.

 * [Connect to SingleStore](https://docs.singlestore.com/db/latest/en/connect-to-your-cluster.html)
 * [Developer Resources](https://docs.singlestore.com/db/latest/en/developer-resources.html)
 * [Integrations](https://docs.singlestore.com/db/latest/en/integrate-with-singlestoredb.html)
 * [Load Data](https://docs.singlestore.com/db/latest/en/load-data.html)

[singlestoredb-dev-image]: https://github.com/singlestore-labs/singlestoredb-dev-image
[Fly.io]: https://fly.io
[SingleStoreDB]: https://www.singlestore.com
[gh-issues]: https://github.com/singlestore-labs/singlestoredb-fly/issues
[forums]: https://www.singlestore.com/forum/
[signup]: https://www.singlestore.com/cloud-trial/
[customer portal]: https://portal.memsql.com/
[install flyctl]: https://fly.io/docs/hands-on/install-flyctl/
[fly signup]: https://fly.io/docs/hands-on/sign-up/
[data-api]: https://docs.singlestore.com/managed-service/en/reference/data-api.html