# Commands Cheatsheets

List of commands that i use occasionaly so keeping it documented here so i can retrive them easily when ever i need 'em.

## MOV to GIF converter

```shell
ffmpeg -v warning -ss 2 -t 5 -i INPUT.MOV -vf scale=320:-1 -gifflags -transdiff -y OUTPUT.gif
```