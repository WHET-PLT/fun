Geotagging
==========
_How to setup a githook to get your current geolocation and add it to the contributors.geojson file._

1. Get the [whereami][wai] binary and put the script somewhere static or in your path (it's a pretty cool script to play with, just type whereami from the commandline to see your lat/long).*

2. Set up your git hooks directory. Either:

	a. Set up a git template directory in your home directory, `~/.git_template/` and copy over the default templates `cp -r /usr/share/git-core/templates ~/.git_template/`.
	
	b. Add the `contributors.geojson` geolocation [pre-commit hook][hook] to the `~/.git_template/hooks` directory. Make sure it is executable and it is named `pre-commit`.
	
	c. run 'git config --global init.templatedir ~/.git_template/` to tell git to source its templates/hooks from that directory.
	
	OR
	
	a. Add the `contributors.geojson` geolocation [pre-commit hook][hook] directly to the default git template directory `/usr/share/git-core/templates`. Make sure it is executable and it is named `pre-commit`.
		
3. Edit the pre-commit hook in a text editor: near the top, modify the line `PATH_TO_WHEREAMI='whereami2'` to reflect the location of the `whereami` executable (if it's in your path, the line can just read `PATH_TO_WHEREAMI='whereami\ 2'` -- I renamed it to get rid of the space; if it's not in your path you can write something like `PATH_TO_WHEREAMI='~/Desktop/whereami\ 2'` or wherever it is. Just make sure you keep it there or update the hook accordingly).

---
This uses the third party script whereami because it's stable and more accurate than the other methods I've tried. If you want to recode the hook to use another method, the next-best I've tried is using `curl http://www.geoplugin.net/json.gp?ip=$IP` where `$IP` is your current IP address. Because hey, I guess thinking you're in the netherlands every once in a while is cool…?

It only works if youre hooked up to the internet, but it won't crash if you're not and it will timeout if whereami hangs in spotty internet conditions. I think it's pretty neat to have a `contributors.geojson`.


---
*I have a folder in documents called "code" where I do all my coding, in it is a folder called "scripts" that is in my path -- to add a directory to your path add a line `export PATH=$PATH:my-new-stuff-path` (ex. `export PATH=$PATH:~/Documents/code/scripts` in my case) to your `.bashrc` or `.bash_profile` in your home directory (ex. `~/.bashrc`)




[wai]: http://d.pr/f/C2qV
[hook]: https://github.com/wfalkwallace/scripts/blob/master/githooks/pre-commit
