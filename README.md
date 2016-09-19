[![SensioLabsInsight](https://insight.sensiolabs.com/projects/e79d4122-c9ad-454f-a1ac-981dd683144f/mini.png)](https://insight.sensiolabs.com/projects/e79d4122-c9ad-454f-a1ac-981dd683144f)

# HashidsBundle

Integrates [hashids/hashids][1] in a Symfony2 project. 
## Installation

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```
    composer require roukmoute/hashids-bundle
```

This command requires you to have Composer installed globally.

## Enable the Bundle

Then, enable the bundle by adding the following line in the ``app/AppKernel.php``
file of your project:

```php
<?php
// app/AppKernel.php
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // …
            new Roukmoute\HashidsBundle\RoukmouteHashidsBundle()
        );
        // …
```

The configuration looks as follows :

```yaml
roukmoute_hashids:

    # if set, the hashids will differ from everyone else's
    salt:               ""

    # if set, will generate minimum length for the id
    # 0 — meaning hashes will be the shortest possible length
    min_hash_length:    0

    # if set, will use only characters of alphabet string
    alphabet:           ""
```

## Usage

```php
$hashids = $this->get('hashids');
```

Next it's the same things of [official documentation][2]

Hashids Converter
===============

Converter Name: `hashids.converter`

The hashids converter attempts to convert request hashid attributes to a
id for fetch a Doctrine entity. 

For specify to use hashids converter just add `"id" = "hashid"` in 
options.

```php
/**
 * @Route("/users/{hashid}")
 * @ParamConverter("user", class="RoukmouteBundle\Entity\User", options={"id" = "hashid"})
 */
public function getAction(User $user)
{
}
```

You could have several hashids one the same URL.
Just finish your word option with "hashid":

```php
/**
 * @Route("/users/{userHashid}/status/{statusHashid}")
 * @ParamConverter("user", class="Shippeo\Model\Entity\User", options={"id" = "userHashid"})
 * @ParamConverter("status", class="Shippeo\Model\Entity\User\Notification", options={"id" = "statusHashid"})
 */
public function getAction(User $user, Status $status)
{
}
```

[1]: https://github.com/ivanakimov/hashids.php
[2]: http://hashids.org/php/