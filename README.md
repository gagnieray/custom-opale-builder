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

The result will be available in the output directory created during the process.

> [!NOTE]
> Have a look at the _[Help](#help)_ section below for a list of all the available options and commands.

> [!TIP]
> The `README.md` file in the `src/` folder will be added to your build. Customize it to your needs too.

### Favicon

You can add a custom favicon simply by adding it in the `src/favicon/` folder. The file must be named `favicon.ico`.

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

## Help

```
usage: build [-n NAME] [-o OUTPUT] [-b BASE] [-v VERSION] [-p] [-h] [{package}]

Custom Opale Redmine Theme Builder

positional arguments:
  {package}              build and package the theme in a .zip archive

options:
  -n, --name NAME        name of the theme (default: opale_customized)
  -o, --output OUTPUT    output directory where to build or package the theme (default: dist/)
  -b, --base BASE        specific Opale base branch on which to build your theme
  -v, --version VERSION  version to append to the name
  -p, --plugins          build the theme along with the existing plugins stylesheets
  -h, --help             show this help message and exit

examples:
  Build the customized theme along with the plugins based on the "redmine-5.x" branch of Opale:
  $ ./build -b redmine-5.x -p

  Build and package the theme with the name "my_theme" and version "1.0.0":
  $ ./build -n my_theme -v 1.0.0 package

  Build the theme with the name "custom_theme" directly in Redmine's themes directory:
  $ ./build -n custom_theme -o /var/www/redmine/themes
```

## Copying

_Custom Opale Redmine Theme Builder_ is licensed under the [GNU Affero General Public License v3.0 or later](https://www.gnu.org/licenses/agpl-3.0), the text of which can be found in [LICENSE](./LICENSE).
