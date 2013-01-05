---
layout: default
title: RubyGems
---


> **Links:** [Homepage](http://rubygems.org/)  
> **Dependencies:** [Ruby](ruby.html)  


**RubyGems** ships with Ruby 1.9+. There is nothing to install. For prior versions of Ruby, see package instructions to install RubyGems.


### Upgrade

To upgrade RubyGems.

	gem update --system


### Documentation

All gems have documentation that is generated when a gem is installed. To start the documentation web server.

	gem server

To view the documentation, point your web browser to [`http://localhost:8808/`](http://localhost:8808/).


### Automatically Starting the Documentation Server at Boot

Create a configuration file for [Launchd](http://en.wikipedia.org/wiki/Launchd).

	sudo nano /Library/LaunchDaemons/org.rubygems.gem.plist

Copy and paste the following text into the aforementioned file. The path to the `gem` executable cannot use the `rbenv` shim binary because the environment in your startup script never gets set up. Pick your primary version of Ruby and use an absolute path to the `gem` executable. Make sure you update the path in the configuration below.

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
		<key>Label</key>
		<string>org.rubygems.gem</string>
		<key>ProgramArguments</key>
		<array>
			<string>/usr/local/rbenv/versions/1.9.3-p194/bin/gem</string>
			<string>server</string>
			<string>--daemon</string>
		</array>
		<key>RunAtLoad</key>
		<true/>
		<key>KeepAlive</key>
		<true/>
	</dict>
	</plist>

And finally, execute the following command to register the configuration file with Launchd.

	sudo launchctl load -w /Library/LaunchDaemons/org.rubygems.gem.plist

If you ever want to stop your documentation server from automatically starting at boot, issue the following command.

	sudo launchctl unload -w /Library/LaunchDaemons/org.rubygems.gem.plist
