zsh '& disown' alias
====================

It is often need launching a GUI program with parameters from a terminal so that it runs in backgound detached from a terminal.

For eg. gedit

```sh
gedit ~/.zsh_aliases & disown
```

The zsh shell can look for alias anythere in the input, so then adding the alias

```sh
alias -g __='& disown'
```

allows to convert the above gedit example into

```sh
gedit ~/~/.zshrc __
```

##.zshrc

This [piece of shell script](.zshrc#L4-L9) also demonstrates 
including both `~/.bash_aliases` and `~/.zsh_aliases` in your zsh starting script.

### .oh-my-zsh

[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) users are encouraged to define aliases within the `ZSH_CUSTOM` folder.
Files on the custom/ directory will be automatically loaded by the init script, in alphabetical order.

So then there is (.oh-my-zsh/custom/aliases.zsh).

