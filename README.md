# CakePHP AdminLTE Theme (1.1.0-plugin)
# Separate Templates for each Plugin

**What's diferent in this fork**

First of all thanks to [maiconpinto](http://github.com/maiconpinto/cakephp-adminlte-theme) and his awesome work!

*Short version*:

Manage AdminLTE template in every Plugin's `/PluginName/src/Template/AdminLTE` path in order to output a totally separate AdminLTE template for each Plugin instead of having all templates sitting in App's Template's root.

*Extended version*:

Since I'm deveolping a multilevel-administered platform fully based on CakePHP 3.7.4 and since there's the need of a diferent setup for each administration level, I tough it would be useful to have the power of AdminLTE for all of the administration templates while using a different set of templates customization for each level of administration.
The project assumes that every administration level is managed as a Plugin, so that it can be plugged/unplugged as the needs. Assuming that it appeared a crucial point to have a core AdminLTE plugin sitting in App's `vendor` path which Template's `.ctp` files could be overwritten by each Plugin's template's `.ctp` files.
This can be achieved by putting the element's you want to overwrite in App root's `plugins/PluginName/src/Template/AdminLTE` in the according `Subfolder/filename.ctp`.

For the sake of clarity, let's say you have two plugins one called `AdminPlugin` abd the other `EditorPlugin` now if you want to use AdminLTE in both buit have a different footer for each one, it would be enough to overwrite them by creating the following files

`/path/to/your/app/plugins/AdminPlugin/src/Template/AdminLTE/Element/footer.ctp`

`/path/to/your/app/plugins/EditorPlugin/src/Template/AdminLTE/Element/footer.ctp`

I know this sounds not much a DRY code, but there can be situations where it's strongly needed to keep templates separated between each other for security reasons or cleaner code deploy. 

Hope it helps someone aroud there...

**What's the news**

The AdminLTE is still at version 2.4.5.

The CakePHP was updated version compatible to 3.7.4.

This release 1.1.0-plugin is can be considered the stable version, as indicated in the [SemVer.org](https://semver.org/) recommendations.

### Installation

You can install using [composer](http://getcomposer.org).

```
composer require sevypannella/cakephp-adminlte-theme
```

### Enable Plugin

```php
// src/Application.php

public function bootstrap()
{
    $this->addPlugin('AdminLTE');
}
```

Before of CakePHP 3.7

```php
// config/bootstrap.php

Plugin::load('AdminLTE', ['bootstrap' => true, 'routes' => true]);
```

### Enable Theme

```php
// src/Controller/AppController.php

public function beforeRender(Event $event)
{
    $this->viewBuilder()->setClassName('AdminLTE.AdminLTE');
    $this->viewBuilder()->setTheme('AdminLTE');

    // Before of CakePHP 3.5
    $this->viewBuilder()->ClassName('AdminLTE.AdminLTE');
    $this->viewBuilder()->theme('AdminLTE');
}
```

### Enable Form

```php
// src/View/AppView.php

public function initialize()
{
    $this->loadHelper('Form', ['className' => 'AdminLTE.Form']);
}
```

### Configure

```php
// new config/adminlte.php file

return [
    'Theme' => [
        'title' => 'AdminLTE',
        'logo' => [
            'mini' => '<b>A</b>LT',
            'large' => '<b>Admin</b>LTE'
        ],
        'login' => [
            'show_remember' => true,
            'show_register' => true,
            'show_social' => true
        ],
        'folder' => ROOT,
        'skin' => 'blue'
    ]
];

// config/bootstrap.php

Configure::load('adminlte', 'default');
```

Before of CakePHP 3.7

```php
// config/bootstrap.php

Configure::write('Theme', [
    'title' => 'AdminLTE',
    'logo' => [
        'mini' => '<b>A</b>LT',
        'large' => '<b>Admin</b>LTE'
    ],
    'login' => [
        'show_remember' => true,
        'show_register' => true,
        'show_social' => true
    ],
    'folder' => ROOT,
    'skin' => 'blue' // default is 'blue'
]);
```

# Customize Layout

If you want to [Customize Layout](https://github.com/sevypannella/cakephp-adminlte-theme/wiki/Customize-Layout)

# What's the features

### Layouts

There are 10 layout files.

- boxed
- collapsed
- default **it's the main layout**
- documentation
- fixed
- lockscreen
- login
- print
- register
- top

### View Blocks

There are 3 Blocks where you can extend your theme.

- **css**

```php
<?php echo $this->fetch('css'); ?>
```

One example is `src/Template/Pages/home.ctp`:

```php
<?php echo $this->Html->css('AdminLTE./bower_components/morris.js/morris', ['block' => 'css']); ?>
```

- **script**

```php
<?php echo $this->fetch('script'); ?>
```

One example is `src/Template/Pages/home.ctp`:

```php
<?php echo $this->Html->script('AdminLTE./bower_components/morris.js/morris.min', ['block' => 'script']); ?>
```

- **scriptBottom**

```php
<?php echo $this->fetch('scriptBottom'); ?>
```

One example is `src/Template/Pages/home.ctp`:

```php
<?php $this->start('scriptBottom'); ?>
    <script>
      $.widget.bridge('uibutton', $.ui.button);
    </script>
<?php  $this->end(); ?>
```

### Elements

There are 7 element files.

- Element/
    - aside/
        - form
        - sidebar-menu
        - user-panel
    - aside-control-sidebar
    - aside-main-sidebar
    - footer
    - nav-top

### Flash Message

The theme is prepared to show Flash Messages.

```php
<?php echo $this->Flash->render(); ?>
<?php echo $this->Flash->render('auth'); ?>
```

### Bake

One of the better Cake features. The theme is prepared to use Bake. 

```
bin/cake bake all user --theme AdminLTE
```

### View

- **AdminLTEView**

This is one the better theme feature. It change the pattern how Cake show view files.

Basically, you overwrite any theme, plugin and prefix files.

1. src/Template/Plugin/$theme/Plugin/$plugin/$prefix/
2. src/Template/Plugin/$theme/Plugin/$plugin/
3. src/Template/Plugin/$theme/$prefix/
4. src/Template/Plugin/$theme/

### FormHelper

FormHelper by default has format template based on Foundation template. This helper overwrite these templates.

### Behavior

- **DatepickerBehavior**

When you configure `App.defaultLocale` to `pt_BR` this Behavior is util.

### Locale

When you configure `App.defaultLocale` to `pt_BR` this Locale is util.

### Page debug

Added link to default page of CakePHP.

![Page debug](docs/page-debug.png)

# Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
