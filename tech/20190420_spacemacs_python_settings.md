# Spacemacs setup for python development

Using Spacemacs as Python3 backend development IDE, I needed to make following changes.

- install python3-venv and pudb for go-to-definition to work properly
- python3 language needs flycheck-python-pycompile-executable to be set to "python3"
- env PYTHONPATH may also be set properly.

to have go-to-definition working properly, the project needs a venv and activation in emacs.
```sh
cd your_project_dir
python3 -m venv env
... in emacs:
spc m V a then select ./env/
```

.spacemacs file:
```.spacemacs
   dotspacemacs-configuration-layers
   '(
     git
     markdown
     syntax-checking
     version-control
     python
   ..
   ;; updated the search tools order to ack first.
   dotspacemacs-search-tools '("ack" "ag" "pt" "grep")

(defun dotspacemacs/user-config ()
  (setq flycheck-python-pycompile-executable "python3")
```

This should fix issues including:
- spc m g g , or g d
- autocomplete

## debugging
I found debugging is still not as good as PyCharm. I use [Pudb](https://pypi.org/project/pudb/) for debugging.

You can find my .spacemacs file [here](https://github.com/neilhan/docker_collection/blob/master/serverless/container/home/.spacemacs)

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
