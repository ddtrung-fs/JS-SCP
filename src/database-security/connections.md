Database Connections
====================

## Connection String Protection

To keep your connection strings secure, it's always a good practice to put the
authentication details in a separated configuration file far from public access.

Instead of placing your configuration file at `/your/app/path/public_html/`,
consider using a restricted access location `/some/private/path/config.json`

```json
{
  "db": {
    "user": "f00",
    "pass": "f00?bar#ItsP0ssible",
    "host": "localhost",
    "port": "3306"
  }
}
```

Then you can load your `config.json` file on your JavaScript application:

```javascript
const fs = require('fs');
const config = require('/some/private/path/config.json');

console.log('Configuration loaded');
```

Of course, if the attacker has root access, he/she could see the file which
brings us to the most secure thing you can do - encrypt the file.

Note that required file path includes the `.json` suffix: this tells Node.js to
load and parse the content as JSON and not as a regular JavaScript file,
preventing code execution.

## Database Credentials

You should use different credentials for every trust distinction and level:

* User
* Read-only user
* Guest
* Admin

Therefore, if a connection is being made for a read-only user, they could never
mess up with your database information because the user actually can only read
the data.
