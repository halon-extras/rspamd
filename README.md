# Rspamd anti-spam client

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-rspamd
```

### RHEL

```
yum install halon-extras-rspamd
```

## Exported classes

These classes needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://rspamd` module path.

### Rspamd (opts)
Scan a message with [rspamd](https://www.rspamd.com/).

**Params**

- opts `array` - options array

**Returns**: class object.

The following options are available in the **opts** array.

- host `string` - IP-address of the rspamd service. The default is `127.0.0.1`.
- port `number` - TCP port. The default is 11333.
- tls `array` - TLS options array for the rspamd service.
- controllerhost `string` - IP-address of the rspamd controller. The default is `127.0.0.1`.
- controllerport `number` - TCP port. The default is 11334.
- controllertls `array` - TLS options array for the rspamd controller.
- password `string` - Password for the rspamd controller.
- timeout `number` - Timeout in seconds. The default is 5 seconds.
- max_message_size `number` - The max message size in bytes. The default is 5 MiB.

The following options are available in the **tls** and **controllertls** array.

- enabled `boolean` - Enable TLS for the specific socket
- opts `array` - All available options can be found on [here](http://docs.halon.se/hsl/functions.html?highlight=tlssocket#TLSSocket)

#### scan(fp, headers)
Check if a message is spam or not. 

**Params**

- fp `File` - file object such as return type of [toFile()](https://docs.halon.io/hsl/functions.html#MailMessage.toFile). **Required**.
- headers `array` - headers array

The following headers can be set in the **headers** array.

- IP `string` - IP-address of the sender
- From `string` - The envelope sender
- Queue-Id `string` - The transaction ID
- Helo `string` - The HELO of the sender
- User `string` - The username of the authenticated client
- Subject `string` - The subject

**Returns**: associative array containing the result of the scan

**Return type**: `array`, `none` on error

#### learn(fp, type)
Send a message to the controller for learning.

**Params**

- fp `File` - file object such as return type of [toFile()](https://docs.halon.io/hsl/functions.html#MailMessage.toFile). **Required**.
- type `string` - Specify a type, either spam or ham. **Required**.

**Returns**: associative array containing the result of the scan

**Return type**: `array`, `none` on error