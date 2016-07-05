Letsencrypt standalone
======================

This role's duty is to install [Certbot](https://certbot.eff.org/) and to obtain SSL certificates via [Letsencrypt](https://letsencrypt.org/) using the standalone plugin.

Furthermore, a cron job will be set up to attempt renewal of already generated certificates (if needed) at a random hour/minute twice a day.

Variables
---------

### `letsencrypt_path`
Path where Certbot binary should be installed. By default, this is `/usr/local/bin`.

### `letsencrypt_staging`
Whether to use staging CA to issue certificates. Using this CA will noticeably increase API limits, but this option should be used for testing purposes only, as the resulting certificate will not be trusted by user browsers. By default, this option is disabled.

### `letsencrypt_renew`
Whether to set up automated renewal of certificates that are close to their expiration date. It is _highly_ recommended that you leave this turned on. By default, this option is enabled.

### `letsencrypt_email`
Email address to be used when issuing requests to Letsencrypt. By default, this option is `webmaster@{{ ansible_fqdn }}` (e.g. `webmaster@example.com`). Despite not strictly necessary, you **SHOULD** customize this setting.

### `letsencrypt_domains`
List of domains to generate certificates for. A single certificate valid for all listed domains will be generated. By default, this list is empty (i.e. no certificate is generated).

Example
-------

```yaml
---
letsencrypt_staging: yes
letsencrypt_renew: yes

letsencrypt_email: "webmaster@example.com"
letsencrypt_domains:
  - example.com
  - www.example.com
  - idp.example.com
  - staging.example.com
  - mail.example.com
```
