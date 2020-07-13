# Validation
A validation class that help php developers validate incoming input

## Usage

```php

$v = new Validate($_POST, [
    'email' => [
        'required' => true,
        'unique' => function (string $value) use ($args): bool {
            $users = (new User())->find(DB::setConditions(['email', $args['email']]));
            return !!!count($users);
        },
    ],
    'password' => [
        'required' => true,
        'min' => 6,
        'matches' => 'password_confirm'
    ],
]);

// checks if the incoming data passes the rules
if($v->passed()){
    // do something here
}else{
    //return a list of errors
    $errors = $v->errors();
}

```


