# Nova Items Field

[![Latest Version on Packagist](https://img.shields.io/packagist/v/blendbyte/nova-items-field.svg?style=flat-square)](https://packagist.org/packages/blendbyte/nova-items-field)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](license.md)

Laravel Nova array items field with sorting, validation & many [display options](#options).

Forked from [dillingham/nova-items-field](https://github.com/dillingham/nova-items-field).

![nova-array-input-field](https://user-images.githubusercontent.com/29180903/51337942-7d1be300-1a56-11e9-84fa-66f5b285c279.png)

## Installation

```bash
composer require blendbyte/nova-items-field
```

## Quick Start

```php
use NovaItemsField\Items;

function fields() {
    return [
        Items::make('Emails'),
    ];
}
```

Be sure to [cast](https://laravel.com/docs/eloquent-mutators#array-and-json-casting) the property as an array on your Eloquent model:

```php
public $casts = [
    'emails' => 'array',
];
```

## Validation

Use Laravel's built-in [array validation](https://laravel.com/docs/validation#validating-arrays):

```php
Items::make('Emails')->rules([
    null => 'required|min:2',
    '*'  => 'email|min:10',
]),
```

In this case, an error is produced if there aren't at least 2 items in the array and if each item is not a valid email or is shorter than 10 characters.

You can also use explicit attribute names — the behaviour is exactly the same:

```php
Items::make('Emails', 'user_email')->rules([
    'user_email'   => 'required|min:2',
    'user_email.*' => 'email|min:10',
]),
```

## Array Processing

Use the array to perform other actions by making an [observer](https://laravel.com/docs/eloquent#observers):

```php
function saving($user)
{
    foreach ($user->emails as $email) {
        //
    }
}
```

## Customizing the Vue Component

You can replace the default item Vue component — see [this walkthrough](https://github.com/dillingham/nova-items-field/issues/10#issuecomment-527315057) for a brief guide.

## Options

| Method                         | Description                                          | Default          |
|--------------------------------|------------------------------------------------------|------------------|
| `->max(number)`                | Limit number of items allowed                        | `false`          |
| `->draggable()`                | Turn on drag/drop sorting                            | `false`          |
| `->fullWidth()`                | Increase the width of the field area                 | `false`          |
| `->maxHeight(pixel)`           | Limit the height of the list                         | `false`          |
| `->listFirst()`                | Move "add new" to the bottom                         | `false`          |
| `->inputType(text)`            | Input type: `text`, `date`, etc.                     | `"text"`         |
| `->placeholder($value)`        | Placeholder text for the new item input              | `"Add a new item"` |
| `->deleteButtonValue($value)`  | Label for the delete button                          | `"x"`            |
| `->createButtonValue($value)`  | Label for the create button                          | `"Add"`          |
| `->hideCreateButton()`         | Hide the "Add" button                                | `false`          |
| `->indexAsList()`              | Display items as a list on index instead of a count  | `false`          |
| `->detailsAsTotal()`           | Display item count on detail view instead of a list  | `false`          |

## Maintained by Blendbyte

<br>

<p align="center">
  <a href="https://www.blendbyte.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://www.blendbyte.com/logo_horizontal_light.png">
      <img src="https://www.blendbyte.com/logo_horizontal.png" alt="Blendbyte" width="360">
    </picture>
  </a>
</p>

<p align="center">
  <strong><a href="https://www.blendbyte.com">Blendbyte</a></strong> builds cloud infrastructure, web apps, and developer tools.<br>
  We've been shipping software to production for 20+ years.
</p>

<p align="center">
  This package runs in our own stack, which is why we keep it maintained.<br>
  Issues and PRs get read. Good ones get merged.
</p>

<br>

<p align="center">
  <a href="https://www.blendbyte.com">blendbyte.com</a> · <a href="mailto:hello@blendbyte.com">hello@blendbyte.com</a>
</p>
