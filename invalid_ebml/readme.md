# valid files

## reference.mkv

A reference file was produced via:

```
ffmpeg -f lavfi -i mandelbrot=s=320x280:r=25 -f lavfi -i sine -t 0.5 -c:v ffv1 -c:a flac reference.mkv
mkclean reference.mkv
```

# invalid files

## no_DocType.mkv

The EBML Header contains no mandated DocType Element.

[no_DocType.mkv](no_DocType.mkv)

## docTypeReadVersion_greaterthan_docTypeVersion.mkv

The docTypeReadVersion MUST be less than docTypeVersion but here it isn't.

[docTypeReadVersion_greaterthan_docTypeVersion.mkv](docTypeReadVersion_greaterthan_docTypeVersion.mkv)

## EBMLReadVersion_greaterthan_EBMLVersion.mkv

The EBMLReadVersion MUST be less than EBMLVersion but here it isn't.

[EBMLReadVersion_greaterthan_EBMLVersion.mkv](EBMLReadVersion_greaterthan_EBMLVersion.mkv)
