What version of Cloud Foundry and CF CLI are you using? (i.e. What is the output of running `cf curl /v2/info && cf version`?

```
{
   "name": "",
   "build": "",
   "support": "",
   "version": 0,
   "description": "",
   "authorization_endpoint": "https://login.fr.cloud.gov",
   "token_endpoint": "https://uaa.fr.cloud.gov",
   "min_cli_version": null,
   "min_recommended_cli_version": null,
   "api_version": "2.101.0",
   "app_ssh_endpoint": "ssh.fr.cloud.gov:2222",
   "app_ssh_host_key_fingerprint": "redacted",
   "app_ssh_oauth_client": "ssh-proxy",
   "doppler_logging_endpoint": "wss://doppler.fr.cloud.gov:443",
   "user": "redacted"
}
```

```
$ cf version
cf version 6.32.0+0191c33d9.2017-09-26
```

What version of the buildpack you are using?

```
buildpack: https://github.com/cloudfoundry/php-buildpack.git
```


If you were attempting to accomplish a task, what was it you were attempting to do?

I'm attempting to pass options to composer but nothing worked. So with these
.bp-config/options.js

```

{
  "WEB_SERVER": "httpd",
  "ADMIN_EMAIL": "your-email@example.com",
  "COMPOSER_INSTALL_OPTIONS": [
    "--this-should-fail"
  ],
  "COMPOSER_VENDOR_DIR": "pbtest"
}
```

What did you expect to happen?

I expected `cf push` to fail with an invalid option as it does on the CLI:

```
composer --this-should-fail


  [Symfony\Component\Console\Exception\RuntimeException]
  The "--this-should-fail" option does not exist.
```


And I expected composer to vendor stuff into `pbtest`

What was the actual behavior?

* No failure
* SSH into container and `find . -name 'pbtest'` turns up nothing

Completed run, no errors.


Please confirm where necessary:
* [ ] I have included a log output
* [ ] My log includes an error message
* [x] I have included steps for reproduction


See https://github.com/pburkholder/php-micro

 
