eslint Docker image
===================

[eslint](https://eslint.org/) as standalone Docker image.

The image is based on `node:10-alpine`. The version identifier refers the
eslint version (e.g. `code-freak/eslint:5.9.0` uses eslint v5.9.0).  
Beside the eslint executable itself the image also contains the popular styles
from [Google](https://github.com/google/eslint-config-google), [Airbnb](https://github.com/airbnb/javascript) and [Standard](https://github.com/standard/standard).
These styles are installed globally including their required peer-dependencies.

***Word of warning***: Because eslint is installed globally it will fail to load
plugins and styles installed locally from your `package.json`. This image is only
meant for simple usages where you provide a simple `.eslintrc` configuration. In
most advanced cases this image will be useless for you and you should work with
the local copy of eslint inside your `node_modules/.bin/` directory so it can
find all local plugins, rules, etc. Your *could* provide a `NODE_PATH` environment
variable that points to your local `node_modules` directory but this might lead
to a broken setup.

# Usage
Create a simple `.eslintrc` file next to your `package.json` with the following
contents (checks your code based on the JS Standard style):
```json
{
  "extends": "standard"
}
```

Afterwards you can lint your code with docker:
```console
$ docker run --rm -t -v $(pwd):/code --workdir /code code-freak/eslint:latest eslint '**/*.js'
```

You can try this inside the `example` directory which already contains
a `.eslintrc` file.

# License
Copyright (C) 2018 Code FREAK

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
