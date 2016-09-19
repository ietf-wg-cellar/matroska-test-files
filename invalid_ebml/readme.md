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

## invalid_EBMLMaxIDLength.mkv

Using an invalid EBMLMaxIDLength value of `3`.

[invalid_EBMLMaxIDLength.mkv](invalid_EBMLMaxIDLength.mkv)

## higher_EBMLMaxSizeLength_than_matroska_allows.mkv

Matroska limits EBMLMaxSizeLength to `8` but this file uses `9`.

[higher_EBMLMaxSizeLength_than_matroska_allows.mkv](higher_EBMLMaxSizeLength_than_matroska_allows.mkv)

## lower_EBMLMaxSizeLength_than_elements_are_using.mkv

The EBMLMaxSizeLength is set to `4` but the file contains one Element (a Void) which uses an Element Data Size of `6`.

[lower_EBMLMaxSizeLength_than_elements_are_using.mkv](lower_EBMLMaxSizeLength_than_elements_are_using.mkv)

## inefficient_elementid.mkv

The EBML Version Element ID is written as 0x200286 rather than as 0x4286.

[inefficient_elementid.mkv](inefficient_elementid.mkv)

## unknown_element.mkv

An unknown element (with Element ID 0x81) is stored at the beginning of the EBML Header. 

[unknown_element.mkv](unknown_element.mkv)

## unknown_sized_non_master_element.mkv

A non-Master Element (DocType) uses an unknown Element Data Size.

[unknown_sized_non_master_element.mkv](unknown_sized_non_master_element.mkv)

## crc_element_has_invalid_hash.mkv

The CRC-32 Element in the EBML Header contains an invalid hash.

[crc_element_has_invalid_hash.mkv](crc_element_has_invalid_hash.mkv)

## crc_element_is_not_first.mkv

The CRC-32 Element in the EBML Header is not the first Child Element of its Parent Element.

[crc_element_is_not_first.mkv](crc_element_is_not_first.mkv)

## non_ascii_in_string_element.mkv

A string element (Track/Language) starts with a non-ascii 0x19 octet.

[non_ascii_in_string_element.mkv](non_ascii_in_string_element.mkv)

## invalid_boolean.mkv

A Unsigned Integer Element that is defined for boolean use contains a non-boolean value (in this case FlagLacing).

[invalid_boolean.mkv](invalid_boolean.mkv)

## element_outside_of_size_range.mkv

The SegmentUID has an Element Data Size of 8 although 16 is required per its definition.

[element_outside_of_size_range.mkv](element_outside_of_size_range.mkv)


