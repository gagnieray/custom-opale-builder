# Custom Opale Redmine Theme Builder

This repository includes [Opale Redmine Theme](https://github.com/gagnieray/opale) as a Git submodule.

To initialize and fetch _Opale_ after cloning, run:

```bash
git submodule update --init --recursive
```

Or, do everything in one step when cloning:

```bash
git clone --recurse-submodules https://github.com/gagnieray/custom-opale-builder.git my_custom_opale
```

This ensures _Opale_ is downloaded and checked out at the correct commit.

## How-to

If you want to customize [Opale Redmine Theme](https://github.com/gagnieray/opale) to your needs, first, make sure that you have installed [Node.js](https://nodejs.org/) and `npm` is available in your terminal.

All the variables defined in `src/opale/src/sass/_variables.scss` with the `!default` flag can be overridden in `src/_custom-variables.scss`.

Example:

```scss
@use 'variables' with (
  $sidebar-position: right,
  $brand-primary: #614ba6
);
```

Then, run the script from the project root directory:

```bash
./build
``` 

The result will be available in the `dist/` folder created during the process, ready to be installed in your Redmine's `themes` folder.

> [!NOTE]
> Have a look at the _[Help](#help)_ section below for a list of all the available options and commands.

> [!TIP]
> The `README.md` file in the `src/` folder will be added to your build. Customize it to your needs too.

> [!IMPORTANT]
> Keep _Opale_ up to date running `git pull origin <branch>` from the `src/opale/` folder.

> [!CAUTION]
> If you customize the theme for _Redmine 5.x_, be sure to use the `-p redmine-5.x` option

### Favicon

You can add a custom favicon simply by adding it in the `src/favicon/` folder. The file must be named `favicon.ico`.

If you don't need a custom favicon, delete the `src/favicon/` folder.

### Logo

You can add a logo to be displayed in the pages' header. 

In order to do that :

1. Add your logo in the `src/images/logo/` folder. The file must be named `logo.png`.
2. Define the required variables in `src/_custom-variables.scss`.
   
   ```scss
   @use 'variables' with (
     $use-logo: true,
     $logo-image-width: 150px,
     $logo-image-height: 60px,
     $header-padding-vertical: 25px, // Only required if $logo-image-height > 40px
     // ...
   );
   ```

> [!CAUTION]
> If your logo's height is greater than 40px, you will have to adjust `$header-padding-vertical` default value which controls the header's minimal height.

If you don’t need a logo, simply delete the `src/images/` folder.

## Help

```
Usage: ./build [OPTIONS] <COMMAND>

Options:
  -b BASE     Opale base branch to use (default: master)
  -n NAME     Package name (default: opale_customized)
  -p yes/no   Include plugins stylesheets (default: no)
  -v VERSION  Package version (optional)
  -h          Display this help message

Commands:
  package     Build and package the theme into a .tar.gz archive
  help        Display this help message

Examples:
  ./build -b redmine-5.x -p yes
  ./build -n my_theme -v 1.0.0 package
  ./build -b redmine-6.x -n custom_theme -v 2.1.0 package

Notes:
  - Options must be placed before the command
  - Version is optional; if provided, it's appended to the package name
  - The script must be run from the project root directory
```

## Copying

_Custom Opale Redmine Theme Builder_ is licensed under the [GNU Affero General Public License v3.0 or later](https://www.gnu.org/licenses/agpl-3.0), the text of which can be found in [LICENSE](./LICENSE).
