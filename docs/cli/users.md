# User Management

nio uses BasicAuth to authenticate to all of it's endpoints. For more information on nio authentication see [Authentication and authorization](/api/conventions.md)

For added security, each password associated with a user name will be one way encrypted using the bcrypt hashing method. This protects nio user credentials stored on a device from malicious authentication. bcrypt hashing prevents reverse password lookups through the use of rainbow tables.  

## Adding a user

```bash
nio add_user <username> <password>
```

Creates a new user with the provided (hashed) password to authenticate to nio with. 

### Example
```bash
nio add_user nio superSecretPassword
```

You should see the output:
```bash
Adding user: nio
Adding permissions for user: nio
```

After running this command you will be able to authenticate to nio by using this BasicAuth:
```javascript
authorization: Basic bmlvOnN1cGVyU2VjcmV0UGFzc3dvcmQ=
```

> bmlvOnN1cGVyU2VjcmV0UGFzc3dvcmQ= is nio:superSecretPassword base64 encoded

---

## Removing a user

```bash
nio remove_user <username>
```

Removes the user from having the ability to authenticate with nio.

### Example
```bash
nio remove_user olduser
```

After running this you should see:

```bash
Removing user: olduser
Removing permissions for user: olduser
```

---


