# Flynn Multi Host Dev Environment

Tweaking the flynn-dev Vagrant setup for bare metal multi host deployment.

### Setup

After checking out this repo:

```text
cd flynn-multi-host
make
```

### Usage

With the Flynn processes running

```text

cd nodejs-example

git push flynn master
```

If the deploy is successful, the example application should have one instance
running which will be running a HTTP server:

```text
curl http://:55000
```

The `flynn` command line tool is used to manipulate the application.

#### Scale

To test out the router and scaling, turn up the web processes and add a domain:

```text
flynn scale web=3

flynn domain example.com
```

The application will now be accessible via the router:

```text
curl -H "Host: example.com" localhost:8080
```

Repeated requests to the router should show that the requests are load balanced
across the running processes.

#### Logs

`flynn ps` will show the running processes. To get the logs from a process, use
`flynn logs`:

```text
flynn logs web.1
```

#### Run

An interactive one-off process may be spawned in a container:

```text
flynn run bash
```
