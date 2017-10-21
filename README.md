# openwhisk-prototyping
Prototyping OpenWisk deployment and examples

Setup your CLI/Bash Shell (make sure openwhisk is current OpenShift Project):

AUTH_SECRET=$(oc get secret openwhisk -o yaml | grep "system:" | awk '{print $2}' | base64 --decode)
wsk property set --auth $AUTH_SECRET --apihost $(oc get route/openwhisk --template={{.spec.host}})

Smoke Test:

wsk -i list
wsk -i action invoke /whisk.system/utils/echo -p message hello -b

Output from "hello message" test:


[keyvan@ocp-master ~]$ wsk -i action invoke /whisk.system/utils/echo -p message hello -b
ok: invoked /whisk.system/utils/echo with id db46e0ef0a704c5586e0ef0a709c559d
[source,json]
----
{
    "activationId": "db46e0ef0a704c5586e0ef0a709c559d",
    "annotations": [
        {
            "key": "limits",
            "value": {
                "logs": 10,
                "memory": 256,
                "timeout": 60000
            }
        },
        {
            "key": "path",
            "value": "whisk.system/utils/echo"
        }
    ],
    "duration": 432,
    "end": 1508534954547,
    "logs": [],
    "name": "echo",
    "namespace": "whisk.system",
    "publish": false,
    "response": {
        "result": {
            "message": "hello"
        },
        "status": "success",
        "success": true
    },
    "start": 1508534954115,
    "subject": "whisk.system",
    "version": "0.0.1"
}
----
