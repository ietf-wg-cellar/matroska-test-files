# valid files

## reference.mkv

A reference file was produced via:

```
ffmpeg -f lavfi -i mandelbrot=s=320x280:r=25 -f lavfi -i sine -t 0.5 -c:v ffv1 -c:a flac reference.mkv
mkclean reference.mkv
```

