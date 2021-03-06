---
layout: default
---

# Welcome to 2's Complement

My name is Kevin Yokley and I write code.

### A work in progress...
My goal for this page is to be a place for me to collect my thoughts and possibly showcase some of the things I'm working on. As such, this site may be in a constant state of flux. Check back often!

## Posts

<ul>
	{% for post in site.posts limit: 20 %}
		<li>
			  <a href="{{ post.url }}">{{ post.title }}</a>
			  {{ post.date | date_to_string }}
			  <p>{{ post.excerpt | remove: '<p>' | remove: '</p>' }}</p>
		</li>
	{% endfor %}
</ul>

## Gists
- Vim Hooks - Some writeups on how to automate some syntax checks to help write better code
	1. [Trailing whitespace handling](https://gist.github.com/kyokley/944de46ab0b35ef4df14)
	2. [Handling syntax errors](https://gist.github.com/kyokley/0d7bb03eede831bea3fa)
	3. [Static analysis for security](https://gist.github.com/kyokley/3e868a6575d28cb4020694876d8f16b7)
- [VCS commands in Vim](https://gist.github.com/kyokley/c10ff97148a6533116ac714ad6fb5ac2)

## Projects
- [BattlePy](https://github.com/kyokley/BattlePyAI) - Framework for creating AIs to play a Battleship-like game
- [Psql pager in Vim](https://github.com/kyokley/vim-psql-pager) - A pager designed for psql with convenience in mind
- [Bitcoin Failsafe](https://github.com/kyokley/bitcoin_failsafe) - Create linked and recoverable bitcoin accounts in case of the worst
- [Confuse](https://github.com/kyokley/confuse) - I18n tool to replace common ascii with easily confusable unicode characters
- [LockBox](https://github.com/kyokley/lockbox) - Simple Passphrase-based AES Encryption
- [Color Blame](https://github.com/kyokley/color_blame) - Colorize VCS blame command output

## How I work
Below are repos that contain the various config files for my development environments
- [Dotfiles](https://github.com/kyokley/dotfiles) (These are a collection of general configs)
- [NeoVim](https://github.com/kyokley/nvimRepo)
- [Vim](https://github.com/kyokley/vimRepo) (I mostly use NeoVim exclusively now so this repo is not actively updated.)
- Zsh with [Prezto](https://github.com/kyokley/prezto)

## About Me
Learn a bit [about me]({{ site.baseurl }}{% link aboutme.md %})
