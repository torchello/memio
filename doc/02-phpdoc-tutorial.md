# PHPdoc Tutorial

Medio also provides a way to document the code with [PHPdoc](http://www.phpdoc.org/).

By default no PHPdoc is generated, this must be triggered by setting a PHPdoc object in the model.

![UML class diagram](http://yuml.me/bc9d239b)

## 1. License

`Files` can have a license header, which usually displays the name of the project,
the author's name and their emails:

```php
use Gnugat\Medio\Model\File;
use Gnugat\Medio\Model\Object;
use Gnugat\Medio\Model\Phpdoc\LicensePhpdoc;

$file = File::make('src/Gnugat/Medio/MyClass')
    ->setLicensePhpdoc(new LicensePhpdoc('MyProject', 'Me', 'me@example.com'))

    ->setStructure(new Object('Gnugat\Medio\MyClass'))
;

echo $prettyPrinter->generateCode($file);
```

This will output:

```php
<?php

/*
 * This file is part of the My Project project.
 *
 * (c) Me <me@example.com>
 *
 * For the full copyright and license information, please view the LICENSE
 * file that was distributed with this source code.
 */

namespace Gnugat\Medio;

class MyClass
{
}
```

## 2. Structure's PHPdoc

A `Structure` (an `Object` or a `Contract`) can have the following:

* a description
* a deprecation tag
* an API tag

Here's how to describe it:

```php
use Gnugat\Medio\Model\Contract;
use Gnugat\Medio\Model\Phpdoc\ApiTag;
use Gnugat\Medio\Model\Phpdoc\Description;
use Gnugat\Medio\Model\Phpdoc\DeprecationTag;
use Gnugat\Medio\Model\Phpdoc\StructurePhpdoc;

$contract = Contract::make('Gnugat\Medio\MyInterface')
    ->setStructurePhpdoc(StructurePhpdoc()
        ->setDescription(Description::make('This is the first line')
            ->addEmptyLine()
            ->addLine('This is the third line')
        )
        ->setDeprecationTag(new DeprecationTag()) // Has 2 optional arguments: version, and description
        ->setApiTag(new ApiTag('v2.0')) // The argument is optional
    )
;

echo $prettyPrinter->generateCode($contract);
```

This will produce:

```php
/**
 * This is the first line
 *
 * This is the third line
 *
 * @deprecated
 *
 * @api v2.0
 */
interface MyInterface
{
}
```

## Next readings

* [Examples](03-examples.md)
* [Extending](04-extending.md)

Previous pages:

* [Model Tutorial](01-model-tutorial.md)
* [README](../README.md)