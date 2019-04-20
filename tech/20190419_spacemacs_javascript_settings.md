# Fixing Spacemacs, smart search does not ignore node_modules

Using Spacemacs as Javascript backend development IDE, I needed to make following changes.

- install tern, eslint, eslint-plugin-jest, jsonlint, standard npm packages globally.
- enable javascript layer
- Using spacemacs, the "smart search" function doesn't exclude node_modules. After trying for awhile,
  I updated the dotspacemacs-search-tools, switched to Ack. Smart search started to ignore node_modules.
- add .tern-project in the project root directory
- add .eslintrc in the project root directory

```sh
npm install -g eslint eslint-plugin-jest tern jsonlint standard
```

```.spacemacs
   dotspacemacs-configuration-layers
   '(
     git
     markdown
     syntax-checking
     version-control
     html
     javascript
   ..
   ;; updated the search tools order to ack first.
   dotspacemacs-search-tools '("ack" "ag" "pt" "grep")
(defun dotspacemacs/user-init ()
  ;; to tell js2-mode that we are working with node modules
  (setq js2-include-node-externs t)

```

.tern-project file:
```json
{
  "libs": [ ],
  "loadEagerly": false,
  "plugins": {
            "commonjs": {},
            "node": {},
            "requirejs": {},
            "node_resolve": {}
  }
}
```

.eslintrc.json
```json
{
    "env": {
        "browser": true,
        "commonjs": true,
        "es6": true,
        "node": true,
        "jest/globals": true
    },
    "plugins": ["jest"],
    "extends": [
        "eslint:recommended",
        "plugin:jest/recommended"
    ],
    "globals": {
        "process": "readonly",
        "exports": "writable"
    },
    "parserOptions": {
        "ecmaVersion": 2018
    },
    "rules": {
        "no-console": "off",
        "no-process-env": "off",
        "jest/no-disabled-tests": "warn",
        "jest/no-focused-tests": "error",
        "jest/no-identical-title": "error",
        "jest/prefer-to-have-length": "warn",
        "jest/valid-expect": "error"
    }
}
```

This should fix issues including:
- spc m g g , or g d
- javascript lint error checking
- autocomplete

Learned js2-include-node-externs from [here](https://simpletutorials.com/c/2799/How%20to%20resolve%20%26quot%3BUndeclared%20variable%20or%20function%20%26%23x27%3Bmodule%26%23x27%3B%26quot%3B%20error%20thrown%20by%20Tern%20in%20Spacemacs)

Learned auto-complete and go-to-definition across files from [here](https://simpletutorials.com/c/2792/How%20to%20setup%20Spacemacs%20for%20auto-complete%20and%20go-to-definition%20across%20files)


You can find my .spacemacs file [here](https://github.com/neilhan/docker_collection/blob/master/serverless/container/home/.spacemacs)

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
