# Customize

## How to change the layout?

Go to `module/Customize/view`, create a `layout` directory and in this directory you have to create a file like `layout.twig` with the content of [default-design](https://github.com/kokspflanze/PServerCore/blob/master/view/layout/layout.twig).
These file that you create will be your custom design, so there you can everything you need=).
Now you have to register your custom layout in the config, for that you have to go to `module/Customize/config/module.config.php`, there you have to add `'layout/layout' => __DIR__ . '/../view/layout/layout.twig',`.
So the file will look like 
 
 ```php
<?php
return [
    'view_manager' => [
        'template_map' => [
            'layout/layout' => __DIR__ . '/../view/layout/layout.twig',
        ],
        'template_path_stack' => [
            __DIR__ . '/../view',
        ],
    ],
];
 ```
 
These workflow will also work with other layout parts, check the PServerCMS [config](https://github.com/kokspflanze/PServerCore/blob/master/config/module.config.php#L154) at the part `template_map`.

Hint: it works also with the `module/controller/action` name if there is no alias set for a layout page.
example: `'p-server-core/index/index' => __DIR__ . '/../view/customize/index/news.twig',`

## how to get the template alias?

In all modules, [list](https://github.com/search?q=topic%3Ap-server&type=Repositories) you can find a `config` directory with a `module.config.php` file.
In that file is also a `template_map` section where you can see the current templates, which you can overwrite. all templates have a qualified name, so you should easy understand for what if that template.

If you are note sure about the name you can also go to the view-helper, which is located in `src/MODULE/view/helper` there is a list of view-helpers, where you can see the code, that include the template_alias name again, like [sidebar](https://github.com/kokspflanze/PServerCore/blob/master/src/PServerCore/View/Helper/ServerInfoWidget.php#L32)
 
## how to call a view-helper

In all modules, [list](https://github.com/search?q=topic%3Ap-server&type=Repositories) you can find a `config` directory with a `module.config.php` file.
In that file is also a `view_helpers` section with a `aliases` part, these view-helpers you can call in all templates, in `*.twig` files is the syntax like `{{ viewHelper }}` and in `*.phtml` is it like `<?= $this->viewHelper() ?>`.

please check also [zend-guide](https://zendframework.github.io/zend-view/helpers/intro/)

see also [How to show icons in ranking](/doc/general-setup/RANKING_ICONS.md)

## Why some styles/scripts get not loaded?

Since PServerCore 1.9 we use internal the [HeadScript](https://docs.zendframework.com/zend-view/helpers/head-script/) and [HeadLink](https://docs.zendframework.com/zend-view/helpers/head-link/) system from [Zend-View](https://docs.zendframework.com/zend-view/).
That help use to set all stylesheet-files on top and all script-files on the bottom of the layout, thats improve the performance and its possible to call custom filters to minimize the size and load-time.

### What happens if i do nothing?

You will see no editor in the ticket-system.

### What i have todo?

- add `{{ headLink()|raw }}` after your custom styles in your layout
- add `{{ headScript()|raw }}` after your custom scripts in your layout

You can find an example [here](https://github.com/kokspflanze/PServerCore/commit/169214d5fd0e493216c215aeda5423e14286483b). There you see these changes and the advanced method, to change the favicon, styles and scripts directly in the system.