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

## currently_undefined_EBMLVersion.mkv

The EBMLVersion is restricted to a range of defined values. At the time of this writing, only EBMLVersion=1 is defined. This value has an EBMLVersion of 255.

[currently_undefined_EBMLVersion.mkv](currently_undefined_EBMLVersion.mkv)


## level_0_crc.mkv

The CRC-32 Element is not allowed at Level 0 but here it is included in between the EBML Header and Segment Element.
[level_0_crc.mkv](level_0_crc.mkv)

## too_many_copies_of_DocTypeVersion.mkv

DocTypeVersion has maxOccurs=1 but here it is included twice in the EBML Header.

[too_many_copies_of_DocTypeVersion.mkv](too_many_copies_of_DocTypeVersion.mkv)

## too_many_copies_of_DocTypeVersion_and_conflicting_values.mkv

Similar to [too_many_copies_of_DocTypeVersion.mkv](too_many_copies_of_DocTypeVersion.mkv) but here the two copies of DocTypeVersion include conflicting values, `3` and `4`.

[too_many_copies_of_DocTypeVersion_and_conflicting_values.mkv](too_many_copies_of_DocTypeVersion_and_conflicting_values.mkv)

## invalid_EBML_ElementDataSize_in_EBMLHeader.mkv

The Elements of the EBML Header are restricted to Element Data Size values that are 4 octets in length or less. This file includes a 5 octet long Element Data Size for DocType.

[invalid_EBML_ElementDataSize_in_EBMLHeader.mkv](invalid_EBML_ElementDataSize_in_EBMLHeader.mkv)

## really_invalid_EBML_ElementDataSize_in_EBMLHeader.mkv

Similar to [invalid_EBML_ElementDataSize_in_EBMLHeader.mkv](invalid_EBML_ElementDataSize_in_EBMLHeader.mkv) but the Element Data Size of the DocType Element is 9 octets long.
[really_invalid_EBML_ElementDataSize_in_EBMLHeader.mkv](really_invalid_EBML_ElementDataSize_in_EBMLHeader.mkv)

