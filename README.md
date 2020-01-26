# Drone CI
How to set up your private delivery platform by using [Drone](https://www.drone.io) and [Bitbucket](https://www.bitbucket.org) and your [private docker registry](https://www.github.com/squaremonks/docker-registry).

## Installation

### Digitalocean
For this project we use a server from [Digitalocean droplets](https://m.do.co/c/5fb9f23e93fe). Create a droplet with a [Docker image](https://marketplace.digitalocean.com/apps/docker) from the Marketplace.
_Add your ssh key to this droplet to enter console easily._

#### Server configuration
Allow traffic via port 443 to your server by adding the firewall rule.
```bash
$ ufw allow '443/tcp'
```

Copy the `docker-compose.yml` file as in this repository.
```bash
DRONE_BITBUCKET_CLIENT_ID: ''       # See OAuth in Bitbucket 
DRONE_BITBUCKET_CLIENT_SECRET: ''   # See OAuth in Bitbucket
DRONE_RPC_SECRET: ''                # A secret code that can be generated with openssl. 
DRONE_SERVER_HOST: ''               # name.domain.ext
DRONE_RPC_HOST: ''                  # name.domain.ext
```
Fill in your own information.

Run the `docker-compose.yml` file with detached so it can be runned on the background.
```bash
$ docker-compose up -d
```

### How to add your drone secrets?
See more at [Drone.io](https://docs.drone.io/cli/install/).

Example:
```bash
$ drone secret add --repository organization/repository -name docker_username --data your_username 
```

### Bitbucket
Go to your account and add your consumer for OAuth.

Example:
```yaml
Name: Drone
Callback URL: https://name.domain.ext/login
Check 'This is a private repository'.

Permissions:
Account: 
- E-mail
- Read

Pull requests:
- Read
- Write

Team membership:
- Read

Repositories:
- Read
- Write
- Admin

Webhooks:
- Read and write
```

Add `.drone.yml` (as an example) to your project and you are good to go to build images.


## Credits and acknowledgements

* Author: [Kiet Tran][link-author]

Also see the list of [contributors][link-contributors] who participated in this project.

## License
The docker-registry is licensed under the MIT License. Please see the [LICENSE file][link-license] for details.

[link-version]: https://packagist.org/packages/squaremonks/docker-registry
[link-license]: LICENSE
[link-author]: https://github.com/kiettran
[link-contributors]: https://github.com/squaremonks/docker-registry/contributors
