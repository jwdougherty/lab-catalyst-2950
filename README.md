# lab-catalyst-2950
Notes on configuring a catalyst 2950 for the home lab.

# Trouble booting up
This particular switch gets stuck booting up. The status light flashes orange, but never turns green. The console never shows any output.
If I interupt the boot process by holding down the mode button, then the prompt loads. From the rescue prompt I am able to load the ios by:

```
flash_init
load_helper
boot
```



