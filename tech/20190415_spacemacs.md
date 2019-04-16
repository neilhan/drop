# Fixing Spacemacs, smart search does not ignore node_modules

Using spacemacs, the "smart search" function doesn't exclude node_modules. After trying for awhile,
I updated the dotspacemacs-search-tools, switched to Ack. Smart search started to ignore node_modules.

```.spacemacs
   ..
   dotspacemacs-search-tools '("ack" "ag" "pt" "grep")
   ..
```

# Fixing Spacemacs Ctrl-i Ctrl-m

With Evil mode, I hoping the ctrl-o and ctrl-i work as Vim does.

However emacs treats ctrl-i as Tab key, and ctrl-m as Enter key.
To fix this, add the following three lines to ~/.spacemacs file "(defun dotspacemacs/user-config".
With display-graphic-p ctrl-i and ctrl-m will only be set when running with GUI.

```.spacemacs
(defun dotspacemacs/user-config ()
  ..
  (when (display-graphic-p)
    (define-key input-decode-map [?\C-i] [C-i])
    (define-key input-decode-map [?\C-m] [C-m]))
  ..
)
```

Restart or refresh SPC f e R, and that will have the ctrl-i working in the evil mode forward.

Ctrl-m is enter key in a terminal.

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
