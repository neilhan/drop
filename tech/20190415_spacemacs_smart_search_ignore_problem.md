# Fixing Spacemacs, smart search does not ignore node_modules

Using spacemacs, the "smart search" function doesn't exclude node_modules. After trying for awhile,
I updated the dotspacemacs-search-tools, switched to Ack. Smart search started to ignore node_modules.

```.spacemacs
   ..
   dotspacemacs-search-tools '("ack" "ag" "pt" "grep")
   ..
```

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
