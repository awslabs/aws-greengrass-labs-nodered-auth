# community.greengrass.nodered.auth

This component is is used to define the authentication mechanism for the Node-RED components.

To specify a new username and password you need to create a secret in AWS Secrets Manager with name `community.greengrass.nodered/<username>` and with the password as plain text value.

You also need to add and configure `aws.greengrass.SecretManager` component to the deployment. The configuration specify the secret to synchronize and should include at least the ARN of the secret created for the username.

```json
"cloudSecrets": [
    {
    "arn": "arn:aws:secretsmanager:eu-west-1:12345678901:secret:community.greengrass.nodered/<username>-XXXXXX"
    }
]
```

You must also configure the username to use in this component via the `username` configuration property.

If `username` is not equal to the value `none` this component gets the secret from SecretManager component, encodes an hash using `bcrypt` (see [Generating a password hash](https://nodered.org/docs/user-guide/runtime/securing-node-red#generating-the-password-hash)), and creates a settings file fragment that is stored in the work folder. 

The Node-RED components append this fragment (which in empty in case no authentication is configured) to the `settings.js` file.

If authentication is enabled, the admin API from Node-RED are protected. The `flows` and `nodes` components use this component to determine if there is a need to do an authenticated access.

## Versions
This component has the following versions:

* 1.0.0

## Type

This component is a generic component. The [Greengrass nucleus](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-nucleus-component.html) runs the component's lifecycle scripts.

For more information, see [component types](https://docs.aws.amazon.com/greengrass/v2/developerguide/manage-components.html#component-types)


## Requirements

This component requires Node v14 or above to be present on the device. 

This component allows the use to write custom code at runtime and additional requirements in term of ports used or permissions cannot be pre-defined.

## Dependencies

When you deploy a component, AWS IoT Greengrass also deploys compatible versions of its dependencies. This means that you must meet the requirements for the component and all of its dependencies to successfully deploy the component. This section lists the dependencies for the released versions of this component and the semantic version constraints that define the component versions for each dependency. You can also view the dependencies for each version of the component in the [AWS IoT Greengrass console](https://console.aws.amazon.com/greengrass). On the component details page, look for the Dependencies list.

### 1.0.0

| Dependency | Compatible versions | Dependency type |
|---|---|---|
| Greengrass nucleus | >=2.0.0 <2.5.0 | Soft |
| Secret Manager | >=0.0.0 | Hard |
| community.greengrass.SecretsManagerClient | >=0.0.0 | Soft |

## Configuration

This component provides the following configuration parameters that you can customize when you deploy the component.


`username`

(Optional) In order to secure the access to the Node-RED UI you can set a username and password.


## Local log file

This component uses the following log file:

```bash
/greengrass/v2/logs/community.greengrass.nodered.auth.log
```


## Changelog

The following table describes the changes in each version of the component.

| Version | Changes |
|---|---|
| 1.0.0 | Initial version |



