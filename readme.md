# Creating an uxn/varvara userland 

Get the emulator starter pack from the [100r uxn page][uxn]

Put the applications (uxnemu, uxnlin, uxncli)into `~/bin`

Get the [roms][roms]

[uxn]: https://100r.co/site/uxn.html
[roms]: https://wiki.xxiivv.com/site/roms.html

https://100r.co/site/uxn_guide.html


Put this at the end of your `.bashrc`:

```
export PATH=$PATH:$HOME/bin
alias left='uxnemu $HOME/roms/left.rom'
```

Or you can use this little script I wrote to auto-hookup all roms in the directory:

```
export PATH=$PATH:$HOME/bin
#alias left='uxnemu $HOME/roms/left.rom'
#alias turye='uxnemu $HOME/roms/turye.rom'
for rom in $HOME/roms/*.rom; do
  rom_name=$(cut -d / -f 5 <<< $rom)
  alias_name=$(cut -d . -f 1 <<< $rom_name)
  alias $alias_name="uxnemu $rom"
done
```

That'll only work if your roms are in e.g. `/home/ste/roms/left.rom`

If there are more/fewer segments in your path, you'll have to change the number `5` above to suit.

## Compiling a rom from source

Get the source from sourcehut, using git:

```
mkdir ~/git
cd ~/git
git clone https://git.sr.ht/~rabbits/adelie
cd adelie
./build.sh
```

Most of the build scripts will copy the compiled rom to your `~/roms` directory. Otherwise you can run:

```
uxnasm src/adelie.tal ~/roms/adelie.rom
```

To build directly to your roms dir.

By outputting to `~/roms`, you can re-run your `.bashrc` to immediately hook-up an alias for the new app:

```
source ~/.bashrc
adelie
``` 

...should launch the newly-built rom.

## Varvara control notes

On Linux

A = Ctrl
B = Alt
S = Shift

## Theme

Four colours expressed as RRRR GGGG BBBB so the triplets go together but aren't written together.

E.g. The default potato theme has the four colours: `5ba, 077, 000, fff` which looks like this in dexe: `500f b70f a70f`

A theme is binary, not ASCII text. Edit themes using `potato` if you want a GUI, or `dexe` for fine control and to see how things work.

Potato also saves your configured pattern preference into the `.theme` file.

The fun thing with dexe is when you `dexe .theme`, if it's in the current working directory, then dexe itself is displayed in your theme, so you get visual feedback (but you'd have to save and re-open after making changes to see them reflected).

## Adelie

By default, the background color is 00 and the blending mode is 00, which will mean that any elements you add are like-colour-on-itself... invisible.

Slides can have names but they're optional. 

So, the minimal viable Adelie presentation is:

```
MODE 03
HEAD Hello World
```

(You can substitute another mode like `0c`)

FILL There are only four options, 00 to 03, corresponding to the colors of your theme, or if there is no theme, then black, dark grey, light grey, white. If you use a number greater than 03, it will roll over, so 04 == 00, etc.

MODE The blending options can be seen in the demo presentation (inside the adelie repo directory, run `adelie slides`) or use this sample presentation to see for yourself:



