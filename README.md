# Progressive Prompt

Allow rendering a prompt immediately, then spend time making it progressively more informative without blocking work.

`.zshrc`:
```zsh
TRAPALRM() {
  if [[ -n "$WIDGET" ]]; then
    zle reset-prompt
  fi
}
function __progressive_prompt_exec_incr() {
  __progressive_prompt_exec_no=$((__progressive_prompt_exec_no+1))
}
precmd_functions+=(__progressive_prompt_exec_incr)
setopt PROMPT_SUBST
PROMPT='$(progressive_prompt $$ $__progressive_prompt_exec_no "\$ " prompt)'
```

`prompt` should be an executable that outputs iterative prompts separated by null bytes, in theory becoming more and more informative. A dummy example is provided.

## Credits

This owes its inspiration to https://github.com/burke/async-shell-prompt
