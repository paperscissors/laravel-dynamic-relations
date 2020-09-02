### Laravel DynamicRelations
---

An extension of `Illuminate\Database\Eloquent\Model` that allows relationships to be called as dynamic properties, such as:
```php
$prop = "myProp";
$user->$prop->toArray();
```
Fork from stale [patinthehat/laravel-dynamic-relations](https://github.com/patinthehat/laravel-dynamic-relations) repo.

####Installation

Install with composer: `composer require paperscissors/laravel-dynamic-relations`

####Usage

To use, extend the `DynamicModel` class.  In the child class, override the `$dynamicRelations` array property, adding items that correlate to relation names.

```php
namespace App\Models;

use Permafrost\DynamicRelations\DynamicModel;

class User extends DynamicModel
{
    public static $dynamicRelations = [
      'abc', 'def',
    ];
    
    public function abc()
    {
        return $this->hasMany('App\Models\Abc');
    }
    
    public function def()
    {
        return $this->hasMany('App\Models\Def');
    }
    
}
```

Now, your relations can be accessed dynamically:
```php
$user = User::find(1);
$prop = "abc";
$user->$prop->toArray();
```