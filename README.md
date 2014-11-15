# BoxSimpleOAuth [![License](http://b.repl.ca/v1/License-MIT-blue.png)]

A quick and simple way to authenticate a Box user in your iPhone or iPad app.

## Adding BoxSimpleOAuth to your project

### Clone from Github

1.  Clone repository from github and copy files directly, or add it as a git submodule.
2.  Add all files from 'Source' directory to your project.

## How To

* Create an instance of `BoxSimpleOAuthViewController` and pass in an [Box client ID, client secret, client callback URL](https://developers.box.com) and completion block to be executed with `BoxLoginResponse` and `NSError` arguments.
* Once the instance of `BoxSimpleOAuthViewController` is presented (either as a modal or pushed on the navigation stack), it will allow the user to login.  After the user logs in, the completion block given in the initialization of the view controller will be executed.  The argument in the completion block, `BoxLoginResponse`, contains an accessToken and other login information for the authenticated user provided by [Box API Response](https://developers.box.com/oauth/).  If there is an issue attempting to authenticate, an error will be given instead.
* By default, if there are issues with authentication, an UIAlertView will be given to the user.  To disable this, and rely on the NSError directly, set the property `shouldShowErrorAlert` to NO.
* Note: Even though an instance of the view controller itself can be initalized without client ID, client secret, client callback and completion block (to help with testing), this data must be set using the view controller's properties before it is presented to the user.

### Example Usage

```objective-c
// Simplest Example:

BoxSimpleOAuthViewController
*viewController = [[BoxSimpleOAuthViewController alloc] initWithClientID:@"123I_am_a_client_id_567890"
clientSecret:@"shhhhhh, I'm a secret"
callbackURL:[NSURL URLWithString:@"http://your.fancy.site"]
completion:^(BoxLoginResponse *response, NSError *error) {
NSLog(@"My Access Token is: %@", response.accessToken);
}];
[self.navigationController pushViewController:viewController
animated:YES];

// Disable error UIAlertViews Example:

BoxSimpleOAuthViewController
*viewController = [[BoxSimpleOAuthViewController alloc] initWithClientID:@"123I_am_a_client_id_567890"
clientSecret:@"shhhhhh, I'm a secret"
callbackURL:[NSURL URLWithString:@"http://your.fancy.site"]
completion:^(BoxLoginResponse *response, NSError *error) {
NSLog(@"My OAuth Token is: %@", response.accessToken);
}];
viewController.shouldShowErrorAlert = NO;

[self.navigationController pushViewController:viewController
animated:YES];
```

## Testing

* Prerequisites: [ruby](https://github.com/sstephenson/rbenv), [ruby gems](https://rubygems.org/pages/download), [bundler](http://bundler.io)

To use the included Rakefile to run Specta tests, run the setup.sh script to bundle required gems and cocoapods:

```bash
$ ./setup.sh
```

Then run rake to run the tests on the command line:

```bash
$ bundle exec rake
```

Additional rake tasks can be seen using rake -T:

```bash
$ rake -T
rake build  # Build BoxSimpleOAuth
rake clean  # Clean
rake test   # Run Tests
```

## Suggestions, requests, and feedback

Thanks for checking out BoxSimpleOAuth for your in-app Box authentication.  Any feedback can be
can be sent to: rbaumbach.github@gmail.com.
