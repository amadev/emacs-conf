# emacs-conf — agent rules

## Source of truth

`emacs.org` is the **only** source of truth for Emacs configuration. `~/.emacs.d/init.el`
is a *generated* artifact, tangled from `emacs.org` (see `emacs.org`'s `:header-args:
:tangle ~/.emacs.d/init.el`).

- **Never** hand-edit `~/.emacs.d/init.el` (or `init2.el`) as the final change — edits
  there are lost on the next tangle and leave the repo out of sync with what's running.
- If you edit `init.el` directly first for quick live-testing via `emacsclient`, always
  port the change into the matching `#+BEGIN_SRC elisp :tangle ~/.emacs.d/init.el` block
  in `emacs.org` afterward, then re-tangle so `init.el` is regenerated from org — don't
  leave the two diverged.
- To re-tangle and reload after editing `emacs.org`: run `M-x
  amadev/tangle-and-reload-init` in the running Emacs (or via `emacsclient -s
  /run/user/1000/emacs/server -e "(amadev/tangle-and-reload-init)"`), which tangles
  `emacs.org` → `init.el` and reloads it in place.

## Live Emacs instance

The user runs a single long-lived self-built Emacs 30.1 GUI instance
(`~/s/emacs-30.1/src/emacs`, launched via `~/bin/em`), reachable via
`emacsclient -s /run/user/1000/emacs/server -e "..."`. Prefer evaluating changes there to
verify behavior before/after editing `emacs.org`, rather than assuming a restart is
needed.
