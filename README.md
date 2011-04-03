sunaku's Ruby wmiirc
==============================================================================

This is a [Ruby][1] and [YAML][2] based configuration of the [wmii][3]
window manager.  It manipulates wmii through the [Rumai][4] library,
which comes with an [interactive shell][5] for live experimentation.

[1]: http://ruby-lang.org
[2]: http://yaml.org
[3]: http://wmii.suckless.org
[4]: http://snk.tuxfamily.org/lib/rumai/
[5]: http://snk.tuxfamily.org/lib/rumai/#EXAMPLES

This configuration is also discussed in the following articles:

* <http://wmii.suckless.org/alternative_wmiirc_scripts>
* <http://snk.tuxfamily.org/log/wmii-3.1-ruby-config.html>
* <http://article.gmane.org/gmane.comp.window-managers.wmii/1704>

------------------------------------------------------------------------------
Prerequisites
------------------------------------------------------------------------------

* wmii 3.9 or newer     -  <http://wmii.suckless.org>

  The `display/status/arrange` status bar applet requires a [patched version
  of wmii-hg r2758]( http://code.google.com/p/wmii/issues/detail?id=232 ).

* Ruby 1.9 or newer     -  <http://www.ruby-lang.org>
* Rumai 4.1.0 or newer  -  `gem install rumai -v '>= 4.1.0'`

------------------------------------------------------------------------------
Installing
------------------------------------------------------------------------------

Backup:

    mv ~/.wmii ~/.wmii.backup
    mv ~/.wmii-hg ~/.wmii-hg.backup

Install:

    git clone git://github.com/sunaku/wmiirc.git ~/.wmii
    ln -s ~/.wmii ~/.wmii-hg

Branch:

    cd ~/.wmii
    git checkout -b personal
    cp -vb EXAMPLE.config.yaml config.yaml

------------------------------------------------------------------------------
Configuring
------------------------------------------------------------------------------

* Edit `~/.wmii/config.yaml` to your liking. For a real-life example,
  see [my personal configuration file](
  http://github.com/sunaku/wmiirc/blob/personal/config.yaml).

* If wmii is already running, run `~/.wmii/wmiirc` or
  invoke the "reload" action to apply your changes.

------------------------------------------------------------------------------
Running
------------------------------------------------------------------------------

* Ensure that your `~/.xinitrc` supports crash recovery by allowing you to
  restart wmii without losing your applications if it crashes or if you
  accidentally kill it:

        xterm -e tail -F ~/.wmii/wmiirc.log &

        while true; do
          ck-launch-session wmii
          xmessage 'Do you really want to quit wmii?' \
                   -buttons 'Yes:0,No:1' -center \
                   -default 'No' -timeout 30 \
          && break
        done

* If wmii is already running, run `~/.wmii/wmiirc` to start the configuration.
  Otherwise, run `startx` normally and wmii will automatically recognize and
  apply this configuration.

------------------------------------------------------------------------------
Upgrading
------------------------------------------------------------------------------

    # assuming that "origin" points to github.com/sunaku/wmiirc
    git fetch origin
    git checkout master
    git rebase origin/master
    git checkout personal
    git rebase master

------------------------------------------------------------------------------
Hacking
------------------------------------------------------------------------------

To use the development version of Rumai directly from its source code
repository (instead of the currently published gem version), do this:

    cd ~/.wmii
    git clone git://github.com/sunaku/rumai.git
    sed '2a$:.unshift File.expand_path("../rumai/lib", __FILE__)' -i wmiirc

------------------------------------------------------------------------------
Contributing
------------------------------------------------------------------------------

Fork this project on GitHub and send pull requests.

------------------------------------------------------------------------------
Bugs, Features, Issues, Questions
------------------------------------------------------------------------------

File a report on [the issue tracker](http://github.com/sunaku/wmiirc/issues/).

------------------------------------------------------------------------------
License
------------------------------------------------------------------------------

Released under the ISC license.  See the LICENSE file for details.
