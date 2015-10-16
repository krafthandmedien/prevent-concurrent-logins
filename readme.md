<!-- DO NOT EDIT THIS FILE; it is auto-generated from readme.txt -->
# Prevent Concurrent Logins

![Banner](assets/banner-1544x500.png)
Prevents users from staying logged into the same account from multiple places.

**Contributors:** [fjarrett](https://profiles.wordpress.org/fjarrett)  
**Tags:** [login](https://wordpress.org/plugins/tags/login), [users](https://wordpress.org/plugins/tags/users), [membership](https://wordpress.org/plugins/tags/membership), [security](https://wordpress.org/plugins/tags/security), [sensei](https://wordpress.org/plugins/tags/sensei), [sessions](https://wordpress.org/plugins/tags/sessions), [woocommerce](https://wordpress.org/plugins/tags/woocommerce)  
**Requires at least:** 4.1  
**Tested up to:** 4.3  
**Stable tag:** 0.3.0  
**License:** [GPLv2+](https://www.gnu.org/licenses/gpl-2.0.html)  

[![Build Status](https://travis-ci.org/fjarrett/prevent-concurrent-logins.png?branch=master)](https://travis-ci.org/fjarrett/prevent-concurrent-logins) 

## Description ##

**Did you find this plugin helpful? Please consider [leaving a 5-star review](https://wordpress.org/support/view/plugin-reviews/prevent-concurrent-logins).**

* Deters members/subscribers from sharing their accounts with others
* Hardens security by destoying old sessions automatically
* Prompts old sessions to login again if they want to continue
* Ideal for membership sites and web applications

**Important:** If you plan to network-activate this plugin on a multisite network, please install the [Proper Network Activation](https://wordpress.org/plugins/proper-network-activation/) plugin _beforehand_.

**Development of this plugin is done [on GitHub](https://github.com/fjarrett/prevent-concurrent-logins). Pull requests welcome. Please see [issues reported](https://github.com/fjarrett/prevent-concurrent-logins/issues) there before going to the plugin forum.**

## Frequently Asked Questions ##

### Where are the options for this plugin? ###
This plugin does not have a settings page. Simply put, I don't like bloating my plugins with a bunch of options.

Instead, I try to develop functionality using the 80/20 principle so that for 80% of use cases you all you need to do is activate the plugin and it "just works".

For the other 20% of you who want things to behave differently there are hooks available in the plugin so you can customize default behaviors.

### Can I still allow concurrent logins for certain users? ###
Yes, simply add this code to your theme's `functions.php` file or as an [MU plugin](http://codex.wordpress.org/Must_Use_Plugins):

```php
function my_pcl_bypass_user_ids( $prevent, $user_id ) {

    $whitelist = array( 1, 2, 3 ); // <--- Provide an array of user IDs to bypass

    if ( in_array( $user_id, $whitelist ) ) {

        return false;

    }

    return $prevent;

}
add_filter( 'pcl_prevent_concurrent_logins', 'my_pcl_bypass_user_ids', 10, 2 );
```

Or this code to bypass users with certain roles:

```php
function my_pcl_bypass_roles( $prevent, $user_id ) {

    $whitelist = array( 'administrator', 'editor' ); // <--- Provide an array of roles to bypass

    $user = get_user_by( 'id', absint( $user_id ) );

    $roles = empty( $user->roles ) ? array() : $user->roles;

    $intersect = array_intersect( $roles, $whitelist );

    if ( ! empty( $intersect ) ) {

        return false;

    }

    return $prevent;

}
add_filter( 'pcl_prevent_concurrent_logins', 'my_pcl_bypass_roles', 10, 2 );
```


## Changelog ##

### 0.4.0 - October 16, 2015 ###
* Official support for WordPress 4.3

Props [fjarrett](https://github.com/fjarrett)

### 0.3.0 - May 4, 2015 ###
* Action hooks now available after sessions are destroyed for logging purposes [(#4)](https://github.com/fjarrett/prevent-concurrent-logins/issues/4)

Props [fjarrett](https://github.com/fjarrett)

### 0.2.0 - January 28, 2015 ###
* Destroy old sessions for all users upon activation

Props [fjarrett](https://github.com/fjarrett), [chuckreynolds](https://github.com/chuckreynolds)

### 0.1.1 - January 2, 2015 ###
* Added filter to allow certain users to have concurrent sessions when necessary

Props [fjarrett](https://github.com/fjarrett), [nutsandbolts](https://github.com/nutsandbolts)

### 0.1.0 - December 31, 2014 ###
* Initial release

Props [fjarrett](https://github.com/fjarrett)


