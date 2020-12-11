## Laravel Socialite Microsoft Graph

```bash
composer require dayanstef/microsoft-graph
```

### Installation & Basic Usage

#### Add configuration to `config/services.php`

```php
'graph' => [    
  'tenant' => env('MICROSOFT_TENANT_ID'),
  'client_id' => env('MICROSOFT_CLIENT_ID'),  
  'client_secret' => env('MICROSOFT_CLIENT_SECRET'),  
  'redirect' => env('MICROSOFT_REDIRECT_URI') 
],
```

#### Add provider event listener

Configure the package's listener to listen for `SocialiteWasCalled` events.

Add the event to your `listen[]` array in `app/Providers/EventServiceProvider`.

```php
use SocialiteProviders\Manager\SocialiteWasCalled;

protected $listen = [
    SocialiteWasCalled::class => [
        'SocialiteProviders\\Graph\\GraphExtendSocialite@handle',
    ],
];
```

#### Usage


```php
Socialite::driver('graph')->stateless()->redirect();

// OR
// Some Applications require specific tenant definition
Socialite::driver('graph')->setTenantId('MICROSOFT_TENANT_ID')->stateless()->redirect();

// Get a user basic details
$user = Socialite::driver('graph')->setTenantId('MICROSOFT_TENANT_ID')->stateless()->user();

// Get user groups
$userGroups = Socialite::driver('graph')->getUserGroupsByToken($user, $user->token);
```
