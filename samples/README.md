# Sample apps for the AWS IoT Device SDK v2 for Python

* [MQTT5 PubSub](#mqtt5-pubsub)
* [PubSub](#pubsub)
* [Basic Connect](#basic-connect)
* [Websocket Connect](#websocket-connect)
* [PKCS#11 Connect](#pkcs11-connect)
* [Windows Certificate Connect](#windows-certificate-connect)
* [Custom Authorizer Connect](#custom-authorizer-connect)
* [Shadow](#shadow)
* [Jobs](#jobs)
* [Fleet Provisioning](#fleet-provisioning)
* [Greengrass Discovery](#greengrass-discovery)

## Build instructions

First, install the aws-iot-devices-sdk-python-v2 with following the instructions from [Installation](../README.md#Installation).

Then change into the samples directory to run the Python commands to execute the samples. You can view the commands of a sample like this:

``` sh
# For Windows: replace 'python3' with 'python'
python3 pubsub.py --help
```

## MQTT5 PubSub
This sample uses the
[Message Broker](https://docs.aws.amazon.com/iot/latest/developerguide/iot-message-broker.html)
for AWS IoT to send and receive messages
through an MQTT5 connection.

MQTT5 introduces additional features and enhancements that improve the development experience with MQTT. You can read more about MQTT5 in the Python V2 SDK by checking out the [MQTT5 user guide](../documents/MQTT5.md).

Note: MQTT5 support is currently in **developer preview**. We encourage feedback at all times, but feedback during the preview window is especially valuable in shaping the final product. During the preview period we may make backwards-incompatible changes to the public API, but in general, this is something we will try our best to avoid.

On startup, the device connects to the server,
subscribes to a topic, and begins publishing messages to that topic.
The device should receive those same messages back from the message broker,
since it is subscribed to that same topic.
Status updates are continually printed to the console.

Source: `samples/mqtt5_pubsub.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect, subscribe, publish, and receive. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Publish",
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/test/topic"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Subscribe"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/test/topic"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 mqtt5_pubsub.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file>
```

## PubSub

This sample uses the
[Message Broker](https://docs.aws.amazon.com/iot/latest/developerguide/iot-message-broker.html)
for AWS IoT to send and receive messages
through an MQTT connection. On startup, the device connects to the server,
subscribes to a topic, and begins publishing messages to that topic.
The device should receive those same messages back from the message broker,
since it is subscribed to that same topic.
Status updates are continually printed to the console.

Source: `samples/pubsub.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect, subscribe, publish, and receive. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Publish",
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/test/topic"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Subscribe"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/test/topic"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 pubsub.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file>
```

## Basic Connect

This sample makes an MQTT connection using a certificate and key file. On startup, the device connects to the server using the certificate and key files, and then disconnects.
This sample is for reference on connecting via certificate and key files.

Source: `samples/basic_connect.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 basic_connect.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file>
```

## Websocket Connect

This sample makes an MQTT connection via websockets and then disconnects. On startup, the device connects to the server via websockets and then disconnects.
This sample is for reference on connecting via websockets.

Source: `samples/websocket_connect.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 websocket_connect.py --endpoint <endpoint> --ca_file <file> --signing_region <signing region>
```

Note that using Websockets will attempt to fetch the AWS credentials from your enviornment variables or local files. See the [authorizing direct AWS](https://docs.aws.amazon.com/iot/latest/developerguide/authorizing-direct-aws.html) page for documentation on how to get the AWS credentials, which then you can set to the `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS`, and `AWS_SESSION_TOKEN` environment variables.

## PKCS#11 Connect

This sample is similar to the [Basic Connect](#basic-connect),
but the private key for mutual TLS is stored on a PKCS#11 compatible smart card or Hardware Security Module (HSM)

WARNING: Unix only. Currently, TLS integration with PKCS#11 is only available on Unix devices.

source: `samples/pkcs11_connect.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

To run this sample using [SoftHSM2](https://www.opendnssec.org/softhsm/) as the PKCS#11 device:

1)  Create an IoT Thing with a certificate and key if you haven't already.

2)  Convert the private key into PKCS#8 format
    ```sh
    openssl pkcs8 -topk8 -in <private.pem.key> -out <private.p8.key> -nocrypt
    ```

3)  Install [SoftHSM2](https://www.opendnssec.org/softhsm/):
    ```sh
    sudo apt install softhsm
    ```

    Check that it's working:
    ```sh
    softhsm2-util --show-slots
    ```

    If this spits out an error message, create a config file:
    *   Default location: `~/.config/softhsm2/softhsm2.conf`
    *   This file must specify token dir, default value is:
        ```
        directories.tokendir = /usr/local/var/lib/softhsm/tokens/
        ```

4)  Create token and import private key.

    You can use any values for the labels, PINs, etc
    ```sh
    softhsm2-util --init-token --free --label <token-label> --pin <user-pin> --so-pin <so-pin>
    ```

    Note which slot the token ended up in

    ```sh
    softhsm2-util --import <private.p8.key> --slot <slot-with-token> --label <key-label> --id <hex-chars> --pin <user-pin>
    ```

5)  Now you can run the sample:
    ```sh
    # For Windows: replace 'python3' with 'python'
    python3 pkcs11_connect.py --endpoint <endpoint> --ca_file <path to root CA> --cert <path to certificate> --pkcs11_lib <path to PKCS11 lib> --pin <user-pin> --token_label <token-label> --key_label <key-label>
    ```

## Windows Certificate Connect

WARNING: Windows only

This sample is similar to the basic [Connect](#basic-connect),
but your certificate and private key are in a
[Windows certificate store](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/certificate-stores),
rather than simply being files on disk.

To run this sample you need the path to your certificate in the store,
which will look something like:
"CurrentUser\My\A11F8A9B5DF5B98BA3508FBCA575D09570E0D2C6"
(where "CurrentUser\My" is the store and "A11F8A9B5DF5B98BA3508FBCA575D09570E0D2C6" is the certificate's thumbprint)

If your certificate and private key are in a
[TPM](https://docs.microsoft.com/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview),,
you would use them by passing their certificate store path.

source: `samples/windows_cert_connect.py`

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

To run this sample with a basic certificate from AWS IoT Core:

1)  Create an IoT Thing with a certificate and key if you haven't already.

2)  Combine the certificate and private key into a single .pfx file.

    You will be prompted for a password while creating this file. Remember it for the next step.

    If you have OpenSSL installed:
    ```powershell
    openssl pkcs12 -in certificate.pem.crt -inkey private.pem.key -out certificate.pfx
    ```

    Otherwise use [CertUtil](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/certutil).
    ```powershell
    certutil -mergePFX certificate.pem.crt,private.pem.key certificate.pfx
    ```

3)  Add the .pfx file to a Windows certificate store using PowerShell's
    [Import-PfxCertificate](https://docs.microsoft.com/en-us/powershell/module/pki/import-pfxcertificate)

    In this example we're adding it to "CurrentUser\My"

    ```powershell
    $mypwd = Get-Credential -UserName 'Enter password below' -Message 'Enter password below'
    Import-PfxCertificate -FilePath certificate.pfx -CertStoreLocation Cert:\CurrentUser\My -Password $mypwd.Password
    ```

    Note the certificate thumbprint that is printed out:
    ```
    Thumbprint                                Subject
    ----------                                -------
    A11F8A9B5DF5B98BA3508FBCA575D09570E0D2C6  CN=AWS IoT Certificate
    ```

    So this certificate's path would be: "CurrentUser\My\A11F8A9B5DF5B98BA3508FBCA575D09570E0D2C6"

4) Now you can run the sample:

    ```sh
    # For Windows: replace 'python3' with 'python'
    python3 windows_cert_connect.py --endpoint <endpoint> --ca_file <path to root CA> --cert <path to certificate>
    ```

## Custom Authorizer Connect

This sample makes an MQTT connection and connects through a [Custom Authorizer](https://docs.aws.amazon.com/iot/latest/developerguide/custom-authentication.html). On startup, the device connects to the server and then disconnects. This sample is for reference on connecting using a custom authorizer.

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
      ]
    }
  ]
}
</pre>
</details>

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 custom_authorizer_connect.py --endpoint <endpoint> --ca_file <path to root CA> --custom_auth_authorizer_name <authorizer name>
```

You will need to setup your Custom Authorizer so that the lambda function returns a policy document. See [this page on the documentation](https://docs.aws.amazon.com/iot/latest/developerguide/config-custom-auth.html) for more details and example return result.

## Shadow

This sample uses the AWS IoT
[Device Shadow](https://docs.aws.amazon.com/iot/latest/developerguide/iot-device-shadows.html)
Service to keep a property in
sync between device and server. Imagine a light whose color may be changed
through an app, or set by a local user.

Once connected, type a value in the terminal and press Enter to update
the property's "reported" value. The sample also responds when the "desired"
value changes on the server. To observe this, edit the Shadow document in
the AWS Console and set a new "desired" value.

On startup, the sample requests the shadow document to learn the property's
initial state. The sample also subscribes to "delta" events from the server,
which are sent when a property's "desired" value differs from its "reported"
value. When the sample learns of a new desired value, that value is changed
on the device and an update is sent to the server with the new "reported"
value.

Source: `samples/shadow.py`

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 shadow.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file> --thing_name <name>
```

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect, subscribe, publish, and receive. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Publish"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/get",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/update"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/get/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/get/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/update/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/update/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/shadow/update/delta"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Subscribe"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/shadow/get/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/shadow/get/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/shadow/update/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/shadow/update/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/shadow/update/delta"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "iot:Connect",
      "Resource": "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
    }
  ]
}
</pre>
</details>

## Jobs

This sample uses the AWS IoT
[Jobs](https://docs.aws.amazon.com/iot/latest/developerguide/iot-jobs.html)
Service to get a list of pending jobs and
then execution operations on these pending jobs until there are no more
remaining on the device. Imagine periodic software updates that must be sent to and
executed on devices in the wild.

This sample requires you to create jobs for your device to execute. See
[instructions here](https://docs.aws.amazon.com/iot/latest/developerguide/create-manage-jobs.html).

On startup, the sample tries to get a list of all the in-progress and queued
jobs and display them in a list. Then it tries to start the next pending job execution.
If such a job exists, the sample emulates "doing work" by spawning a thread
that sleeps for several seconds before marking the job as SUCCEEDED. When no
pending job executions exist, the sample sits in an idle state.

The sample also subscribes to receive "Next Job Execution Changed" events.
If the sample is idle, this event wakes it to start the job. If the sample is
already working on a job, it remembers to try for another when it's done.
This event is sent by the service when the current job completes, so the
sample will be continually prompted to try another job until none remain.

Source: `samples/jobs.py`

Run the sample like this:
``` sh
# For Windows: replace 'python3' with 'python'
python3 jobs.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file> --thing_name <name>
```

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect, subscribe, publish, and receive. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>Sample Policy</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iot:Publish",
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/start-next",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/*/update",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/*/get",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/get"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "iot:Receive",
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/notify-next",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/start-next/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/*/update/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/get/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/things/<b>thingname</b>/jobs/*/get/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "iot:Subscribe",
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/jobs/notify-next",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/jobs/start-next/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/jobs/*/update/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/jobs/get/*",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/things/<b>thingname</b>/jobs/*/get/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "iot:Connect",
      "Resource": "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
    }
  ]
}
</pre>
</details>

## Fleet Provisioning

This sample uses the AWS IoT
[Fleet provisioning](https://docs.aws.amazon.com/iot/latest/developerguide/provision-wo-cert.html)
to provision devices using either a CSR or Keys-And-Certificate and subsequently calls RegisterThing.

On startup, the script subscribes to topics based on the request type of either CSR or Keys topics,
publishes the request to corresponding topic and calls RegisterThing.

Source: `samples/fleetprovisioning.py`

Run the sample using createKeysAndCertificate:
``` sh
# For Windows: replace 'python3' with 'python'
python3 fleetprovisioning.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file> --template_name <name> --template_parameters <parameters>
```

Run the sample using createCertificateFromCsr:
``` sh
# For Windows: replace 'python3' with 'python'
python3 fleetprovisioning.py --endpoint <endpoint> --ca_file <file> --cert <file> --key <file> --template_name <name> --template_parameters <parameters> --csr <csr file>
```

Your Thing's [Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) must provide privileges for this sample to connect, subscribe, publish, and receive. Make sure your policy allows a client ID of `test-*` to connect or use `--client_id <client ID here>` to send the client ID your policy supports.

<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iot:Publish",
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create/json",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create-from-csr/json",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/provisioning-templates/<b>templatename</b>/provision/json"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create/json/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create-from-csr/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/certificates/create-from-csr/json/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/provisioning-templates/<b>templatename</b>/provision/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/$aws/provisioning-templates/<b>templatename</b>/provision/json/rejected"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Subscribe"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/certificates/create/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/certificates/create/json/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/certificates/create-from-csr/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/certificates/create-from-csr/json/rejected",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/provisioning-templates/<b>templatename</b>/provision/json/accepted",
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/$aws/provisioning-templates/<b>templatename</b>/provision/json/rejected"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "iot:Connect",
      "Resource": "arn:aws:iot:<b>region</b>:<b>account</b>:client/test-*"
    }
  ]
}
</pre>
</details>

### Fleet Provisioning Detailed Instructions

#### AWS Resource Setup

Fleet provisioning requires some additional AWS resources be set up first. This section documents the steps you need to take to
get the sample up and running. These steps assume you have the AWS CLI installed and the default user/credentials has
sufficient permission to perform all of the listed operations. These steps are based on provisioning setup steps
that can be found at [Embedded C SDK Setup](https://docs.aws.amazon.com/freertos/latest/lib-ref/c-sdk/provisioning/provisioning_tests.html#provisioning_system_tests_setup).

First, create the IAM role that will be needed by the fleet provisioning template. Replace `RoleName` with a name of the role you want to create.
``` sh
aws iam create-role \
    --role-name [RoleName] \
    --assume-role-policy-document '{"Version":"2012-10-17","Statement":[{"Action":"sts:AssumeRole","Effect":"Allow","Principal":{"Service":"iot.amazonaws.com"}}]}'
```
Next, attach a policy to the role created in the first step. Replace `RoleName` with the name of the role you created previously.
``` sh
aws iam attach-role-policy \
        --role-name [RoleName] \
        --policy-arn arn:aws:iam::aws:policy/service-role/AWSIoTThingsRegistration
```
Finally, create the template resource which will be used for provisioning by the demo application. This needs to be done only
once. To create a template, the following AWS CLI command may be used. Replace `TemplateName` with the name of the fleet
provisioning template you want to create. Replace `RoleName` with the name of the role you created previously. Replace
`TemplateJSON` with the template body as a JSON string (containing escape characters). Replace `account` with your AWS
account number.
``` sh
aws iot create-provisioning-template \
        --template-name [TemplateName] \
        --provisioning-role-arn arn:aws:iam::[account]:role/[RoleName] \
        --template-body "[TemplateJSON]" \
        --enabled
```
The rest of the instructions assume you have used the following for the template body:

<details>
<summary>(see template body)</summary>
``` sh
{
  "Parameters": {
    "DeviceLocation": {
      "Type": "String"
    },
    "AWS::IoT::Certificate::Id": {
      "Type": "String"
    },
    "SerialNumber": {
      "Type": "String"
    }
  },
  "Mappings": {
    "LocationTable": {
      "Seattle": {
        "LocationUrl": "https://example.aws"
      }
    }
  },
  "Resources": {
    "thing": {
      "Type": "AWS::IoT::Thing",
      "Properties": {
        "ThingName": {
          "Fn::Join": [
            "",
            [
              "ThingPrefix_",
              {
                "Ref": "SerialNumber"
              }
            ]
          ]
        },
        "AttributePayload": {
          "version": "v1",
          "serialNumber": "serialNumber"
        }
      },
      "OverrideSettings": {
        "AttributePayload": "MERGE",
        "ThingTypeName": "REPLACE",
        "ThingGroups": "DO_NOTHING"
      }
    },
    "certificate": {
      "Type": "AWS::IoT::Certificate",
      "Properties": {
        "CertificateId": {
          "Ref": "AWS::IoT::Certificate::Id"
        },
        "Status": "Active"
      },
      "OverrideSettings": {
        "Status": "REPLACE"
      }
    },
    "policy": {
      "Type": "AWS::IoT::Policy",
      "Properties": {
        "PolicyDocument": {
          "Version": "2012-10-17",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [
                "iot:Connect",
                "iot:Subscribe",
                "iot:Publish",
                "iot:Receive"
              ],
              "Resource": "*"
            }
          ]
        }
      }
    }
  },
  "DeviceConfiguration": {
    "FallbackUrl": "https://www.example.com/test-site",
    "LocationUrl": {
      "Fn::FindInMap": [
        "LocationTable",
        {
          "Ref": "DeviceLocation"
        },
        "LocationUrl"
      ]
    }
  }
}
```
</details>

If you use a different body, you may need to pass in different template parameters.

#### Running the sample and provisioning using a certificate-key set from a provisioning claim

To run the provisioning sample, you'll need a certificate and key set with sufficient permissions. Provisioning certificates are normally
created ahead of time and placed on your device, but for this sample, we will just create them on the fly. You can also
use any certificate set you've already created if it has sufficient IoT permissions and in doing so, you can skip the step
that calls `create-provisioning-claim`.

We've included a script in the utils folder that creates certificate and key files from the response of calling
`create-provisioning-claim`. These dynamically sourced certificates are only valid for five minutes. When running the command,
you'll need to substitute the name of the template you previously created, and on Windows, replace the paths with something appropriate.

(Optional) Create a temporary provisioning claim certificate set:
``` sh
aws iot create-provisioning-claim \
        --template-name [TemplateName] \
        | python3 ../utils/parse_cert_set_result.py \
        --path /tmp \
        --filename provision
```

The provisioning claim's cert and key set have been written to `/tmp/provision*`. Now you can use these temporary keys
to perform the actual provisioning. If you are not using the temporary provisioning certificate, replace the paths for `--cert`
and `--key` appropriately:

``` sh
# For Windows: replace 'python3' with 'python'
python3 fleetprovisioning.py \
        --endpoint <endpoint> \
        --ca_file <path to root CA> \
        --cert <path to certificate> \
        --key <path to private key> \
        --template_name <template name> \
        --template_parameters "{\"SerialNumber\":\"1\",\"DeviceLocation\":\"Seattle\"}"
```

Notice that we provided substitution values for the two parameters in the template body, `DeviceLocation` and `SerialNumber`.

#### Run the sample using the certificate signing request workflow

To run the sample with this workflow, you'll need to create a certificate signing request.

First create a certificate-key pair:
``` sh
openssl genrsa -out /tmp/deviceCert.key 2048
```

Next create a certificate signing request from it:
``` sh
openssl req -new -key /tmp/deviceCert.key -out /tmp/deviceCert.csr
```

(Optional) As with the previous workflow, we'll create a temporary certificate set from a provisioning claim. This step can
be skipped if you're using a certificate set capable of provisioning the device:

``` sh
aws iot create-provisioning-claim \
        --template-name [TemplateName] \
        | python3 ../utils/parse_cert_set_result.py \
        --path /tmp \
        --filename provision
```

Finally, supply the certificate signing request while invoking the provisioning sample. As with the previous workflow, if
using a permanent certificate set, replace the paths specified in the `--cert` and `--key` arguments:

``` sh
# For Windows: replace 'python3' with 'python'
python3 fleetprovisioning.py \
        --endpoint <endpoint> \
        --ca_file <path to root CA> \
        --cert <path to certificate> \
        --key <path to key> \
        --template_name <template name> \
        --template_parameters "{\"SerialNumber\":\"1\",\"DeviceLocation\":\"Seattle\"}" \
        --csr <path to csr file>
```

## Greengrass Discovery

This sample is intended for use with the following tutorials in the AWS IoT Greengrass documentation:

* [Connect and test client devices](https://docs.aws.amazon.com/greengrass/v2/developerguide/client-devices-tutorial.html) (Greengrass V2)
* [Test client device communications](https://docs.aws.amazon.com/greengrass/v2/developerguide/test-client-device-communications.html) (Greengrass V2)
* [Getting Started with AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/latest/developerguide/gg-gs.html) (Greengrass V1)
