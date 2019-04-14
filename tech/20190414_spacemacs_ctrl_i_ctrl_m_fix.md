# Fixing Spacemacs Ctrl-i Ctrl-m

For Evil mode, I am hope the ctrl-o and ctrl-i work as Vim does. 

However emacs treat ctrl-i as Tab key, and ctrl-m as Enter key. 
To fix that, add the following two lines to .spacemacs file "(defun dotspacemacs/user-config". 

```.spacemacs
(defun dotspacemacs/user-config ()
  ..
  (define-key input-decode-map [?\C-i] [C-i])
  (define-key input-decode-map [?\C-m] [C-m])
  ..
)
```

Restart or refresh SPC f e R, and that will have the ctrl-i working in the evil mode forward.

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
