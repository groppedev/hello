## Hello, OpenShift for Developers! ##
This is a example that will serve an HTTP response of "Hello OpenShift for Developers!" written in Golang. It is also
intended to be build and used with the [Golang Source-to-Image builder image](https://github.com/sclorg/golang-container).  This builder image is included in current versions of OpenShift (4.7 at the time).

### Deploying on OpenShift
You can deploy this application on OpenShift using the following command:

```shell
oc new-app golang~https://github.com/groppedev/hello --name=s2i-go-v1 -l app=s2i-go-v1
```

Note: this example app is derived from the [example at sclorg/golang-ex](https://github.com/sclorg/golang-ex).

The response message can be set by using the RESPONSE environment
variable.  You will need to edit the pod definition and add an
environment variable to the container definition and run the new pod.

    $ curl locahost:8080
     Hello OpenShift for Developers!
     
    $ curl http://s2i-go-v1:8080
     Hello OpenShift for Developers!

To test from external network, you need to create router.

The container doesn't expose any ports, this will require you to expose it manually.
For example:

    $ oc expose dc/s2i-go-v1 --port=8080

and lastly if you want to expose a route, by doing:

    $ oc expose service/s2i-go-v1
