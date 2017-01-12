# nix-home

Utilities for working with user configurations in Nix.

The command delegates to nix-env, so it supports any parameter that nix-env does.

## Installation

The package for installing nix-home is on the wiki [here](https://github.com/sheenobu/nix-home/wiki/package.nix). Include it in your configuration.nix file via:

```
environment.systemPackages = [
  ((pkgs.callPackage path/to/nixhome/package.nix) { })
]
```

## Supported

`nix-home`, when invoked, builds `~/default.nix`, which must define a derivation.

nix-home calls nix-env to build a profile from the derivation. The derivation
is an overlay that gets linked into your home directory.

There is a helper function in nixhome called `mkHome`, for making the derivation:

	with import <nixpkgs> {};
	with import <nixhome> { inherit stdenv; inherit pkgs; };
	mkHome {
	  user = "username";
	  files = {
		 ".screenrc" = ./path-to-file;
		 ".vimrc" = "${somePkg}/path-to-file";
		 ".bashrc".content = ''
			... bashrc conents
		 '';
	  };
	}

